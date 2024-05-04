![image](https://hackmd.io/_uploads/H11eCoLZC.png)
- Từ source  code ta biết được sever sẽ cho ta flag khi mà  ta thỏa điều kiện của hàm sau:
```Python
 elif your_input['option'] == 'vote':
            vote = int(your_input['vote'], 16)
            verified_vote = long_to_bytes(pow(vote, ALICE_E, ALICE_N))

            # remove padding
            vote = verified_vote.split(b'\00')[-1]

            if vote == b'VOTE FOR PEDRO':
                return {"flag": FLAG}
            else:
                return {"error": "You should have voted for Pedro"}

```
- Chall yêu cầu chúng ta tìm một số nguyên x sao $x^3\ mod(n)$ tương đương với giá trị của "VOTE FOR PEDRO". Ta sẽ lợi dụng rằng n của chall rất lớn để tạo 1 số x thỏa mãn.
- Ta sẽ tìm x với code sau:
```Python
from sage.all import *
msg = bytes_to_long(b'VOTE FOR PEDRO')
modulus = 256**15
Zmod_n = Zmod(modulus)
x_candidates = Zmod_n(msg).nth_root(3, all=True)
for x in x_candidates:
    if x**3 == msg:
        print(hex(x))
        break
```
- Sau khi có x ta gửi lên sever và thu được flag.

![image](https://hackmd.io/_uploads/HydcqdwZ0.png)
