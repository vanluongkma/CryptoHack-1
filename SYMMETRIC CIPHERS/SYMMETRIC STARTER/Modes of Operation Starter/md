## Modes of Operation Starter
![image](https://hackmd.io/_uploads/Hy26N4Yc6.png)
- Chall có liên quan đến AES mode ECB.
- Đầu tiên ta sẽ lấy output của encrypt chính là ciphertext, sau đó gửi ciphertext đi để decrypt là ta thu được flag.
```Python
import requests

BASE_URL = "http://aes.cryptohack.org/block_cipher_starter"
r = requests.get(f"{BASE_URL}/encrypt_flag")
data = r.json()
ciphertext = data["ciphertext"]
r = requests.get(f"{BASE_URL}/decrypt/{ciphertext}")
data = r.json()
plaintext = data["plaintext"]
print(bytearray.fromhex(plaintext).decode())
```
- Flag: `crypto{bl0ck_c1ph3r5_4r3_f457_!}`
