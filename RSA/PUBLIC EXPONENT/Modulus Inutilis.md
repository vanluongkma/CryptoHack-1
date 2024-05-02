![image](https://hackmd.io/_uploads/rJvAHLSFp.png)
- Challenge này tương đối giống với challene `Salty` chỉ khác chỉ số $e= 3$ thay vì $e= 1$. Nên ta cũng có dự đoán như bài `Salty`.
- Thật vậy ta có:
```Python
from Crypto.Util.number import *
from sage import *
ct= 243251053617903760309941844835411292373350655973075480264001352919865180151222189820473358411037759381328642957324889519192337152355302808400638052620580409813222660643570085177957
ct= pow(ct, 1/3)
flag= long_to_bytes(ct)
print(flag)
```
![image](https://hackmd.io/_uploads/BkGM5IrY6.png)
