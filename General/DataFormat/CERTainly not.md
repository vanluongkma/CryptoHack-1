# CERTainly not
![image](https://github.com/Caycon/CryptoHack/assets/97203151/99c45828-e238-45be-bac4-1c1e2a0fbc82)
- Chall cho ta file .der ta sẽ mở file bằng code sau:
```Python
from Crypto.PublicKey import RSA
with open('2048b-rsa-example-cert_3220bd92e30015fe4fbeb84a755e7ca5.der', 'rb') as f:
    key_data = f.read()
public_key = RSA.import_key(key_data)
print(public_key.export_key().decode())
```
- Ta thu được pem và giải mã pem ta thu được chuỗi số chính là flag.
![image](https://github.com/Caycon/CryptoHack/assets/97203151/4db16397-12be-4a2b-8c91-236ff3e548de)
