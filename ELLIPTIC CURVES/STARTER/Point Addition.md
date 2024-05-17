## Point Addition
![image](https://hackmd.io/_uploads/BJvjZiIa6.png)
- Chall cho ta cách tính $P+Q$.
>Algorithm for the addition of two points: P + Q
(a) If P = O, then P + Q = Q.
(b) Otherwise, if Q = O, then P + Q = P.
(c) Otherwise, write P = (x1, y1) and Q = (x2, y2).
(d) If x1 = x2 and y1 = −y2, then P + Q = O.
(e) Otherwise:
  (e1) if P ≠ Q: λ = (y2 - y1) / (x2 - x1)
  (e2) if P = Q: λ = (3x12 + a) / 2y1
(f) x3 = λ2 − x1 − x2,     y3 = λ(x1 −x3) − y1
(g) P + Q = (x3, y3).
- Yêu cầu ta tính $S= P+P+Q+R$, với $E: Y2 = X3 + 497 X + 1768, p: 9739$, $P = (493, 5564), Q = (1539, 4742), R = (4403,5202)$.
```sage
sage: E = EllipticCurve(GF(9739),[497,1768])
sage: P = E(493, 5564)
sage: Q = E(1539, 4742)
sage: R = E(4403,5202)
sage: P+ P+ Q+ R
(4215 : 2162 : 1)
```
- Flag: `crypto{4215,2162}`
