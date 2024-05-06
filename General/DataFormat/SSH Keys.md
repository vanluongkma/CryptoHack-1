# SSH Keys
![image](https://github.com/Caycon/CryptoHack/assets/97203151/9cefb503-4074-495c-b7a6-bc56744b41ab)
- Challenge cho ta file `pub` ta sẽ mở và lấy thông tin tương tự những bài trên.
```Python
from Crypto.PublicKey import *
f = open('bruce_rsa_6e7ecd53b443a97013397b1a1ea30e14.pub','rb').read()
flag = RSA.importKey(f)
print(flag.n)
```
- ![image](https://github.com/Caycon/CryptoHack/assets/97203151/e91df536-3506-421a-ad37-3d6f7dc44a20)
