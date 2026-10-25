# BÁO CÁO BÀI TẬP LẬP TRÌNH AN TOÀN VÀ BẢO MẬT THÔNG TIN

* **Họ và tên:** Ngô Văn Nguyên
* **Mã sinh viên:** K235480106052
* **Lớp:** K59KMT
* **Công nghệ sử dụng:** C# (.NET 10 SDK), VS Code, Git, GitHub

---

## BÀI 1: MÃ HÓA ĐỐI XỨNG AES (AES-256 CBC)

### 1. Yêu cầu & Giải pháp
* Triển khai thuật toán mã hóa đối xứng AES-256 bit kết hợp xử lý luồng `CryptoStream` để mã hóa/giải mã file dung lượng lớn mà không gây tràn bộ nhớ RAM.
* Sinh khóa, xuất/nhập khóa ra file `key.txt`, thực hiện so sánh dữ liệu từng byte (Byte-by-byte comparison) giữa file nguồn và file sau khi giải mã.

### 2. Kết quả thực nghiệm

![Kết quả Bài 1 AES](images/aes_result.png)

* **Thời gian xử lý file:**
  * Thời gian Mã hóa: `0.00 giây`
  * Thời gian Giải mã: `0.03 giây`
* **Kết quả so sánh Bytes:** `GIỐNG NHAU 100% (MATCH)`

### 3. Kết luận Bài 1
* Thuật toán AES mang lại hiệu năng cao, tốc độ mã hóa và giải mã cực nhanh nhờ hỗ trợ phần cứng.
* Xử lý dữ liệu dạng Stream giúp chương trình hoạt động ổn định với các file dung lượng lớn.
* Dữ liệu sau khi giải mã hoàn toàn nguyên vẹn 100% so với file nguồn ban đầu.

---

## BÀI 2: MÃ HÓA BẤT ĐỐI XỨNG RSA & HÀM BĂM SHA256

### 1. Yêu cầu & Giải pháp
* Sinh cặp khóa RSA 2048-bit và xuất/nhập dưới dạng chuẩn PEM (`public_key.pem`, `private_key.pem`).
* Mã hóa/Giải mã dữ liệu kích thước nhỏ (dưới 190 bytes).
* Đánh giá sự chênh lệch tốc độ giữa Public Key ($e$ nhỏ) và Private Key ($d$ lớn).
* Thực nghiệm hàm băm SHA256 đánh giá hiệu ứng thác đổ (Avalanche Effect).
* **Chữ ký số ngẫu nhiên (Randomized Digital Signature):** Áp dụng chuẩn **RSA-PSS (Probabilistic Signature Scheme)** chèn giá trị Salt ngẫu nhiên vào dữ liệu băm trước khi ký.

### 2. Kết quả thực nghiệm

![Kết quả Bài 2 RSA SHA256](images/rsa_result.png)

* **Trích xuất thông số PEM:** Xuất thành công các giá trị $n, e, d$.
* **Đánh giá tốc độ Mã hóa vs Giải mã:**
  * Mã hóa bằng Public Key ($e = 65537$) thực thi rất nhanh.
  * Giải mã bằng Private Key ($d$ lớn 2048-bit) tốn nhiều thời gian tính toán hơn.
* **Hiệu ứng thác đổ SHA256:** Thay đổi $1\text{ bit}$ đầu vào làm mã băm đầu ra thay đổi hoàn toàn $50\%$ số bit một cách ngẫu nhiên.
* **Chữ ký số RSA-PSS:**
  * Cùng dữ liệu + Cùng Private Key $\rightarrow$ Sinh ra 2 chuỗi Chữ ký số hoàn toàn khác nhau.
  * Cả 2 chữ ký đều được Public Key xác minh **HỢP LỆ (VALID)** 100%.

---

## CẤU TRÚC THƯ MỤC BÀI TẬP

```text
.
├── AES_App/                # Dự án C# Mã hóa đối xứng AES
│   ├── Program.cs
│   └── key.txt
├── RSA_App/                # Dự án C# Mã hóa bất đối xứng RSA & SHA256
│   ├── Program.cs
│   ├── public_key.pem
│   └── private_key.pem
├── images/                 # Ảnh chụp màn hình kết quả thực thi
│   ├── aes_result.png
│   └── rsa_result.png
└── README.md               # Báo cáo chi tiết bài tập