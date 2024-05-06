# Extended GCD
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
