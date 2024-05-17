## Curves and Logs
![image](https://hackmd.io/_uploads/HyzKboU6p.png)
- Chall yêu cầu ta tính x của $S(x, y)$ sau khi băm SHA1 với: $Q_A = n_AG$; $Q_B = n_BG$; shared secret : $S = n_A*Q_B = n_B * Q_A$.
```Python
sage: E = EllipticCurve(GF(9739),[497,1768])
sage: QA = E(815,3190)
sage: nB = 1829
sage: S = QA*nB
sage: S
(7929 : 707 : 1)
```
- SHA1 x= 7929 ta thu được flag.
- Flag: `crypto{80e5212754a824d3a4aed185ace4f9cac0f908bf}`
