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
Sao chép mã
CREATE TABLE Books (
    book_id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    category_id INT NOT NULL,
    publication_year INT,
    author VARCHAR(255),
    edition INT,
    publisher_id INT,
    library_branch_id INT,
    FOREIGN KEY (category_id) REFERENCES Categories(category_id),
    FOREIGN KEY (publisher_id) REFERENCES Publishers(publisher_id),
    FOREIGN KEY (library_branch_id) REFERENCES LibraryBranches(branch_id)
);```
2. Bảng Thể Loại Sách (Categories)
```sql
Sao chép mã
CREATE TABLE Categories (
    category_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    total_books INT
);```
3. Bảng Nhà Xuất Bản (Publishers)
```sql
Sao chép mã
CREATE TABLE Publishers (
    publisher_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    address VARCHAR(255)
);```
4. Bảng Nhân Viên (Employees)
```sql
Sao chép mã
CREATE TABLE Employees (
    employee_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    position VARCHAR(50),
    contact_info VARCHAR(255),
    id_card_number VARCHAR(20),
    address VARCHAR(255)
);```
5. Bảng Người Mượn (Borrowers)
```sql
Sao chép mã
CREATE TABLE Borrowers (
    borrower_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    contact_info VARCHAR(255),
    address VARCHAR(255),
    date_of_birth DATE,
    id_card_number VARCHAR(20)
);```
6. Bảng Phiếu Mượn Sách (BorrowingRecords)
```sql
Sao chép mã
CREATE TABLE BorrowingRecords (
    record_id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255),
    creation_date DATE,
    borrow_date DATE,
    return_date DATE,
    employee_id INT,
    borrower_id INT,
    FOREIGN KEY (employee_id) REFERENCES Employees(employee_id),
    FOREIGN KEY (borrower_id) REFERENCES Borrowers(borrower_id)
);```
7. Bảng Hóa Đơn Mượn (BorrowingInvoices)
```sql
Sao chép mã
CREATE TABLE BorrowingInvoices (
    invoice_id INT AUTO_INCREMENT PRIMARY KEY,
    record_id INT,
    total_books INT,
    FOREIGN KEY (record_id) REFERENCES BorrowingRecords(record_id)
);```
8. Bảng Danh Sách Mượn (BorrowingList)
```sql
Sao chép mã
CREATE TABLE BorrowingList (
    list_id INT AUTO_INCREMENT PRIMARY KEY,
    book_id INT,
    quantity INT,
    FOREIGN KEY (book_id) REFERENCES Books(book_id)
);```
9. Bảng Thư Viện (LibraryBranches)
```sql
Sao chép mã
CREATE TABLE LibraryBranches (
    branch_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    address VARCHAR(255),
    contact_info VARCHAR(255)
);```
10. Bảng Quan Hệ Thư Viện - Nhân Viên (LibraryBranchEmployees)
```sql
CREATE TABLE LibraryBranchEmployees (
    branch_id INT,
    employee_id INT,
    salary DECIMAL(10, 2),
    days_off INT,
    PRIMARY KEY (branch_id, employee_id),
    FOREIGN KEY (branch_id) REFERENCES LibraryBranches(branch_id),
    FOREIGN KEY (employee_id) REFERENCES Employees(employee_id)
);```
11. Bảng Quan Hệ Thư Viện - Sách (LibraryBranchBooks)
```sql
Sao chép mã
CREATE TABLE LibraryBranchBooks (
    branch_id INT,
    book_id INT,
    available_quantity INT,
    category_id INT,
    PRIMARY KEY (branch_id, book_id),
    FOREIGN KEY (branch_id) REFERENCES LibraryBranches(branch_id),
    FOREIGN KEY (book_id) REFERENCES Books(book_id),
    FOREIGN KEY (category_id) REFERENCES Categories(category_id)
);```
12. Bảng Quan Hệ Thư Viện - Thể Loại (LibraryBranchCategories)
```sql
Sao chép mã
CREATE TABLE LibraryBranchCategories (
    branch_id INT,
    category_id INT,
    total_quantity INT,
    PRIMARY KEY (branch_id, category_id),
    FOREIGN KEY (branch_id) REFERENCES LibraryBranches(branch_id),
    FOREIGN KEY (category_id) REFERENCES Categories(category_id)
);```
13. Bảng Quan Hệ Thư Viện - Phiếu Mượn (LibraryBranchBorrowingRecords)
```sql
Sao chép mã
CREATE TABLE LibraryBranchBorrowingRecords (
    branch_id INT,
    borrower_id INT,
    record_id INT,
    return_status BOOLEAN,
    PRIMARY KEY (branch_id, borrower_id, record_id),
    FOREIGN KEY (branch_id) REFERENCES LibraryBranches(branch_id),
    FOREIGN KEY (borrower_id) REFERENCES Borrowers(borrower_id),
    FOREIGN KEY (record_id) REFERENCES BorrowingRecords(record_id)
);```
Chỉ Mục (Indexing)
Để tăng tốc độ truy vấn, chúng ta có thể tạo thêm các chỉ mục cho các bảng thường xuyên được truy vấn.

Ví Dụ về Chỉ Mục
```sql
Sao chép mã
CREATE INDEX idx_books_category ON Books(category_id);
CREATE INDEX idx_books_publisher ON Books(publisher_id);
CREATE INDEX idx_borrowing_records_employee ON BorrowingRecords(employee_id);
CREATE INDEX idx_borrowing_records_borrower ON BorrowingRecords(borrower_id);
```