**Inferius Prime**
![image](https://hackmd.io/_uploads/S1oWJUBFT.png)
- Challenge cho ta một bài thuần RSA bình thường với lỗ hỏng là n tương đối nhỏ có thể phân tích ra được
```Python
from Crypto.Util.number import *
p, q = 752708788837165590355094155871, 986369682585281993933185289261
n, phi = p * q, (p - 1) * (q - 1)
e = 3
d = pow(e, -1, phi)
ct = 39207274348578481322317340648475596807303160111338236677373
print(long_to_bytes(pow(ct, d, n)))
```
![image](https://hackmd.io/_uploads/B1SbeLBKp.png)
