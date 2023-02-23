# ASCII
![image](https://user-images.githubusercontent.com/97203151/220949405-2304e796-343b-4eaa-8ff6-e5606a964be5.png)
ord(): chuyển 1 ký tự về mã tương ứng trên Unicode, nhận type str trả về type int.  
chr(): chuyển số về mã Unicode tương ứng, nhận type int trả về type str.  
```Python

a= [99, 114, 121, 112, 116, 111, 123, 65, 83, 67, 73, 73, 95, 112, 114, 49, 110, 116, 52, 98, 108, 51, 125]
b= str()
for i in range (0, len(a)):
    b += chr(a[i])
print(b)
    
```
Lưu ý: phải khai báo biến ngoài vòng for.
___
