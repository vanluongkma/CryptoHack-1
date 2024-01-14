# Diffie-Hellman Starter 2
![image](https://github.com/Caycon/CryptoHack/assets/97203151/02aa117f-4474-4d08-83c1-d05ab52e7c7a)

```Python
def is_generator(k, p):
  for n in range(2, p):
    if pow(k, n, p) == k:
      return False
  return True

p = 28151
for k in range(p):
  if is_generator(k, p):
    print(k)
```
