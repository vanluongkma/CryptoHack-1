## Round Keys
![image](https://hackmd.io/_uploads/HJ4JPmY56.png)
- Chall cung cấp thông tin về AddRoundKey .
- Với chall này ta chỉ cần xor từng phần tử trong matrix với phần từ tương ứng trong matrix state.
```Python
from pwn import *

state = [
    [206, 243, 61, 34],
    [171, 11, 93, 31],
    [16, 200, 91, 108],
    [150, 3, 194, 51],
]

round_key = [
    [173, 129, 68, 82],
    [223, 100, 38, 109],
    [32, 189, 53, 8],
    [253, 48, 187, 78],
]

def add_round_key(s, k):
    x= str()
    for i in range(4):
        for j in range(4):
            s[i][j]= (xor(state[i][j], round_key[i][j]))
            a= (s[i][j]).decode()
            x+= str(a)
    return x
print(add_round_key(state, round_key))
```
- Flag: `crypto{r0undk3y}`
