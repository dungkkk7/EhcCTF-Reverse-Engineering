**Có vẻ File sample đã bị đảo ngược vị trí 2 byte liền kề cho nhau**
-Chữ ZM ở đây chăc chắn là file PE
![alt text](image.png)


**Tạo 1 script để khô phục lại file gốc** 
![alt text](image-1.png)

**Thu được** 
![alt text](image-2.png)

**Tiếp tục phân tích file này với IDA pro** 
-đây là hàm mã hóa xor như đề bài nói 
![alt text](image-3.png)

**Giải mã hàm này** 
'''
def xor_decrypt(data):
    decrypted = bytearray()
    for i, byte in enumerate(data):
        if i % 2 == 1:
            decrypted.append(byte ^ 0x16)
        else:
            decrypted.append(byte ^ 0x0C)
    return decrypted.decode('utf-8')

# Dữ liệu mã hóa được lấy từ .rdata 
encrypted_data = bytearray([
    0x49, 0x5E, 0x4F, 0x42, 0x4A, 0x6D, 0x4E, 0x77,
    0x65, 0x78, 0x6D, 0x6F, 0x7D, 0x63, 0x6D, 0x72,
    0x63, 0x78, 0x6B, 0x7F, 0x6D, 0x78, 0x7A, 0x7F,
    0x62, 0x79, 0x6F, 0x7E, 0x65, 0x4E, 0x43, 0x44,
    0x4C, 0x56, 0x4C, 0x6B
])

decrypted_text = xor_decrypt(encrypted_data)
print("Decrypted text:", decrypted_text)

'''
# Flag : EHCCTF{BainayquadongianvinochiXOR@@@}