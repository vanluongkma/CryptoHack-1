# Structure of AES
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
-   Code trên dùng để chuyển `text` từ mảng 16 byte thành mảng 2 chiều 4x4 được biểu diễn dưới dạng một danh sách các danh sách con. Mỗi danh sách con đại diện cho một hàng trong ma trận và chứa 4 giá trị số nguyên tương ứng với giá trị ASCII của các ký tự trong phần tương ứng của đầu vào `text`.  
-   Hàm `matrix2bytes(matrix)` nhận vào một ma trận 4x4 được biểu diễn dưới dạng một danh sách các danh sách con (`matrix`) làm đầu vào, và trả về một mảng 16 byte được biểu diễn dưới dạng chuỗi byte. Hàm này được thực hiện bằng cách ghép các danh sách con trong ma trận lại với nhau và chuyển đổi chúng thành một đối tượng bytes.

-   Sau đó, đoạn mã định nghĩa một ma trận 4x4 có giá trị đã được cung cấp, và sử dụng hàm `matrix2bytes(matrix)` để chuyển đổi ma trận này thành một mảng 16 byte. Kết quả được in ra màn hình.
