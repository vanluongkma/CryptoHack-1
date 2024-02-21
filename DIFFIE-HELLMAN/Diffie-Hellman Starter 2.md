# Diffie-Hellman Starter 2
![image](https://github.com/Caycon/CryptoHack/assets/97203151/02aa117f-4474-4d08-83c1-d05ab52e7c7a)

```Python
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
