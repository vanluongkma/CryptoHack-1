
## Forbidden Fruit

![image](https://hackmd.io/_uploads/Hk0AjRj5T.png)
- Trước hết ta sẽ tìm hiểu về Galois Counter Mode (GCM).
- Tham khảo ở [đây](https://eprint.iacr.org/2016/475.pdf)  và [đây](https://www.youtube.com/watch?v=V2TlG3JbGp0&t=40s) trước nha.
- Xét $T= g(X)$, $g(X)$ là hàm GHASH.
- Ta có:
$$g(X)= A_1X^{m+n+1}+ ...+ A_mX^{n+2}+ C_1X^{n+1}+...+ C_nX^2+ LX+ S$$
- Với $A_i,\ C_i$ là các data blocks và cipher blocks, L= len(message), S là nonce value. Các block đều là 128bits trong trường hữu hạn $GF(2^{128})$
$$f_1(X)= A_{1,\ 1}X^5+ C_{1,\ 1}X^4+ C_{1,\ 2}X^3+ C_{1,\ 3}X^2+ LX+ S$$ $$f_2(X)= A_{2,\ 1}X^5+ C_{2,\ 1}X^4+ C_{2,\ 2}X^3+ C_{2,\ 3}X^2+ LX+ S$$
- Mặt khác:
$$f'_1(X)=A_{1,1}X^5+C_{1,1}X^4+C_{1,2}X^3+C_{1,3}X^2+LX+S+T_1$$ $$f'_2(X)=A_{2,1}X^5+C_{2,1}X^4+C_{2,2}X^3+C_{2,3}X^2+LX+S+T_2$$
$$=> g(X)= f'_1(X)+f'_2(X)$$ $$= (A_{1,1}+ A_{2,1})X^5+ (C_{1,1}+ C_{2,1})X^4+...+ LX +T1 +T2$$
- Áp dụng vào ta có:
$$TAG = (((((((((((H * AD0) + AD1) * H) + c0) * H) + c1) * H) + c2) * H) + L) * H) + S$$
 $$TAG = AD0*H^6 + AD1*H^5 + c0*H^4 + c1*H^3 + c2*H^2 + L*H + S$$
- Nhập 2 block ta thu được:
   $$TAG = (((((H * c_0) + c_1) * H) + L) * H + S)$$ $$<=> TAG = c_0*H^3 + c_1*H^2 + L*H + S$$
- Ta có:
       $$TAG_1 = A*H^3 + c_1*H^2 + L*H + S$$ $$TAG_2 = A*H^3 + c_2*H^2 + L*H + S$$ $$ TAG_1 - TAG_2 = (c_1-c_2)*H^2$$ $$TAG_1 - c_1*H^2 = TAG_2 - c_2*H^2$$
- X là TAG giả mạo. Ta có:
$$X = TAG_1 - c_1*H^2 == TAG_2 - c_2*H^2$$
- Mặt khác: 
   $$ forge(tag) = c*H^2 + tag_1 - c_1*H^2 $$ $$ forge(tag) = c*H^2 + X $$
 - Giờ chỉ cần gửi nonce, ciphertext, forge(tag), AD("Cryptohack") vào server và get flag.
```Python
from Crypto.Util.number import *
from Crypto.Util.number import *
from sage.all import *
import struct
import requests
import json

F.<x> = GF(2^128, x^128+x^7+x^2+x+1)

def polynomial_to_bytes(X):
    return int(f"{X.integer_representation():0128b}"[::-1], 2)

def bytes_to_polynomial(X):
    return F.fetch_int(int(f"{X:0128b}"[::-1], 2))

def ENCRYPT(plaintext):
    url = 'http://aes.cryptohack.org/forbidden_fruit/encrypt/'
    url += plaintext.hex()
    r = requests.get(url).json()
    if "error" in r:
        return None
    return  bytes.fromhex(r["nonce"]), bytes.fromhex(r["ciphertext"]), bytes.fromhex(r["tag"]), bytes.fromhex(r["associated_data"])

def DECRYPT(nonce, ciphertext, tag, associated_data):
    url = 'http://aes.cryptohack.org/forbidden_fruit/decrypt/'
    url += nonce.hex() + '/' + ciphertext.hex() + '/' + tag + '/' + associated_data.hex()
    r = requests.get(url).json()
    if "plaintext" in r:
        return bytes.fromhex(r["plaintext"])
    return None
payload = b"\x00"*16
nonce, c1, tag1, AD = ENCRYPT(payload)
payload = b"\x01"*16
_nonce, c2, tag2, _AD = ENCRYPT(payload)
c1 = bytes_to_polynomial(int.from_bytes(c1, 'big'))
c2 = bytes_to_polynomial(int.from_bytes(c2, 'big'))
tag1 = bytes_to_polynomial(int.from_bytes(tag1, 'big'))
tag2 = bytes_to_polynomial(int.from_bytes(tag2, 'big'))
print(f"{c1 = }\n")
print(f"{c2 = }\n")
print(f"{tag1 = }\n")
print(f"{tag2 = }\n")
    

H2= (tag1-tag2)/(c1-c2)
X = tag1 - c1*H2
assert X == tag2-c2*H2

ciphertext = requests.get("http://aes.cryptohack.org/forbidden_fruit/encrypt/" + (b"give me the flag").hex())
ciphertext = json.loads(ciphertext.text)
ciphertext = bytes.fromhex(ciphertext["ciphertext"])

tag = bytes_to_polynomial(int.from_bytes(ciphertext, 'big'))*H2 + X
tag = polynomial_to_bytes(tag)

print(f"{tag = }\n")
print(f"{nonce.hex() = }\n")
print(f"{AD.hex() = }\n")
print(DECRYPT(nonce, ciphertext, hex(tag)[2:], AD))
#Source: ldv
```
