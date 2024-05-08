## Passwords as Keys
![image](https://hackmd.io/_uploads/HykOP4Fq6.png)
- Chall này là AES mode ECB với key là md5 của 1 key có trong [link sau](https://gist.githubusercontent.com/wchargin/8927565/raw/d9783627c731268fb2935a731a618aa8e95cf465/words).
- Ta lưu nội dung trong link về và tiến hành bruteforce.
```Python
from Crypto.Cipher import AES
import hashlib
import requests
url = 'http://aes.cryptohack.org/passwords_as_keys/'

r = requests.get(f'{url}encrypt_flag/')
first_request = r.json()
ciphertext = first_request['ciphertext']
ciphertext = bytes.fromhex(ciphertext)

with open("words.txt") as f:
    words = [w.strip() for w in f.readlines()]

for w in words:
    key = hashlib.md5(w.encode()).digest()
    cipher = AES.new(key, AES.MODE_ECB)
    decrypted = cipher.decrypt(ciphertext)
    if b'crypto' in decrypted:
      print("plaintext", decrypted)
      exit
```
- Flag: `crypto{k3y5__r__n07__p455w0rdz?}`
