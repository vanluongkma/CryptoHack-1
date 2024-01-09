# Signing Sever
![image](https://github.com/Caycon/CryptoHack/assets/97203151/f1b846ec-7934-4567-8e9c-c2c8a398299c)
- Bài này tương đối dễ ta nhận 'secret' r gửi lại là thu được flag.
- Code python:
```Python
from pwn import *
from json import *
from Crypto.Util.number import *
f= remote("socket.cryptohack.org", 13374)
f.recvline()
f.sendline(dumps({"option": "get_pubkey"}))
a = loads(f.recvline())
n = int(a["N"], 16)
print(n)
e= int(a["e"], 16)
print(e)
f.sendline(dumps({"option": "get_secret"}))
a = loads(f.recvline())
c= a["secret"]
f.sendline(dumps({"option": "sign", "msg": (c)}))
a = loads(f.recvline())
flag= long_to_bytes(int(a["signature"], 16))
print(flag)
```
