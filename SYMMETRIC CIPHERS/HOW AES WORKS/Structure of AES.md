## Structure of AES
![image](https://hackmd.io/_uploads/ryj3HQY56.png)
- Chall cung cấp thông tin về AES cho ta, cũng như cách chuyển 1 đoạn plantext thành từng phần mỗi phần 16 bytes, rồi xếp mỗi phần đó thành ma trận 4x4.
```Python
def bytes2matrix(text):
    """ Converts a 16-byte array into a 4x4 matrix.  """
    return [list(text[i:i+4]) for i in range(0, len(text), 4)]

def matrix2bytes(matrix):
    """ Converts a 4x4 matrix into a 16-byte array.  """
    return bytes(sum(matrix, []))

matrix = [
    [99, 114, 121, 112],
    [116, 111, 123, 105],
    [110, 109, 97, 116],
    [114, 105, 120, 125],
]

print(matrix2bytes(matrix))
```
- Flag: `crypto{inmatrix}`

## Round Keys
