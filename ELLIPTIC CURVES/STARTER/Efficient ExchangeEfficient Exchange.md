## Efficient Exchange
![image](https://hackmd.io/_uploads/HkQeCcU6T.png)
 - Chall cho ta $q_x = 4726$ và $n_B = 6534$ và file [decrypt.py](https://cryptohack.org/static/challenges/decrypt_08c0fede9185868aba4a6ae21aca0148.py) để decrypt ra flag.
 - Thay x vào $Y^2 = X^3 + 497 X + 1768$ để tìm $Y^2$
 - Với $Y^2$ ta tính $Y$ dựa vào $p \equiv 3\ mod(4)$ và Symbol Legend.
![image](https://hackmd.io/_uploads/HkaiesIpT.png)

- Flag: `crypto{3ff1c1ent_k3y_3xch4ng3}`.
