# Ung Dung Quan Ly va Tinh Thue Thu Nhap Ca Nhan (QLThueCaNhan)

Du an mon hoc: Kiem thu phan mem (Software Testing) - Dai hoc Phenikaa

---

## 1. Gioi thieu tong quan

QLThueCaNhan la ung dung web ho tro tinh toan va quyet toan thue thu nhap ca nhan (TNCN) theo bieu thue luy tien tung phan tai Viet Nam. Du an di kem bo kich ban kiem thu tu dong (Automation Testing) su dung Selenium WebDriver, Mocha va Mochawesome.

He thong hoat dong theo kien truc Client-side, du lieu nguoi dung va bang luong duoc doc va xu ly truc tiep tu tep tin Excel (excel_data/data_tt.xlsx) thong qua thu vien SheetJS.

---

## 2. Cac chuc nang chinh

He thong phan quyen su dung theo 3 vai tro:

### Nhan vien (html/nhanvien.html)
- Xem thong tin ca nhan: Ho ten, chuc vu, phong ban, email, so dien thoai, so nguoi phu thuoc, muc luong co ban.
- Tinh thu thue: Nhap thu nhap va so nguoi phu thuoc bat ky de uoc tinh so thue phai nop.
- Tinh thue 1 thang: Tinh thue thu nhap thuc te trong thang dua tren muc luong hien tai.
- Quyet toan thue 1 nam: Tinh tong thue TNCN ca nam dua tren thu nhap chiu thue va cac khoan giam tru gia canh.

### Ke toan (html/ketoan.html)
- Bao gom toan bo chuc nang tinh thue ca nhan nhu nhan vien.
- Thiet lap muc giam tru: Dieu chinh muc giam tru cho ban than va nguoi phu thuoc.
- Xem thue nhan vien: Tra cuu va tinh toan so thue phai nop cua tung nhan su.
- Quan ly phong ban va nhan vien: Hien thi, them, sua thong tin nhan su va phong ban.

### Truong phong (html/truongphong.html)
- Bao gom cac chuc nang tinh thue ca nhan.
- Danh sach nhan vien phong ban: Theo doi danh sach, thong tin va luong cua nhan vien thuoc bo phan quan ly truc tiep.

---

## 3. Bo kich ban kiem thu tu dong (Automation Test Suite)

Cac kich ban kiem thu duoc xay dung dua tren ky thuat phan tich gia tri bien va phan vung tuong duong, thuc thi tu dong bang Selenium WebDriver:

| Tep kiem thu | Muc tieu kiem thu | Cong nghe / Trinh duyet |
| :--- | :--- | :--- |
| js/testDangNhap.js | Kiem tra dang nhap danh sach tai khoan thuc te | Mocha, Selenium (Chrome) |
| js/dangNhap.spec.js | Kich ban dang nhap xuat tu Selenium IDE | Mocha, Selenium (Chrome) |
| js/tinhThuThue.spec.js | Kiem thu tinh thu thue voi cac gia tri bien (luong am, 0, luong cao, vuot nguong nguoi phu thuoc) | Mocha, Selenium (Chrome) |
| js/giamTru.spec.js | Kiem thu nghiep vu thiet lap muc giam tru gia canh | Mocha, Selenium (Chrome) |
| js/tinhThue1Thang.spec.js | Kiem thu tinh thue 1 thang va kiem tra trang thai dang xuat | Mocha, Selenium (Firefox) |
| js/xemThueNhanVien.spec.js | Kiem thu chuc nang Ke toan xem thue nhan vien | Mocha, Selenium (Chrome) |

---

## 4. Cau truc thu muc

```plaintext
kiemthu/
├── index.html                   # Trang chu va man hinh dang nhap he thong
├── html/                        # Giao dien nguoi dung theo vai tro
│   ├── nhanvien.html            # Trang danh cho Nhan vien
│   ├── ketoan.html              # Trang danh cho Ke toan
│   └── truongphong.html         # Trang danh cho Truong phong
├── css/
│   ├── styles.css               # Dinh dang giao dien man hinh dang nhap
│   └── style.css                # Dinh dang giao dien khu vuc lam viec chinh
├── js/                          # Ma nguon JavaScript va kich ban kiem thu
│   ├── script.js                # Xu ly dang nhap va doc tep Excel
│   ├── nhanvien.js              # Nghiep vu man hinh Nhan vien
│   ├── ketoan.js                # Nghiep vu man hinh Ke toan
│   ├── truongphong.js           # Nghiep vu man hinh Truong phong
│   └── *.spec.js, test*.js      # Cac kich ban kiem thu tu dong
├── excel_data/
│   ├── data_tt.xlsx             # Tep du lieu tai khoan, luong, phong ban
│   └── id.csv                   # Danh sach ma nhan vien phuc vu test
├── package.json                 # Khai bao goi phu thuoc va thu vien kiem thu
└── README.md                    # Tai lieu huong dan du an
```

---

## 5. Huong dan cai dat va khoi chay

### 5.1. Yeu cau moi truong
- Node.js (phien ban 16.x tro len).
- Trinh duyet Google Chrome hoac Mozilla Firefox.
- Extension Live Server tren Visual Studio Code (hoac mot HTTP server bat ky).

### 5.2. Cai dat goi phu thuoc
Chay lenh sau tai thu muc goc cua du an:
```bash
npm install
```

### 5.3. Khoi chay giao dien Web
De trinh duyet co the doc tep Excel ma khong bi loi chan CORS:
1. Mo thu muc du an trong VS Code.
2. Chuot phai vao tep index.html va chon Open with Live Server (cong mac dinh: 5500).
3. Truy cap dia chi: http://127.0.0.1:5500/index.html.

---

## 6. Huong dan chay kiem thu tu dong

Luu y: Can dam bao Live Server dang hoat dong tai dia chi http://127.0.0.1:5500/ truoc khi chay test.

### Chay tung kich ban:
```bash
# Kiem thu chuc nang dang nhap
npx mocha js/testDangNhap.js

# Kiem thu tinh thu thue (kiem thu gia tri bien va phan vung tuong duong)
npx mocha js/tinhThuThue.spec.js

# Kiem thu thiet lap muc giam tru
npx mocha js/giamTru.spec.js

# Kiem thu ke toan xem thue nhan vien
npx mocha js/xemThueNhanVien.spec.js
```

### Chay va xuat bao cao HTML bang Mochawesome:
```bash
npx mocha js/tinhThuThue.spec.js --reporter mochawesome --reporter-options reportDir=mochawesome-report,reportFilename=test-report
```
Sau khi chay xong, mo tep `mochawesome-report/test-report.html` tren trinh duyet de xem ket qua chi tiet.

---

## 7. Tai khoan mau de thu nghiem thu cong

| Tai khoan | Mat khau | Vai tro | Phong ban |
| :--- | :--- | :--- | :--- |
| 20212002 | 1234 | Ke toan | Phong Ke toan |
| 20202005 | 3344 | Ke toan | Phong Ke toan |
| 20202001 | 1234 | Nhan vien | Phong Ky thuat |
| 20232004 | 1122 | Nhan vien | Phong Kinh doanh |

---

## 8. Thong tin du an
- Don vi: Dai hoc Phenikaa
- Mon hoc: Kiem thu phan mem
- Nam thuc hien: 2024
