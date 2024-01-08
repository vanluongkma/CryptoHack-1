# Endless Emails
![image](https://github.com/Caycon/CryptoHack/assets/97203151/24384c33-ef95-49e0-86b3-5ed4b3a698ab)
- Chall cho ta 7 bộ số c, n, e. Với e là số nhỏ là 3. Từ e ta có thể đoán được rằng c= m^3.
- Từ chall ta định hướng rằng sử dụng Thặng dư Trung Hoa để giải quyết.
```Python
import gmpy2
from Crypto.Util.number import *
from itertools import combinations

def public(file_path):
    data= {'n': [], 'c': []}
    with open(file_path, 'r') as file:
        for line in file:
            line= line.strip()
            if not line or line.startswith('e'):
                continue
            key, value= map(str.strip, line.split('='))
            data[key].append(int(value))
    return data
def decrypt(groups, e):
    for group in combinations(zip(groups['n'], groups['c']), e):
        N= gmpy2.mpz(1)
        for n_i, _ in group:
            N= N* n_i
        m= sum(c_i* inverse(N// n_i, n_i)*(N// n_i)for n_i, c_i in group)% N
        M, trueee= gmpy2.iroot(m, e)
        if trueee:
            print(long_to_bytes(int(M)))
publickey= "output_0ef6d6343784e59e2f44f61d2d29896f.txt"
datas= public(publickey)
decrypt(datas, 3)
```
