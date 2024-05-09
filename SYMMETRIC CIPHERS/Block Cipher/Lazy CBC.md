## Lazy CBC
![image](https://hackmd.io/_uploads/H1Pyqw556.png)
- Chall này là mode CBC, từ source ta biết được sever sẽ đưa flag cho ta khi mà ta gửi key đúng bằng KEY của chall.
- `cipher = AES.new(KEY, AES.MODE_CBC, KEY)` ta thấy cipher mà hóa với IV= KEY. Dựa vào điều này ta sẽ tìm KEY để gửi.
- Đây là CBC decrypt:
![image](https://hackmd.io/_uploads/H10lND99p.png)
- Theo sơ đồ ta có:
$$P_{i+1}= C_i \oplus D(C_{i+1}); C_0= IV$$$$=> P_1 \oplus P_2= C_0 \oplus D(C_1) \oplus C_1 \oplus D(C_2)$$
- Khi này nếu ta gửi tới sever 1 chuỗi với 32 bytes '0' thì ta có được:
$$P_0 \oplus P_1= D(0) \oplus C_0 \oplus D(0) \oplus D(0)= C_0= IV= KEY$$
```Python
from Crypto.Cipher import AES
from Crypto.Util.Padding import *
from Crypto.Util.number import *
from pwn import xor
import requests

def encrypt(plaintext):
	url = "https://aes.cryptohack.org/lazy_cbc/encrypt/"
	url += plaintext.hex()
	r = requests.get(url)
	js = r.json()
	return (js["ciphertext"])

def get_flag(key):
    url = "https://aes.cryptohack.org/lazy_cbc/get_flag/"
    url += key.hex() + "/"
    r = requests.get(url)
    js = r.json()
    print(bytes.fromhex(js["plaintext"]))
    
def receice(ciphertext):
    url = "https://aes.cryptohack.org/lazy_cbc/receive/"
    url += ciphertext.hex() + "/"
    r = requests.get(url)
    js = r.json()
    return bytes.fromhex(js["error"][len("Invalid plaintext: "):])
ciphertext= long_to_bytes(0)* 32
plaintext = receice(ciphertext)
get_flag(xor(plaintext[:16], plaintext[16:32]))
```
- Flag: `crypto{50m3_p30pl3_d0n7_7h1nk_IV_15_1mp0r74n7_?}`
