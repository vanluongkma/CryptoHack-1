# Modular Inverting
![image](https://hackmd.io/_uploads/S1bucJjOa.png)
- Bài toán này ta sẽ kiến thức của áp dụng thuật toán Euclid mở rộng để tìm d hay nói cách khác là tìm nghịch đảo modul của 3 mod 13.
```Python
from Crypto.Util.number import *
print(inverse(3, 13))
```
- Hoặc:
```Python
print(pow(3, -1, 13))
# flag: 9
```
