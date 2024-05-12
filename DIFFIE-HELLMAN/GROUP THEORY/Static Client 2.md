## Static Client 2
![image](https://hackmd.io/_uploads/BJ_RB4m26.png)
- Với chall này ta nhận thấy không thể giải như chall `Static Client` do đã Bob đã nghi ngờ thông tin ta gửi đến. Nên ta sẽ phải làm cách khác.
- Ta sẽ thử sử dụng `Pohlig_hellman` để làm.
```Python
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad, unpad
import hashlib
from pwn import *
import json
from Crypto.Util.number import *
def is_pkcs7_padded(message):
    padding = message[-message[-1]:]
    return all(padding[i] == len(padding) for i in range(0, len(padding)))
def decrypt_flag(shared_secret: int, iv: str, ciphertext: str):
    sha1 = hashlib.sha1()
    sha1.update(str(shared_secret).encode('ascii'))
    key = sha1.digest()[:16]
    ciphertext = bytes.fromhex(ciphertext)
    iv = bytes.fromhex(iv)
    cipher = AES.new(key, AES.MODE_CBC, iv)
    plaintext = cipher.decrypt(ciphertext)

    try:
        return plaintext.decode('ascii')
    except UnicodeDecodeError:
        try:
            return plaintext.decode('utf-8')
        except UnicodeDecodeError:
            return str(plaintext)

def smooth_p():
    Smooth_p = 1
    i = 2
    while Smooth_p < p or not isPrime(Smooth_p+1):
        Smooth_p *= i
        i += 1
    Smooth_p += 1
    return Smooth_p
r = remote("socket.cryptohack.org", 13378)
r.recvuntil(b"Intercepted from Alice: ")
recv = r.readline().strip()
recv= json.loads(recv)
p= int(recv["p"], 16)
g= recv["g"]
A= recv["A"]
r.recvuntil(b"Intercepted from Bob: ")
recv = r.readline().strip()
recv= json.loads(recv)
B= int(recv["B"], 16)
r.recvuntil(b"Intercepted from Alice: ")
recv = r.readline().strip()
recv= json.loads(recv)
iv= recv["iv"]
ciphertext= recv["encrypted"]
p1= smooth_p()
r.recvuntil("Bob connects to you, send him some parameters: ")
r.sendline(json.dumps({"p": hex(p1), "g": g, "A": A}))
r.recvuntil("Bob says to you: ")
recv = r.readline().strip()
recv= json.loads(recv)
B= int(recv["B"], 16)
from sympy.ntheory.residue_ntheory import *
b= discrete_log(p1, B, 2)
shared_secret= pow(int(A, 16), b, p)
print(decrypt_flag(shared_secret, iv, ciphertext))
```
![image](https://hackmd.io/_uploads/Hy3okrmn6.png)

- Flag: `crypto{uns4f3_pr1m3_sm4ll_oRd3r}  `
