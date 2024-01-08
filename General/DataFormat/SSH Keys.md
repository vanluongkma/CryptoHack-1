# SSH Keys
![image](https://github.com/Caycon/CryptoHack/assets/97203151/9cefb503-4074-495c-b7a6-bc56744b41ab)
- Chall cho ta file .pub ta sẽ mở file này và lấy thông tin tương tự bài `CERTainly not`.
```Python
from Crypto.PublicKey import RSA
with open('bruce_rsa_6e7ecd53b443a97013397b1a1ea30e14.pub', 'rb') as f:
    key_data = f.read()
public_key = RSA.import_key(key_data)
print(public_key.export_key().decode())
```
- Ta thu được pem sau đó giải pem đó ta thu được flag là chính là n.
- ![image](https://github.com/Caycon/CryptoHack/assets/97203151/e91df536-3506-421a-ad37-3d6f7dc44a20)
