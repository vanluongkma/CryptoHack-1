## Point Negation
![image](https://hackmd.io/_uploads/rJLhbsLp6.png)
- Chall cho ta: $E: Y^2 = X^3 + 497 X + 1768, p: 9739.$
- Yêu cầu tính tọa độ $Q(x, y)$ với $P + Q = 0$ và $P(8045, 6936).$
- $Q = -P.$
```sage
sage: E = EllipticCurve(GF(9739),[497,1768])
sage: P = E(8045,6936)
sage: -P
(8045 : 2803 : 1)
```
- Flag: `crypto{8045,2083}`## Point Negation
![image](https://hackmd.io/_uploads/rJLhbsLp6.png)
- Chall cho ta: $E: Y^2 = X^3 + 497 X + 1768, p: 9739.$
- Yêu cầu tính tọa độ $Q(x, y)$ với $P + Q = 0$ và $P(8045, 6936).$
- $Q = -P.$
```sage
sage: E = EllipticCurve(GF(9739),[497,1768])
sage: P = E(8045,6936)
sage: -P
(8045 : 2803 : 1)
```
- Flag: `crypto{8045,2083}`
