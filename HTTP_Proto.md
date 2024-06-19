# HTTP là gi
    HTTP là viết tắt của hypertext tranfer protocol hay còn gọi là giao thức 
truyền tải siêu văn bản là giao thức lớp ứng dụng trong việc truyền tải dữ liệu dạng siêu phương tiện phân tán, cộng tác. Là nên tảng trong việc trao đổi dữ liệu trong hệ thống web hiện nay 

## trước khi 

# các phương thức truyền dẫn dữ liệu trong dữ liệu trong giao thức truyền tải 


# GET
Phương thức GET là một trong những phương thức HTTP được sử dụng phổ biến nhất trong giao thức HTTP. Nó được sử dụng để yêu cầu dữ liệu từ máy chủ và không thay đổi trạng thái của tài nguyên trên máy chủ. Khi bạn thực hiện một yêu cầu GET, bạn đang yêu cầu máy chủ trả về một tài nguyên cụ thể (ví dụ: một trang web, một tài liệu JSON, một hình ảnh, v.v.).
## Cách Thức Hoạt Động của Phương Thức GET
    Yêu cầu GET: Khi bạn nhập một URL vào trình duyệt của mình hoặc nhấp vào một liên kết, trình duyệt sẽ gửi một yêu cầu GET tới máy chủ.
    Máy chủ xử lý yêu cầu: Máy chủ nhận yêu cầu GET và xác định tài nguyên cần trả về dựa trên đường dẫn URL.
    Phản hồi: Máy chủ gửi lại tài nguyên yêu cầu (ví dụ: trang HTML, dữ liệu JSON, hình ảnh) dưới dạng phản hồi HTTP.
    Trình duyệt hiển thị: Trình duyệt nhận phản hồi và hiển thị tài nguyên cho người dùng.
## Cấu Trúc của Yêu Cầu GET
    - Đường dẫn URL: Chỉ định tài nguyên cần truy cập.
    - Headers: Bao gồm thông tin về yêu cầu, như loại trình duyệt, định dạng dữ liệu mong muốn, xác thực, v.v.
    - Query Parameters: Các cặp khóa-giá trị được thêm vào URL để truyền thêm thông tin cho máy chủ (nếu cần).
## Kết Luận
Phương thức GET là một phương thức HTTP cơ bản được sử dụng để yêu cầu dữ liệu từ máy chủ mà không thay đổi trạng thái của tài nguyên trên máy chủ. Nó rất phổ biến và là một phần không thể thiếu trong việc phát triển web và giao tiếp API. Bằng cách sử dụng các thư viện như axios, bạn có thể dễ dàng thực hiện các yêu cầu GET trong ứng dụng Node.js của mình.




## Vai trò của Query Param

Query parameters được sử dụng trong các yêu cầu GET để cung cấp thêm thông tin cho máy chủ về tài nguyên được yêu cầu. Mặc dù yêu cầu GET chủ yếu để lấy tài nguyên, nhưng các tham số truy vấn (query parameters) giúp tùy chỉnh và tinh chỉnh yêu cầu đó theo nhiều cách khác nhau. Dưới đây là một số lý do chính giải thích tại sao query parameters lại đi kèm với yêu cầu GET:
###  Lọc Dữ Liệu (Filtering)
Query parameters giúp lọc dữ liệu được trả về từ máy chủ theo các tiêu chí cụ thể. Ví dụ, khi yêu cầu danh sách người dùng, bạn có thể chỉ muốn lấy những người dùng thuộc một thành phố cụ thể.
### Sắp Xếp Dữ Liệu (Sorting)
Bạn có thể yêu cầu máy chủ trả về dữ liệu đã được sắp xếp theo một thứ tự nhất định, chẳng hạn như theo tên hoặc theo ngày tạo.

### Phân Trang (Pagination)
Khi làm việc với các bộ dữ liệu lớn, bạn thường không muốn tải tất cả dữ liệu trong một lần. Thay vào đó, bạn có thể chia nhỏ dữ liệu thành các trang.


### Chỉ Định Trường Trả Về (Field Selection)
Trong một số trường hợp, bạn chỉ cần một vài trường dữ liệu cụ thể từ tài nguyên. Query parameters có thể giúp chỉ định các trường này.
## Kết Luận
Query parameters đóng vai trò quan trọng trong việc tùy chỉnh và tinh chỉnh các yêu cầu GET, giúp người dùng có thể lấy được dữ liệu chính xác và phù hợp với nhu cầu của họ. Chúng cung cấp một cách linh hoạt để tương tác với API mà không cần thay đổi cấu trúc cơ bản của URL hoặc phải tạo ra các endpoint mới cho từng trường hợp sử dụng khác nhau.

## GET với body request
Phương thức GET theo chuẩn HTTP không sử dụng phần thân (body) trong yêu cầu. Các thông tin bổ sung cần gửi đi thường được gửi dưới dạng query parameters hoặc headers. Mặc dù về lý thuyết, việc sử dụng thân yêu cầu với phương thức GET không bị cấm bởi giao thức HTTP, nhưng nhiều máy chủ, thư viện HTTP và các proxy trung gian không hỗ trợ hoặc không mong đợi thân yêu cầu trong các yêu cầu GET. Điều này có thể dẫn đến hành vi không nhất quán hoặc lỗi.

### Tại Sao GET Không Sử Dụng Body
Chuẩn HTTP: Phương thức GET được định nghĩa trong chuẩn HTTP để lấy dữ liệu và không yêu cầu thân yêu cầu. Các tham số bổ sung nên được gửi qua URL dưới dạng query parameters.
Caching: Các proxy và bộ nhớ đệm thường chỉ dựa vào URL khi lưu và tìm lại các phản hồi GET. Thân yêu cầu không được xem xét trong các hoạt động này, dẫn đến việc không thể kiểm soát được.
Trình duyệt và Thư viện HTTP: Nhiều trình duyệt và thư viện HTTP không hỗ trợ thân yêu cầu cho phương thức GET hoặc không đảm bảo hoạt động đúng đắn nếu có thân yêu cầu.
### Kết Luận
Phương thức GET theo chuẩn HTTP không sử dụng thân yêu cầu (body). Thông tin bổ sung cần gửi đi thường được truyền qua URL dưới dạng query parameters hoặc headers. Sử dụng thân yêu cầu với phương thức GET có thể dẫn đến hành vi không nhất quán hoặc lỗi, do đó, nên tránh. Khi cần gửi dữ liệu trong yêu cầu GET, hãy sử dụng query parameters như trong ví dụ trên để đảm bảo tính tương thích và hoạt động đúng đắn.

# POST
Phương thức POST là một trong những phương thức HTTP thường được sử dụng để gửi dữ liệu từ client (người dùng hoặc ứng dụng) đến server (máy chủ). Khác với phương thức GET, phương thức POST không chỉ yêu cầu tài nguyên mà còn gửi dữ liệu đến server để tạo mới hoặc cập nhật tài nguyên.

## Cách Thức Hoạt Động của Phương Thức POST
1. Yêu cầu POST: Khi người dùng gửi một yêu cầu POST, dữ liệu sẽ được gửi kèm theo yêu cầu đó, thường nằm trong phần thân (body) của yêu cầu.
2. Máy chủ nhận yêu cầu: Máy chủ nhận yêu cầu và đọc dữ liệu trong phần thân.
3. Xử lý dữ liệu: Máy chủ xử lý dữ liệu theo yêu cầu. Ví dụ, nếu yêu cầu POST để tạo một người dùng mới, máy chủ sẽ tạo một bản ghi mới trong cơ sở dữ liệu với dữ liệu nhận được.
4. Phản hồi: Máy chủ gửi lại phản hồi cho client, thông báo kết quả của yêu cầu POST. Phản hồi này có thể chứa thông tin về tài nguyên vừa được tạo hoặc trạng thái của quá trình xử lý.

## Cấu Trúc của Yêu Cầu POST
Một yêu cầu POST bao gồm các phần chính sau:

Đường dẫn URL: Chỉ định tài nguyên mà bạn muốn gửi dữ liệu đến.
Headers: Bao gồm thông tin về yêu cầu, như loại dữ liệu được gửi, xác thực, v.v.
Body: Phần thân của yêu cầu chứa dữ liệu cần gửi.

## Các Trường Hợp Sử Dụng Phương Thức POST
Phương thức POST thường được sử dụng trong các trường hợp sau:

Tạo tài nguyên mới: Ví dụ, tạo một người dùng mới, tạo một bài viết mới, v.v.
Gửi dữ liệu biểu mẫu: Khi người dùng điền và gửi một biểu mẫu trên trang web.
Tương tác với API: Khi cần gửi dữ liệu đến một API để xử lý hoặc lưu trữ.
Tải tệp lên: Khi cần tải tệp lên máy chủ.
## Kết Luận
Phương thức POST là một phần quan trọng của giao thức HTTP, được sử dụng để gửi dữ liệu từ client đến server nhằm tạo hoặc cập nhật tài nguyên. Nó đóng vai trò quan trọng trong việc phát triển các ứng dụng web hiện đại, cho phép gửi dữ liệu một cách linh hoạt và an toàn. Bằng cách sử dụng các thư viện như axios, bạn có thể dễ dàng thực hiện các yêu cầu POST trong ứng dụng Node.js của mình, hỗ trợ nhiều trường hợp sử dụng khác nhau trong việc giao tiếp với server và API.

## Query Param trong post
Phương thức POST chủ yếu sử dụng phần thân (body) của yêu cầu để gửi dữ liệu tới máy chủ. Tuy nhiên, nó vẫn có thể sử dụng query parameters nếu cần thiết. Dưới đây là cách mà POST hoạt động với và không có query parameters:

### POST Với Query Parameters
Khi bạn sử dụng query parameters cùng với phương thức POST, chúng thường được sử dụng để cung cấp các thông tin bổ sung cho yêu cầu. Query parameters sẽ được thêm vào URL, trong khi dữ liệu chính vẫn được gửi trong phần thân của yêu cầu.

### POST Không Có Query Parameters
Thông thường, khi bạn thực hiện yêu cầu POST mà không có query parameters, tất cả dữ liệu cần thiết sẽ được gửi trong phần thân của yêu cầu. Điều này đơn giản hóa URL và làm cho yêu cầu trở nên rõ ràng hơn.

### Cách Thức Hoạt Động của POST Không Có Query Parameters
Yêu cầu POST: Khi bạn gửi yêu cầu POST, dữ liệu chính sẽ được đính kèm trong phần thân (body) của yêu cầu. URL chỉ định endpoint mà bạn muốn gửi dữ liệu đến.
Máy chủ nhận yêu cầu: Máy chủ nhận yêu cầu và xử lý dữ liệu trong phần thân.
Xử lý dữ liệu: Máy chủ thực hiện các thao tác cần thiết như tạo mới hoặc cập nhật tài nguyên dựa trên dữ liệu nhận được.
Phản hồi: Máy chủ gửi lại phản hồi cho client, cho biết kết quả của quá trình xử lý.
### Tổng Kết
Phương thức POST thường được sử dụng để gửi dữ liệu từ client đến server và không yêu cầu query parameters để hoạt động. Tất cả dữ liệu cần thiết thường được gửi trong phần thân của yêu cầu. Tuy nhiên, khi cần thiết, query parameters có thể được sử dụng để cung cấp thêm thông tin cho yêu cầu. Bằng cách sử dụng các thư viện như axios, bạn có thể dễ dàng thực hiện các yêu cầu POST trong ứng dụng Node.js của mình, hỗ trợ nhiều trường hợp sử dụng khác nhau.

Phương thức POST chủ yếu được sử dụng để gửi dữ liệu từ client đến server, và phần thân (body) của yêu cầu POST chứa dữ liệu này. Dữ liệu có thể ở nhiều định dạng khác nhau, như JSON, XML, hoặc dữ liệu dạng form (x-www-form-urlencoded hoặc multipart/form-data). Dưới đây là cách hoạt động của phương thức POST và cách thực hiện yêu cầu POST với body request sử dụng Node.js và Axios.



## POST Với Body Request
Phương thức POST chủ yếu được sử dụng để gửi dữ liệu từ client đến server, và phần thân (body) của yêu cầu POST chứa dữ liệu này. Dữ liệu có thể ở nhiều định dạng khác nhau, như JSON, XML, hoặc dữ liệu dạng form (x-www-form-urlencoded hoặc multipart/form-data). Dưới đây là cách hoạt động của phương thức POST và cách thực hiện yêu cầu POST với body request sử dụng Node.js và Axios.
### Cách Thức Hoạt Động của Phương Thức POST Với Body Request
Yêu cầu POST: Khi bạn gửi yêu cầu POST, dữ liệu sẽ được đính kèm trong phần thân (body) của yêu cầu.
Máy chủ nhận yêu cầu: Máy chủ nhận yêu cầu và đọc dữ liệu trong phần thân.
Xử lý dữ liệu: Máy chủ thực hiện các thao tác cần thiết như tạo mới hoặc cập nhật tài nguyên dựa trên dữ liệu nhận được.
Phản hồi: Máy chủ gửi lại phản hồi cho client, cho biết kết quả của quá trình xử lý.

### Kết Luận
Phương thức POST được sử dụng để gửi dữ liệu từ client đến server, và phần thân (body) của yêu cầu chứa dữ liệu này. Bạn có thể gửi dữ liệu ở nhiều định dạng khác nhau như JSON, form-urlencoded, hoặc multipart/form-data. Sử dụng thư viện như axios giúp việc thực hiện các yêu cầu POST trở nên dễ dàng và hiệu quả trong ứng dụng Node.js của bạn.