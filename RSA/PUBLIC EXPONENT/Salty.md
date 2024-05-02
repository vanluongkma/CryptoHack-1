![image](https://hackmd.io/_uploads/HJHnNLBK6.png)
- Challenge này cho ta giá trị của $e= 1$. Điều này khiến cho $c= m$ nếu $m< n$ do cách encrypt là: $c \equiv m^e mod(n)$.
- Thật vậy, sau khi decrypt theo suy đoán ta có:
```Python
from Crypto.Util.number import *
ct= 44981230718212183604274785925793145442655465025264554046028251311164494127485
flag= long_to_bytes(ct)
print(flag)
```
![image](https://hackmd.io/_uploads/rJCnB8SKp.png)
