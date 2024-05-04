![image](https://hackmd.io/_uploads/ryqDei8Fp.png)
- Challenge ta chỉ cần gửi ngược lại `C` là có được flag.
```Python
from pwn import *
import json

r = remote("socket.cryptohack.org", 13374)
r.recvline()
r.sendline(json.dumps({'option': 'get_secret'}))
data = json.loads(r.recvline().decode())
ciphertext = data['secret'][2:]
r.sendline(json.dumps({'option': 'sign', 'msg': ciphertext}).encode())
data = json.loads(r.recvline().decode())
print(data)
r.close()
```
![image](https://hackmd.io/_uploads/SJ0ZHsUFp.png)
![image](https://hackmd.io/_uploads/HJ9CSs8Yp.png)

**Let's Decrypt**
![image](https://hackmd.io/_uploads/HJPoxiOK6.png)
- Máy chủ xác minh chữ ký không chính xác bằng cách so sánh trực tiếp thông điệp được tính toán với chữ ký được cung cấp.
- Điều này cho phép giả mạo chữ ký bằng cách thao tác với mod(N) trong phương trình xác minh.
- Ta chọn e= 1 cho dễ.
![image](https://hackmd.io/_uploads/Bkm5esOFp.png)
