## Diffie-Hellman Starter 1
![image](https://hackmd.io/_uploads/rJApW-Xnp.png)
- Chall yêu cầu ta tìm d= inverse(g, p).
- Ta có thể sử dụng Euclid mở rộng để tìm hoặc sử dụng hàm trong python để tìm d.
```python
g= 209
p= 991
d= pow(g,-1 , p)
print(d)
```
![image](https://hackmd.io/_uploads/H1cqXWQhT.png)
- Flag: `569`
