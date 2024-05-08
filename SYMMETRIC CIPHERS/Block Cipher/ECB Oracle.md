## ECB Oracle
![image](https://hackmd.io/_uploads/HkqHvxq9p.png)
- ECB có điểm yếu là với những block plaintext giống nhau thì sẽ cho ra những ciphertext giống nhau.
- Ta sẽ sẽ làm như sau:
    - Gửi plaintext 32 bytes với: 16 bytes đầu là các số 0+ 'crypto{'  , 16 bytes sau: byte đầu chạy từ 33-> 128 các bytes còn lại là 0.
    - Sau đó ta so sánh 2 phần đầu cuối của cipher thu được, nếu nó giống nhau thì byte ta bruteforce là byte thuộc flag.
```Python
import requests
from Crypto.Cipher import AES

flag = b'crypto{'

def encrypt(plaintext):
    url = 'https://aes.cryptohack.org/ecb_oracle/encrypt/' + plaintext.hex()
    r = requests.get(url).json()
    return bytes.fromhex(r['ciphertext'])
b = ''.join([chr(i) for i in range(32, 127)])

while True:
    plaintext = b'1' * (31 - len(flag))
    target = encrypt(plaintext)[16:32]
    plaintext += flag
    found = False
    for j in b:
        plaintext_temp = plaintext[:31] + j.encode()
        bullet = encrypt(plaintext_temp)[16:32]
        if bullet == target:
            flag += j.encode()
            print(flag)
            found = True
            break
    
    if not found:
        break
```
- Flag: `crypto{p3n6u1n5_h473_3cb}`
