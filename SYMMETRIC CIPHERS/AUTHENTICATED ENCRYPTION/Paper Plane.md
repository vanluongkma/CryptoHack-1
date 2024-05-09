## Paper Plane
![image](https://hackmd.io/_uploads/SycZ9O5cp.png)
![image](https://hackmd.io/_uploads/SkBqGas9a.png)
```Python
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad, unpad
import os


KEY = ?
FLAG = ?


class AesIge:
    def __init__(self, key):
        self.cipher = AES.new(key, AES.MODE_ECB)

    def encrypt(self, data, m0=os.urandom(16), c0=os.urandom(16)):
        data = pad(data, 16, 'pkcs7')

        last_block_plaintext = m0
        last_block_ciphertext = c0
        result = b''
        for i in range(0, len(data), 16):
            block = data[i: i + 16]
            x = AesIge._xor_blocks(block, last_block_ciphertext)
            x = self.cipher.encrypt(x)
            x = AesIge._xor_blocks(x, last_block_plaintext)
            result += x

            last_block_plaintext = block
            last_block_ciphertext = x

        return result, m0, c0

    def decrypt(self, data, m0, c0):
        last_block_plaintext = m0
        last_block_ciphertext = c0
        result = b''

        for i in range(0, len(data), 16):
            block = data[i: i + 16]
            x = AesIge._xor_blocks(block, last_block_plaintext)
            x = self.cipher.decrypt(x)
            x = AesIge._xor_blocks(x, last_block_ciphertext)
            result += x

            last_block_ciphertext = block
            last_block_plaintext = x

        if AesIge._is_pkcs7_padded(result):
            return unpad(result, 16, 'pkcs7')
        else:
            return None

    @staticmethod
    def _is_pkcs7_padded(message):
        padding = message[-message[-1]:]
        return all(padding[i] == len(padding) for i in range(0, len(padding)))

    @staticmethod
    def _xor_blocks(a, b):
        return bytes([x ^ y for x, y in zip(a, b)])



@chal.route('/paper_plane/encrypt_flag/')
def encrypt_flag():
    ciphertext, m0, c0 = AesIge(KEY).encrypt(FLAG.encode())
    return {"ciphertext": ciphertext.hex(), "m0": m0.hex(), "c0": c0.hex()}


@chal.route('/paper_plane/send_msg/<ciphertext>/<m0>/<c0>/')
def send_msg(ciphertext, m0, c0):
    ciphertext = bytes.fromhex(ciphertext)
    m0 = bytes.fromhex(m0)
    c0 = bytes.fromhex(c0)
    if len(ciphertext) % 16 != 0:
        return {"error": "Data length must be a multiple of the blocksize!"}
    if len(c0) != 16 or len(m0) != 16:
        return {"error": "m0 and c0 must be 16 bytes long!"}

    plaintext = AesIge(KEY).decrypt(ciphertext, m0, c0)
    if plaintext is not None:
        return {"msg": "Message received"}
    else:
        return {"error": "Can't decrypt the message."}

```
- Trước hết thì ta sẽ tìm hiểu về `Padding Oracle Attack`. Hãy xem qua video [sau](https://www.youtube.com/watch?v=uDHo-UAM6_4).
- Padding Oracle là một kỹ thuật lợi dụng việc xác thực padding của một thông điệp được mã hóa để giải mã nội dung thông điệp đó.
- Ta có hiểu như sau: 
	- Lấy ciphertext được mã hóa.
	- Sửa đổi một byte trong ciphertext.
	- Gửi ciphertext được chỉnh sửa đến sever.
	- Sever sẽ phản hồi thông tin về việc padding có hợp lệ hay không.
    - Phân tích phản hồi để suy ra vị trí byte bị lỗi trong padding.
    - Sửa đổi ciphertext một lần nữa để sửa lỗi padding.
    - Lặp lại quá trình này cho đến khi giải mã được toàn bộ plaintext.
- Source solve:
```Python
import requests
from pwn import xor
from Crypto.Util.number import *

def encrypt_flag():
    url = 'https://aes.cryptohack.org/paper_plane/encrypt_flag/'
    r = requests.get(url).json()
    return bytes.fromhex(r['ciphertext']), bytes.fromhex(r["m0"]), bytes.fromhex(r["c0"])

def send_msg(ciphertext, m0, c0):
    url = 'https://aes.cryptohack.org/paper_plane/send_msg/'
    url += ciphertext.hex() + "/" + m0.hex() + "/" + c0.hex()
    r = requests.get(url).json()
    return  'error' not in r


def decrypt_block(ctt, m0, c0):
    plaintext = b""
    new_xor = b""
    for i in range(1, 17):
        tmp = c0[:16-i]
        for j in range(255, -1, -1):
            if len(plaintext) > 0:
                pad = long_to_bytes(i)*(i-1)
                send = tmp + long_to_bytes(j) + xor(pad, new_xor)
            else:
                send = tmp + long_to_bytes(j)
            if send_msg(ctt, m0, send):
                new_xor = xor(long_to_bytes(i),(j)) +new_xor
                plaintext = xor(xor(long_to_bytes(i),(j)), (c0[16-i:17-i])) + plaintext 
                print(plaintext)
                break
    return plaintext

ciphertext, m0, c0 = encrypt_flag()
print(c0.hex())
ciphertext1 = ciphertext[:16]
ciphertext2 = ciphertext[16:]

pt1 = decrypt_block(ciphertext1, m0, c0)
print("block1 done")
print(f"{pt1 = }")
pt2 = decrypt_block(ciphertext2, pt1, ciphertext1)

print("flag: " , pt1 + pt2 )
#Source: ldv
```
- Flag: `crypto{h3ll0_t3l3gr4m}`
