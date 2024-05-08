## Flipping Cookie
![image](https://hackmd.io/_uploads/By6VZvcqT.png)
- Chall liên quan đến mode CBC. Từ source ta biết được sever sẽ trả cho ta flag khi mà b"admin=True" nằm trong cookie.
- Cookie ban đầu là `admin=False;expiry={expires_at}`. Ta cần chuyển về `admin=True`.
- Đây là CBC decrypt:
![image](https://hackmd.io/_uploads/H10lND99p.png)
- Ta có:
$$ P= IV \oplus D(C) <=> (b'admin=False') =IV \oplus D(C)$$ $$<=> (b'admin=False') \oplus (b'admin=True') \oplus IV= D(C) \oplus (b'admin=True')$$
```Python
from Crypto.Cipher import AES
from Crypto.Util.Padding import*
from pwn import xor
import requests

def get_cookie():
	url = "https://aes.cryptohack.org/flipping_cookie/get_cookie/"
	r = requests.get(url)
	js = r.json()
	return bytes.fromhex(js["cookie"])

def check_admin(cookie, iv):
    url = "http://aes.cryptohack.org/flipping_cookie/check_admin/"
    url += cookie.hex() + "/" + iv.hex() + "/"
    r = requests.get(url)
    js = r.json()
    print(js)
cookie = get_cookie()
adminfalse= (b"admin=False;expiry=")[:16]
admintrue= pad(b"admin=True;", 16)
IV= cookie[:16]
IV= xor(xor(adminfalse, admintrue), IV)
check_admin(cookie[16:32], IV)
```
- Flag: `crypto{4u7h3n71c4710n_15_3553n714l}`
