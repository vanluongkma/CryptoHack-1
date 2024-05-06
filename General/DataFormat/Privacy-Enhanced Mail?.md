# Privacy-Enhanced Mail?
![image](https://github.com/Caycon/CryptoHack/assets/97203151/680fc104-1c13-4778-b900-f2ffcf2f0a07)
- Challenge cho ta file `pem` ta mở file và decode pem đó bằng tool trên `dcode.fr` va thu được d chính là flag.
- File `pem` là file lưu trữ các khóa mật mã.
- Thông tin trong file pem được mã hóa bằng `base64` nên ta hoàn toàn có thể tìm được plantext chỉ bằng cách decode base64. 
- Hoặc ta cũng có thể dùng code để lấy dữ liệu trong file pem nếu không mở được file pem.
```Python
from Crypto.PublicKey import *
f = open('privacy_enhanced_mail_1f696c053d76a78c2c531bb013a92d4a.pem','rb').read()
flag = RSA.importKey(f)
print(flag.d)      
```
![image](https://github.com/Caycon/CryptoHack/assets/97203151/2821d9e7-23c9-4f02-b876-5b427fd99003)
