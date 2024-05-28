# Chinese Remainder Theorem
```Python
a = [2,3,5]
n = [5,11,17]
N = [ n[1]*n[2] , n[0]*n[2], n[0]*n[1] ]
b= len(a)
y = [pow(N[i],n[i]-2,n[i]) for i in range(b)]
c = 0
for i in range(b):
        c += a[i]*N[i]*y[i]
c %= 935
print(c)
```
Hoặc
```Python
a = [2,3,5]
n = [5,11,17]
S= int(935)
x= pow(187, -1, 5)* 2* 187
y= pow(85, -1, 11)* 3* 85
z= pow(55, -1, 17)* 5* 55
print((x+y+z)%935)
```