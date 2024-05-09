## Triple DES
![image](https://hackmd.io/_uploads/Hy7Rxdq56.png)
- Chall này là Triple DES, với chall này ta biết được điểm yếu của DES chính là các khóa yếu. Nên ta tiến hành brute force với các khóa yếu.
- Source challenge:
```Python
from Crypto.Cipher import AES
from Crypto.Util.Padding import*
from pwn import xor
import requests

def encrypt_flag(key):
	url = "https://aes.cryptohack.org/triple_des/encrypt_flag/"
	url += key
	r = requests.get(url)
	js = r.json()
	return (js["ciphertext"])

def encrypt(key, plaintext):
    url = "https://aes.cryptohack.org/triple_des/encrypt/"
    url += key + "/" + plaintext + "/"
    r = requests.get(url)
    js = r.json()
    print(bytes.fromhex(js["ciphertext"]))
a= ['01010101', '01010101','FEFEFEFE', 'FEFEFEFE','E0E0E0E0', 'F1F1F1F1','1F1F1F1F', '0E0E0E0E']
for i in a:
    for j in a:
        for k in a:
             for f in a:
                try:
                    key = i+ j+ k+ f
                    ciphertext = encrypt_flag(key)
                    flag = encrypt(key, ciphertext)
                except:
                     continue
```
- Flag: `crypto{n0t_4ll_k3ys_4r3_g00d_k3ys}`
