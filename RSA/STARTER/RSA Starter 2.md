**RSA Starter 2**
![image](https://hackmd.io/_uploads/ryCVQxBF6.png)
- Challenge này cho ta $(p, q, m, e)= (17, 23, 12, 65537)$ và yêu cầu ta tìm `c`. Với $c \equiv m^e mod(n)$ $(n= pq)$
```Python
(p, q, m, e)= (17, 23, 12, 65537)
print(pow(m, e, p*q))
```
![image](https://hackmd.io/_uploads/SkPTEert6.png)
