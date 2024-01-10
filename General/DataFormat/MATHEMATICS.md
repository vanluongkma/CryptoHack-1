### MATHEMATICS:
#### Greatest Common Divisor:
![image](https://hackmd.io/_uploads/SJx0URcdT.png)
- Challenge yêu cầu ta tính gcd(a,b).
```Python
def gcd(a, b):
    while b:
        a, b = b, a % b
    return a
a = 66528
b = 52920
print(gcd(a, b))
```
#### Extended GCD:
![image](https://hackmd.io/_uploads/r1tq3RqOT.png)
- Challenge này ta sẽ dựa vào thuật toán Euclid mở rộng. Mình cũng có trình bày về thuật toán này ở [đây](https://github.com/Caycon/Algorithm).
```Python
def extended_gcd(a, b):
    if b == 0:
        return a, 1, 0
    else:
        d, x, y = extended_gcd(b, a % b)
        return d, y, x - y * (a // b)
p = 26513
q = 32321
gcd_value, u, v = extended_gcd(p, q)
if u > v:
    u, v = v, u
print(v, u)
```
- `flag: -8404`
#### Modular Arithmetic 1:
![image](https://hackmd.io/_uploads/HkGCDJida.png)
- Challenge này yêu cầu ta tìm mod, tham khảo thêm về modulo tại [đây](https://github.com/Caycon/Algorithm).
```Python
print(8146798528947%17)
print(11%6)
```
`flag: 4`.
#### Modular Arithmetic 2:
![image](https://hackmd.io/_uploads/HkTtO1oup.png)
- Áp dụng kiến thức về modulo tại [đây](https://github.com/Caycon/Algorithm) để giải quyết challenge.
- Ta có `a^(p−1) ≡1(mod p)` với p là số nguyên tố. Nên kết quả cần tìm sẽ là 1.
- `flag: 1`.
#### Modular Inverting:
![image](https://hackmd.io/_uploads/S1bucJjOa.png)
- Bài toán này ta sẽ kiến thức của áp dụng thuật toán Euclid mở rộng để tìm d hay nói cách khác là tìm nghịch đảo modul của 3 mod 13.
```Python
from Crypto.Util.number import *
print(inverse(3, 13))
```
- Hoặc:
```Python
print(pow(3, -1, 13))
```
-`flag: 9`
