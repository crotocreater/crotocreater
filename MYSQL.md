# Bài tập quản lý mượn trả sách trong thư viện. 
 
## các đối tượng cần quản lý
        - Sách 
        - Ngượn mượn
        - nhân viên
        - Thư viện 


## thông tin chi tiết về các đối tượng phải quản lý 

### sách
    - Thông tin về sách 
        - mã sách 
        - tên sách 
        - mã thể loại 
        - năm xuất bản 
        - tác giả 
        - lần tái bản 
        - mã nhà xuất bản 
        - mã thư viện


    - thể loại sách 
        - mã thể loại 
        - tên thể loại 
        - số lượng hiện có trong thư viện 


    - nhà xuất bản 
        - mã nhà xuất bản 
        - tên nhà xuất bản 
        - địa chỉ 
    

### nhân viên thư viện 
    - nhân viên
        - tên nhan viên 
        - mã nhân viê(khóa chính)
        - chức vụ 
        - thông tin liên lạc 
        - số căn cước công dân 
        - địa chỉ 
        - mã thư viện 


### người mượn 
    - thông tin về người mượn 
        - borrower_id: Khóa chính, tự tăng
        - national_id: Số căn cước công dân, duy nhất
        - name: Tên người mượn
        - contact_info: Thông tin liên lạc
        - address: Địa chỉ 

    

    - BorrowingRecords (Phiếu mượn sách)
        - record_id: Khóa chính, tự tăng
        - borrow_date: Ngày mượn sách
        - return_date: Ngày trả sách
        - employee_id: Mã nhân viên lập phiếu
        - borrower_id: Mã người mượn (Khóa ngoại tham chiếu đến Borrowers)
        - mã thư viện 

    - BorrowingDetails (Chi tiết mượn sách)
        - detail_id: Khóa chính, tự tăng
        - record_id: Mã phiếu mượn (Khóa ngoại tham chiếu đến BorrowingRecords)
        - book_id: Mã sách
        - quantity: Số lượng mượn
    
### thư viện
    - thư viện
        - mã thư viện 
        - tên thư viện 
        - địa chỉ 
        - thông tin liên lạc 
        



# Thực hiện 
Tối Ưu Hóa Thiết Kế Cơ Sở Dữ Liệu
Dưới đây là cách tối ưu hóa và thiết kế cơ sở dữ liệu quản lý mượn trả sách trong thư viện, bao gồm các bảng cần thiết và mối quan hệ giữa chúng. Chúng ta sẽ tuân thủ các nguyên tắc bình thường hóa (normalization) và tối ưu hóa để đảm bảo tính toàn vẹn và hiệu quả của dữ liệu.

Bảng Thực Thể và Quan Hệ
1. Bảng Sách (Books)
```sql
CREATE DATABASE QLTV;


-- CÁC MỐI QUAN HỆU CHỦ YẾU 
-- THƯ VIỆN - NHÂN VIÊN 
-- THƯ VIÊN - SÁCH 
-- NGƯƠI MƯỢN - SÁCH 

-- THƯ VIỆN VÀ NHÂN VIÊN 

-- THƯ VIỆN 
 CREATE TABLE THU_VIEN(
	MA VARCHAR(10) PRIMARY KEY, 
	TEN VARCHAR(50) NOT NULL,
	TVCONTRACT VARCHAR(20) NOT NULL, 
	ADRESSS VARCHAR(20) 
);

-- SÁCH 

CREATE TABLE THELOAI(
	MATHELOAI VARCHAR(20) PRIMARY KEY, 
	TENTHELOAI VARCHAR(100) NOT NULL, 
	SOLUONG INT CHECK(SOLUONG > 0)
);

CREATE TABLE NXB(
		MANXB VARCHAR(20) PRIMARY KEY, 
		TENNXB VARCHAR(100) NOT NULL, 
		DIACHI VARCHAR(100), 
		NXBCONTRACT VARCHAR(50),
);
CREATE TABLE SACH(
    MASACH VARCHAR(20) PRIMARY KEY,
    TENSACH VARCHAR(100) NOT NULL,
    MATHELOAI VARCHAR(20) REFERENCES THELOAI(MATHELOAI),
    NAMXUATBAN DATETIME CHECK (YEAR(NAMXUATBAN) BETWEEN 1500 AND 2024),
    TACGIA VARCHAR(50),
	LANTAIBAN INT CHECK(LANTAIBAN > 0 ),
	MANXB VARCHAR(20) REFERENCES NXB(MANXB),
	MATV VARCHAR(10) REFERENCES THU_VIEN(MA)
);


-- NHAN VIEN 
CREATE TABLE NHANVIEN(
    TENNV VARCHAR(50) NOT NULL,
    MANV VARCHAR(20) PRIMARY KEY,
	VITRILV VARCHAR(30),
	INFORCONTRACT VARCHAR(50) NOT NULL, 
	DIACHI VARCHAR(100) NOT NULL,
	MATV VARCHAR(10) REFERENCES THU_VIEN(MA)
	);


-- NGUOI MUON
CREATE TABLE NGUOI_MUON(
	MA INT IDENTITY(1,1) PRIMARY KEY,
    SCCCD VARCHAR(20) NOT NULL,
    TENNGUOIMUON VARCHAR(50),
	THONGTINLIENLAC VARCHAR(50) NOT NULL,
    DIACHI VARCHAR(100) NOT NULL
);


CREATE TABLE PHIEUMUON(
	MAPHIEU INT IDENTITY(1,1) PRIMARY KEY, 
	NGAYMUON DATE NOT NULL, 
	NGAYTRA DATE NOT NULL, 
	NVLAP VARCHAR(20) REFERENCES NHANVIEN(MANV),
	MANGUOIMUON INT REFERENCES NGUOI_MUON(MA),
	MATV VARCHAR(10) REFERENCES THU_VIEN(MA),
);



CREATE TABLE DSMUON(
	MAPHIEUMUON INT REFERENCES PHIEUMUON(MAPHIEU), 
	MANGUOIMUON INT REFERENCES NGUOI_MUON(MA), 
	MASACH VARCHAR(20) REFERENCES SACH(MASACH), 
	SOLUONG INT CHECK(SOLUONG > 0),
	PRIMARY KEY (MAPHIEUMUON, MANGUOIMUON)
);

```