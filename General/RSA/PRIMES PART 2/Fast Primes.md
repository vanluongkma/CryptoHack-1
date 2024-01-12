# Fast Primes
![image](https://github.com/Caycon/CryptoHack/assets/97203151/60671568-00e9-430c-8509-8830ea0753f9)
- Challenge này ta chỉ chú ý vào cách lấy dữ liệu trong file pem và cách giải mã bằng key để có được cipher.
```Python
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_OAEP
f = open('key_17a08b7040db46308f8b9a19894f9f95.pem', 'rb')
key = RSA.import_key(f.read())
p = 51894141255108267693828471848483688186015845988173648228318286999011443419469
q = 77342270837753916396402614215980760127245056504361515489809293852222206596161
phi = (p - 1) * (q - 1)
c = "249d72cd1d287b1a15a3881f2bff5788bc4bf62c789f2df44d88aae805b54c9a94b8944c0ba798f70062b66160fee312b98879f1dd5d17b33095feb3c5830d28"
c = bytes.fromhex(c)
d = pow(key.e, -1, phi)
key = RSA.construct((key.n, key.e, d))
print(key)
cipher = PKCS1_OAEP.new(key)
print(cipher)
plaintext = cipher.decrypt(c)
print(plaintext)
```
