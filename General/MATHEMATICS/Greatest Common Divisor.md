# Greatest Common Divisor
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
