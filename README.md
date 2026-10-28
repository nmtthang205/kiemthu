# ĐÁNH GIÁ CHẤT LƯỢNG PHẦN MỀM TÍNH THUẾ THU NHẬP CÁ NHÂN (QLThueCaNhan)

Báo cáo bài tập lớn môn: Đánh giá và kiểm định chất lượng phần mềm
Trường Công nghệ Thông tin Phenikaa - Đại học Phenikaa

---

## 1. Thông tin chung

- Đề tài: Đánh giá phần mềm tính thuế thu nhập cá nhân
- Giảng viên hướng dẫn: TS. Trịnh Thanh Bình
- Nhóm thực hiện: Nhóm 15 (Lớp: CSE703010-1-1-26(COUR01.LT2))
- Sinh viên thực hiện:
  Nguyễn Mạnh Thắng MSV: 23010098

---

## 2. Giới thiệu đề tài

Quản lý thuế thu nhập cá nhân (TNCN) là nghiệp vụ quan trọng và phức tạp trong doanh nghiệp, đòi hỏi tính minh bạch, chính xác và tự động hóa cao nhằm giảm thiểu sai sót do tính toán thủ công.

Hệ thống QLThueCaNhan được phát triển trên nền tảng Web theo mô hình Client-side gọn nhẹ. Hệ thống phục vụ ba đối tượng tác nhân chính trong tổ chức gồm Nhân viên, Kế toán và Trưởng phòng; đồng thời sử dụng tệp dữ liệu Excel (excel_data/data_tt.xlsx) được kết nối và xử lý thông qua thư viện SheetJS.

Mục tiêu trọng tâm của đề tài là áp dụng các phương pháp và quy trình kiểm thử phần mềm hiện đại (bao gồm kiểm thử thủ công và kiểm thử tự động với Selenium WebDriver, Mocha) để đánh giá chất lượng toàn diện của phần mềm theo tiêu chuẩn.

---

## 3. Các tác nhân và chức năng hệ thống

Hệ thống được thiết kế với 3 tác nhân chính và 9 Use Case (UC) tương ứng:

### 3.1. Tác nhân Nhân viên
- UC1.1 Xem thông tin cá nhân: Hiển thị các trường thông tin cá nhân gồm họ tên, chức vụ, phòng ban, email, số điện thoại, người phụ thuộc, mức lương cơ bản.
- UC1.2 Tính thử thuế: Cho phép nhập mức thu nhập và số người phụ thuộc bất kỳ để dự tính số tiền thuế TNCN phải nộp.
- UC1.3 Tính thuế 1 tháng: Tính toán số thuế TNCN phát sinh trong 1 tháng dựa trên biểu thuế lũy tiến từng phần và thu nhập thực tế.
- UC1.4 Quyết toán thuế 1 năm: Tổng hợp dữ liệu thu nhập, các khoản giảm trừ gia cảnh để tính quyết toán thuế TNCN cho cả năm (có hỗ trợ xuất dữ liệu).

### 3.2. Tác nhân Kế toán
- Kế thừa toàn bộ chức năng cá nhân của nhân viên (UC1.1, UC1.2, UC1.3, UC1.4).
- UC1.6 Thiết lập mức giảm trừ: Cấu hình mức giảm trừ gia cảnh cho bản thân và người phụ thuộc của từng nhân viên vào cơ sở dữ liệu.
- UC1.7 Xem thuế nhân viên: Tra cứu thông tin thuế và tính toán số thuế chi tiết của từng nhân sự trong công ty.
- UC1.8 Quản lý phòng ban: Thực hiện các thao tác Thêm phòng ban, Chỉnh sửa thông tin phòng ban, Xóa phòng ban.
- UC1.9 Quản lý nhân viên: Thực hiện các thao tác Thêm nhân viên mới, Chỉnh sửa thông tin nhân viên, Xóa nhân viên.

### 3.3. Tác nhân Trưởng phòng
- Kế thừa các chức năng tính thuế cá nhân (UC1.1, UC1.2, UC1.3, UC1.4).
- UC1.5 Hiển thị danh sách nhân viên: Xem danh sách, thông tin liên lạc và lương của tất cả nhân viên thuộc phòng ban mình phụ trách; hỗ trợ tính năng xuất danh sách ra tệp tin Excel.

---

## 4. Kế hoạch và Kỹ thuật kiểm thử

Đề tài áp dụng các kỹ thuật thiết kế ca kiểm thử hộp đen (Black-box Testing):
- Phân vùng tương đương (Equivalence Partitioning): Phân chia miền dữ liệu đầu vào thành các lớp hợp lệ và không hợp lệ (ví dụ: các khoảng thu nhập tính thuế, số người phụ thuộc hợp lệ từ 0 đến 10).
- Phân tích giá trị biên (Boundary Value Analysis): Tập trung kiểm thử tại các điểm biên của trường thu nhập (lương âm -1, mức 0, mức 1 đồng, các mốc chuyển bậc thang thuế lũy tiến, mức lương lớn) và số người phụ thuộc (0, 1, 10, 11, 100).
- Kiểm thử tự động hóa (Automation Testing): Sử dụng framework Mocha kết hợp thư viện Selenium WebDriver để kiểm tra hồi quy và kiểm tra hàng loạt tài khoản.

---

## 5. Danh mục kịch bản kiểm thử tự động

| Tên tệp kịch bản | Chức năng kiểm thử | Công nghệ / Trình duyệt |
| :--- | :--- | :--- |
| js/testDangNhap.js | Kiểm thử chức năng đăng nhập hàng loạt với bộ dữ liệu hơn 40 tài khoản | Mocha, Selenium WebDriver (Chrome) |
| js/dangNhap.spec.js | Kịch bản kiểm thử đăng nhập xuất từ công cụ Selenium IDE | Mocha, Selenium WebDriver (Chrome) |
| js/tinhThuThue.spec.js | Kiểm thử chức năng tính thử thuế với các bộ dữ liệu kiểm thử biên và phân vùng tương đương | Mocha, Selenium WebDriver (Chrome) |
| js/giamTru.spec.js | Kiểm thử chức năng thiết lập mức giảm trừ gia cảnh của Kế toán | Mocha, Selenium WebDriver (Chrome) |
| js/tinhThue1Thang.spec.js | Kiểm thử tính thuế 1 tháng và kiểm tra hiển thị nút đăng xuất trên giao diện | Mocha, Selenium WebDriver (Firefox) |
| js/xemThueNhanVien.spec.js | Kiểm thử phân quyền Kế toán khi xem thông tin thuế của nhân viên | Mocha, Selenium WebDriver (Chrome) |

---

## 6. Cấu trúc thư mục dự án

```plaintext
kiemthu/
├── index.html                           # Giao diện màn hình đăng nhập hệ thống
├── COUR01.LT3_Group11KiemThu.docx        # Báo cáo bài tập lớn hoàn chỉnh của nhóm
├── html/                                # Giao diện chức năng theo vai trò
│   ├── nhanvien.html                    # Giao diện dành cho tác nhân Nhân viên
│   ├── ketoan.html                      # Giao diện dành cho tác nhân Kế toán
│   └── truongphong.html                 # Giao diện dành cho tác nhân Trưởng phòng
├── css/                                 # Định dạng giao diện người dùng
│   ├── styles.css                       # CSS cho trang đăng nhập
│   └── style.css                        # CSS cho các trang nghiệp vụ
├── js/                                  # Mã nguồn nghiệp vụ và mã kiểm thử tự động
│   ├── script.js                        # Xử lý xác thực và kết nối tệp Excel
│   ├── nhanvien.js                      # Logic tính toán và giao diện Nhân viên
│   ├── ketoan.js                        # Logic quản lý nhân sự, phòng ban và tính thuế
│   ├── truongphong.js                   # Logic quản lý danh sách phòng ban
│   └── *.spec.js, test*.js              # Toàn bộ mã nguồn kiểm thử tự động
├── excel_data/                          # Cơ sở dữ liệu nguồn dạng bảng tính
│   ├── data_tt.xlsx                     # Tệp dữ liệu nhân viên, tài khoản, lương, phòng ban
│   └── id.csv                           # Danh sách định danh nhân viên phục vụ test
├── package.json                         # Cấu hình phụ thuộc Node.js (Selenium, Mocha)
└── README.md                            # Tài liệu mô tả và hướng dẫn dự án
```

---

## 7. Yêu cầu hệ thống và Hướng dẫn cài đặt

### 7.1. Yêu cầu hệ thống
- Phần cứng: Bộ vi xử lý Intel Core i3 trở lên; RAM tối thiểu 8 GB; ổ cứng trống tối thiểu 2 GB; độ phân giải màn hình từ 1366x768 trở lên.
- Phần mềm: Môi trường Node.js (phiên bản 16.x trở lên); trình duyệt Google Chrome hoặc Mozilla Firefox.
- Công cụ phục vụ: Visual Studio Code, extension Live Server (chạy cổng 5500).

### 7.2. Cài đặt các gói thư viện
Mở cửa sổ dòng lệnh tại thư mục gốc của dự án và chạy lệnh:
```bash
npm install
```

### 7.3. Khởi chạy ứng dụng Web
Do tính năng đọc dữ liệu từ tệp Excel thông qua JavaScript cần giao thức HTTP để tránh lỗi phân quyền tải tệp (CORS):
1. Mở dự án trong Visual Studio Code.
2. Nhấp chuột phải vào tệp index.html và chọn Open with Live Server.
3. Ứng dụng sẽ hoạt động tại địa chỉ: http://127.0.0.1:5500/index.html.

---

## 8. Hướng dẫn thực thi kịch bản kiểm thử tự động

Yêu cầu tiên quyết: Máy chủ Live Server phải đang chạy ở địa chỉ http://127.0.0.1:5500/.

### 8.1. Chạy từng kịch bản kiểm thử
```bash
# Kiểm thử chức năng đăng nhập
npx mocha js/testDangNhap.js

# Kiểm thử chức năng tính thử thuế (kiểm tra giá trị biên)
npx mocha js/tinhThuThue.spec.js

# Kiểm thử thiết lập mức giảm trừ
npx mocha js/giamTru.spec.js

# Kiểm thử xem thuế nhân viên
npx mocha js/xemThueNhanVien.spec.js
```

### 8.2. Xuất báo cáo kiểm thử tự động dạng HTML
Để xuất kết quả kiểm thử ra báo cáo trực quan thông qua công cụ Mochawesome, thực hiện lệnh:
```bash
npx mocha js/tinhThuThue.spec.js --reporter mochawesome --reporter-options reportDir=mochawesome-report,reportFilename=test-report
```
Sau khi thực thi, tệp báo cáo sẽ được tạo tại mochawesome-report/test-report.html.

---

## 9. Tài khoản mẫu để kiểm thử thủ công

| Mã tài khoản | Mật khẩu | Tác nhân / Vai trò | Bộ phận phòng ban |
| :--- | :--- | :--- | :--- |
| 20212002 | 1234 | Kế toán | Phòng Kế toán |
| 20202005 | 3344 | Kế toán | Phòng Kế toán |
| 20202001 | 1234 | Nhân viên | Phòng Kỹ thuật |
| 20232004 | 1122 | Nhân viên | Phòng Kinh doanh |

---

## 10. Đánh giá kết quả và Kết luận

Dựa trên kết quả thực hiện đề tài và nội dung báo cáo:
- Kết quả đạt được: Hệ thống đã triển khai thành công các chức năng xác thực người dùng, tính thử thuế, tính thuế một tháng và quyết toán thuế năm; giao diện trực quan, dễ thao tác; các kịch bản kiểm thử tự động bằng Selenium và Mocha đều cho kết quả đạt (Pass).
- Hạn chế: Chưa tích hợp cổng thanh toán trực tuyến cho chức năng nộp thuế thực tế; cơ chế lưu trữ dữ liệu hiện phụ thuộc vào xử lý client-side với tệp Excel.
- Hướng phát triển trong tương lai: Xây dựng hệ thống máy chủ Backend hoàn chỉnh (RESTful API, cơ sở dữ liệu quan hệ), tích hợp cổng thanh toán thuế trực tuyến, nâng cao bảo mật mã hóa mật khẩu và tối ưu hóa hiệu năng hệ thống khi xử lý lượng người dùng lớn.
