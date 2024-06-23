## what is rest api

REST API là gì?
REST API (Representational State Transfer Application Programming Interface) là một kiểu kiến trúc phần mềm và một phương pháp thiết kế API (Giao diện lập trình ứng dụng) dựa trên giao thức HTTP. RESTful APIs cho phép các ứng dụng giao tiếp với nhau qua mạng, thường là qua Internet, bằng cách sử dụng các phương thức HTTP chuẩn như GET, POST, PUT, DELETE, v.v.

# Các chuẩn của restfull api

## Nguyên tắc 1: Trao đổi dữ liệu 
### HTTP method 
là một trong những câu hỏi kinh điển khi tham gia phỏng vấn 
các tiêu chuẩn của http gồm các phương thức như:
    - get
    - post
    - put
    - patch
    - delete

qua các tiêu chuần này mà chúng ta tương tác giữa các máy chủ web chủ yêu thông qua các tiêu chuẩn này và  **URL**


## Nguyên tắc 2: Định dạng

### JSON
Trong các trường hợp khác dữ liệu truyền đi theo nhiều cách khác nhau có thể là **XML**, **Text**, **JSON**
nhưng trong **Rest API** thì định dạng dữ liệu truyền đi bắt buộc phải là **JOSN**

## Nguyên tắc 3: Quan hệ giũa Client - Sever 

### Mối quan hệ của Client - Sever
Hệ thống client và sever api rest đc đặt tách biệt với nhau trong hệ thống liên kết 
Chúng kết nối với nhau qua mạng để đưa ra yêu cầu và nhận phản hồi 

#### Ưu điểm của mô hình này 
có thể mở rộng quy mô một cách ko giới hạn và độc lập do client và sever chỉ giao tiếp với nhau qua internet thông qua các giao thức chứ ko có liên quan trực tiếp gì đến nhau trong quá trình xây dựng 


## Nguyên tắc 4: Stateless (Không quốc tịch ?)

Nguyên tắc này quy định khi máy khách tiến hành gửi thông tin lên máy chủ phải chứa đầy đủ thông tin để có thể nhận biết và sử lý yêu cầu trong hệ thống đó 
Sever sẽ ko lưu trữ bất kì thông tin nào của client yêu cầu lên máy chủ 


Khi máy chủ hoạt động ko chỉ có 1 client thao tác gửi yêu cầu lên máy chủ mà có đến hàng nghìn thậm chí là hàng triệu client gửi yêu cầu lên máy chủ. Do phải sử lý lượng khổng lồ đó mà máy chủ vẫn lưu trữ lại thông tin của client sẽ dẫn đến việc máy chủ phải lưu trữ một nguồn thông tin khồng lồ dẫn tới việc máy chủ hoạt động bị ảnh hưởng ko hề nhỏ do đó nguyên tắc này sinh ra nhằm đảm bảo máy chủ luôn hoạt động trong trạng thái tối ưu nhất cho việc giải   quyết yêu cầu từ phía client
Mỗi client lưu trữ thông tin sẽ đảm bảo tính an toàn cao hơn cũng như tính cá nhân cao hơn trong quá trình thực thi nó


Điều này cho phép khả năng mở rộng và triển khai máy chủ trở nên đơn giản hơn trong quá trình phát triền



## Nguyên tắc 5: Sử dụng tài nguyên 

Rest API là API hoạt động dựa trên tài nguyên do đó nó tập trung lớn vào việc sử dụng và phân phối tài nguyên máy chủ 

### Nguyên lý hoạt động
Trong tài nguyên máy chủ của chúng ta sẽ có một bộ định vị tài nguyên mà theo đó nếu có mã định vị tài nguyên chúng ta có thể truy cập vào tại nguyên tại vị trí đó và sử dụng đc nó
Thông qua **URL** or **URI** chúng ta chỉ định đến tài nguyên nào cần thiết đc sử dụng và điều này được gửi đi cùng với yêu cầu từ client đưa lên cho máy chủ 
Việc kết hớp giữa sử dụng tại nguyên và authentication API xác định API nào bạn cần bạn có thể truy cập vào đc nó hay ko và nhiều vấn đề khác nữa


# Ví dụ thành công nhất của Restfull API là internet ngày nay khi mà chúng ta hoạt động mọi thứ thông qua **URL** và phản hồi cx như gửi phản hồi thông qua hệ thống API khổng lồ đc tạo nên sẵn trong quá trình phát triển của nó 



# Start Buid Rest API 

## Method Get 