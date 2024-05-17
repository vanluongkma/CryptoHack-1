## Scalar Multiplication
![image](https://hackmd.io/_uploads/Hy_5Zs8pT.png)
- Chall yêu cầu ta tính $Q(x,y)= 7863 P$, với $E: Y2 = X3 + 497 X + 1768, p: 9739$; $P= (2339, 2213)$.
- Với thông tin được cung cấp từ chall là:
>Double and Add algorithm for the scalar multiplication of point P by n.
>Input: P in E(Fp) and an integer n > 0
>1. Set Q = P and R = O.
>2. Loop while n > 0.
  >3. If n ≡ 1 mod 2, set R = R + Q.
  >4. Set Q = 2 Q and n = ⌊n/2⌋.
  >5. If n > 0, continue with loop at Step 2.
>6. Return the point R, which equals nP.
```sage
sage: E = EllipticCurve(GF(9739),[497,1768])
sage: P = E(2339, 2213)
sage: 7863*P
(9467 : 2742 : 1)
```
- Flag: `crypto{9467,2742}`
