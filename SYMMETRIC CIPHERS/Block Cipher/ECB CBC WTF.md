## ECB CBC WTF
![image](https://hackmd.io/_uploads/ryQuAkcc6.png)
- Chall cung cấp thông tin về CBC, ECB. Source chall cho ta biết flag được mã hóa bằng CBC như lại được giải mã bằng ECB.
- Ta có sơ đồ encrypt CBC:
![image](https://hackmd.io/_uploads/rkCfklq9a.png)
- Sơ đồ decrypt ECB:
![image](https://hackmd.io/_uploads/S1kryg996.png)
- Từ source ta biết output của encrypt sẽ là IV(16Bytes)+ encrypt.
- Từ đó ta có được IV. Ta thấy CBC với ECB khác nhau ở bước xor.
```Python
from Crypto.Cipher import AES
from Crypto.Util.Padding import*
from pwn import xor
import requests
url = 'https://aes.cryptohack.org/ecbcbcwtf/'
def encrypt_flag():
	r = requests.get(f"{url}/encrypt_flag")
	js = r.json()
	return (js["ciphertext"])

def decrypt(ciphertext):
	r = requests.get(f"{url}/decrypt/{ciphertext}")
	js = r.json()
	return (js["plaintext"])

cipher = encrypt_flag()
plaintext = decrypt(cipher)

iv1 = bytes.fromhex(cipher[:32])
ciphertext = cipher[32:]

iv2 = bytes.fromhex(ciphertext[:32])

plaintext1 =  bytes.fromhex(plaintext[32:64])
plaintext2 = bytes.fromhex(plaintext[64:])

print(xor(plaintext1, iv1) + xor(plaintext2, iv2))
```
- Flag: `crypto{3cb_5uck5_4v01d_17_!!!!!}`
