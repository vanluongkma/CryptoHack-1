**RSA Starter 4**
![image](https://hackmd.io/_uploads/BJ9G8gSta.png)
- Challenge này yêu cầu ta tính `d` dựa vào yếu tố đã cung cấp.
- Ta biết rằng $d= e^{-1} mod(\phi(n))$.
```Python
p = 857504083339712752489993810777
q = 1029224947942998075080348647219
e= 65537
phi= (p- 1)*(q- 1)
d= pow(e, -1, phi)
print(d)
```
![image](https://hackmd.io/_uploads/rJzMwgrFp.png)
