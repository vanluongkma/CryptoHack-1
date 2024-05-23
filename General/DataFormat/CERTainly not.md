# CERTainly not
![image](https://github.com/Caycon/CryptoHack/assets/97203151/99c45828-e238-45be-bac4-1c1e2a0fbc82)
- Challenge cho ta một file `der` ta sẽ mở file và lấy dữ liệu trong file bằng code sau:
```Python
from Crypto.PublicKey import *
f = open('2048b-rsa-example-cert_3220bd92e30015fe4fbeb84a755e7ca5.der','rb').read()
flag = RSA.importKey(f)
print(flag.n)
```
![image](https://github.com/Caycon/CryptoHack/assets/97203151/4db16397-12be-4a2b-8c91-236ff3e548de)
