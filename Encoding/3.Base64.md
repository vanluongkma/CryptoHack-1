# Base64  
![image](https://user-images.githubusercontent.com/97203151/220959772-f2ad790c-bd50-4c14-af63-5b32443131a5.png)
import : gọi/ nhập module.  
```Python


a= bytes.fromhex('72bca9b68fc16ac7beeb8f849dca1d8a783e8acf9679bf9269f7bf')
b= base64.b64encode(a)
print(b)


```
Lưu ý: base64.b64encode: b64 nghĩa là base64, encode nghĩa là mã hóa dữ liệu, ngược lại decode là giải mà dữ liệu.
