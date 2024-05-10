## Diffie-Hellman Starter 2
![image](https://hackmd.io/_uploads/S1jCm-mha.png)
- Chall yêu cầu ta tìm phần tử sinh nhỏ nhất trong trường $F_p$ hay đơn giản hơn là tìm g thỏa mãn: $g= g^n\ mod(p)$.
```python
def find(g, p):
  for n in range(2, p):
    if pow(g, n, p) == g:
      return False
  return True

p = 28151
for g in range(p):
  if find(g, p):
    print(g)
    break
```
- Flag: `7`
