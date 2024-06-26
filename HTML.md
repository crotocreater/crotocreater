# HTML là gì?
HTML viết tắt của HyperText markup language hay còn gọi là ngôn ngữ đánh dấu siêu văn bản 
HTML được sử dụng để tạo và cấu trúc các thành phần trong trang web hoặc ứng dụng, phân chia các đoạn văn, heading, titles, blockquotes… và HTML không phải là ngôn ngữ lập trình.

Một tài liệu HTML được hình thành bởi các phần tử HTML (HTML Elements) được quy định bằng các cặp thẻ (tag và attributes). Các cặp thẻ này được bao bọc bởi một dấu ngoặc ngọn (ví dụ <html>) và thường là sẽ được khai báo thành một cặp, bao gồm thẻ mở và thẻ đóng. Ví dụ, chúng ta có thể tạo một đoạn văn bằng cách đặt văn bản vào trong cặp tag mở và đóng văn bản <p> và </p> :

<p>Đây là cách bạn thêm đoạn văn trong HTML.</p>

Nhưng một số thẻ đặc biệt lại không có thẻ đóng và dữ liệu được khai báo sẽ nằm trong các thuộc tính (ví dụ như thẻ <img>).

Cha đẻ của HTML là Tim Berners-Lee, cũng là người khai sinh ra World Wide Web và chủ tịch của World Wide Web Consortium (W3C – tổ chức thiết lập ra các chuẩn trên môi trường Internet). Các thiết lập và cấu trúc HTML được vận hành và phát triển bởi World Wide Web Consortium (W3C). Bạn có thể kiểm tra tình trạng mới nhất của ngôn ngữ này bất kỳ lúc nào trên trang W3C’s website.

Tham khảo việc làm lập trình viên HTML mới nhất

HTML hoạt động ra sao?
Các website hoạt động như thế nào?

Khi bạn gõ ra 1 tên miền, trình duyệt mà bạn đang sử dụng (chẳng hạn như Chrome) sẽ kết nối tới 1 máy chủ web, bằng cách dùng 1 địa chỉ IP, vốn được thấy bằng cách phân giải tên miền đó (DNS). Máy chủ web chính là 1 máy tính được kết nối tới internet và nhận các yêu cầu tới trang web từ trình duyệt của bạn. Máy chủ sau đó sẽ gửi trả thông tin về trình duyệt của bạn, là 1 tài liệu HTML, để hiển thị trang web!

Một tập tin HTML sẽ bao gồm các phần tử HTML và được lưu lại dưới đuôi mở rộng là .html hoặc .htm. Khi một tập tin HTML được hình thành, việc xử lý nó sẽ do trình duyệt web đảm nhận. Trình duyệt sẽ đóng vai trò đọc hiểu nội dung HTML từ các thẻ bên trong và sẽ chuyển sang dạng văn bản đã được đánh dấu để đọc, nghe hoặc hiểu (do các bot máy tính hiểu).

Bạn có thể xem chúng bằng cách sử dụng bất kỳ trình duyệt web nào (như Google Chrome, Safari, hay Mozilla Firefox). Trình duyệt đọc các files HTML này và xuất bản nội dung lên internet sao cho người đọc có thể xem được nó.

Thông thường, trung bình một web chứa nhiều trang web HTML, ví dụ như: trang home, trang product, trang blog…

Cấu trúc một đoạn HTML
Mỗi trang HTML chứa một bộ các tag (cũng được gọi là elements). Mỗi thẻ sẽ có những tác dụng nhất định, giúp xây dựng nên một cấu trúc hoàn chỉnh cho Website. Bạn có thể xem như là việc xây dựng từng khối của một trang web. Nó tạo thành cấu trúc cây thư mục bao gồm section, paragraph, heading, và những khối nội dung khác.

Hầu hết các HTML elements đều có tag mở và tag đóng với cấu trúc như <tag></tag>.

Để biết bố cục HTML của một trang web như thế nào, bạn có thể xem code ví dụ của một trang HTML được cấu trúc như thế nào:

<!DOCTYPE html>

<html>

    <head>

        <title>Page Title</title>

    </head>

    <body>

 

        <h1>The Main Heading</h1>

        <h2>A catchy subheading</h2>

        <p>First paragraph</p>



    </body>

</html>
Trong đó:

<!DOCTYPE html>: khai báo kiểu dữ liệu hiển thị
<html> và </html>: cặp thẻ bắt buộc, element cấp cao nhất, có nhiệm vụ đóng gói tất cả nội dung của trang HTML
<head> và </head>: khai báo các thông tin meta của trang web như: tiêu đề trang, charset
<title> và </title>: cặp thẻ nằm bên trong thẻ <head>, dùng để khai báo tiêu đề của trang
<body> và </body>: cặp thẻ dùng để đóng gói tất cả các nội dung sẽ hiển thị trên trang
<h1></h1>, <h2></h2>: định dạng dữ liệu dạng heading. Thông thường có 6 cấp độ heading trong HTML, trải dài từ <h1> tới <h6>. Trong đó, <h1> là cấp độ heading cao nhất và <h6> là cấp độ heading thấp nhất.
<p> và </p>: cặp thẻ chứa các đoạn văn bản của trang web
Các tag thông dụng của HTML
HTML tags được sử dụng chủ yếu là 2 loại chính: block-level tags và inline tags.

Elements Block-level : đây là loại tag cấp cao nhất, sẽ sử dụng toàn không gian trang web và luôn bắt đầu dòng mới của trang web. 3 block-level tags mà tất cả các trang HTML đầu cần có đó là <html></html>, <head></head> và <body></body>.
Inline elements chỉ chiếm phần nhỏ không gian web và không bắt đầu dòng mới của trang web. Chúng thường dùng để định dạng nội dung bên trong của block level elements.
Block-Level Tags
3 block level tags của mỗi trang HTML cần có những tag như là <html>, <head>, và <body>.

Tag <html></html> là element cao nhất dùng để đóng gói mỗi trang HTML.
Tag <head></head> chứa các thông tin meta như là tiêu đề trang và charset.
Cuối cùng, <body></body> tag dùng để đóng gói tất cả nội dung sẽ hiện trên trang.
<html>

<head>

<!-- META INFORMATION -->

</head>

<body>

<!-- PAGE CONTENT -->

</body>

</html>
Inline Tags
Inline tags thường được dùng để định dạng, tạo bố cục cho nội dung bên trong của block-level tags.. Ví dụ như, tag <strong></strong> sẽ định dạng chữ in đậm, trong khi đó tag <em></em> sẽ định dạng chữ in nghiên.

Hyperlinks cũng là yếu tố element mà cần tag <a></a> và attributes href để xác định link cụ thể: <a href="https://topdev.vn/">Click me!</a>

Ảnh cũng là element inline. Bạn có thể thêm ảnh bằng cách sử dụng tag <img> mà không cần tag đóng. Nhưng bạn cũng cần sử dụng attribute src để xác định nguồn ảnh, ví dụ như:

<img src="/images/example.jpg" alt="Example image">

Nếu bạn muốn tìm hiểu thêm về tag HTML, hãy cân nhắc xem qua cheat sheet HTML

>>> Xem thêm: HTML5 khác HTML như thế nào?

Ưu và nhược điểm HTML
HTML là một ngôn ngữ đánh dấu siêu văn bản nên nó sẽ có vai trò xây dựng cấu trúc siêu văn bản trên một website, hoặc khai báo các tập tin kỹ thuật số (media) như hình ảnh, video, nhạc. Tuy nhiên, HTML có ưu và nhược điểm của riêng nó.

Ưu điểm:

Được sử dụng rộng rãi, có rất nhiều nguồn tài nguyên hỗ trợ và cộng đồng sử dụng lớn.
Học đơn giản và dễ hiểu.
Mã nguồn mở và hoàn toàn miễn phí.
Markup gọn gàng và đồng nhất.
Tiêu chuẩn thế giới được vận hành bởi World Wide Web Consortium (W3C).
Dễ dàng tích hợp với các ngôn ngữ backend như PHP, Python…
Khuyết điểm:

Được dùng chủ yếu cho web tĩnh. Đối với các tính năng động như update hay realtime thời gian thực, bạn cần sử dụng JavaScript hoặc ngôn ngữ backend bên thứ 3 như PHP.
Một số trình duyệt chậm hỗ trợ tính năng mới.
Xem ngay tin tức tuyển dụng HTML Hồ Chí Minh đãi ngộ tốt

HTML đóng vai trò gì trong website
Với những ưu và khuyết điểm trên, điều đó không có nghĩa là chỉ sử dụng HTML để tạo ra một website mà HTML chỉ đóng một vai trò hình thành trên website. Một website chuẩn sẽ được hình thành bởi:

HTML – Xây dựng cấu trúc và định dạng các siêu văn bản.
CSS – Định dạng các siêu văn bản dạng thô tạo ra từ HTML thành một bố cục website, có màu sắc, ảnh nền,….
Javascript – Tạo ra các sự kiện tương tác với hành động của người dùng (ví dụ như là chat, update nội dung, hiệu ứng slide).
PHP – Ngôn ngữ lập trình để xử lý và trao đổi dữ liệu giữa máy chủ đến trình duyệt.
MySQL – Hệ quản trị cơ sở dữ liệu truy vấn có cấu trúc.
Nếu website là một cơ thể hoàn chỉnh thì HTML chính là bộ xương của cơ thể đó. Dù website thuộc thể loại nào, giao tiếp với ngôn ngữ lập trình nào để xử lý dữ liệu thì vẫn phải cần HTML để hiển thị nội dung ra cho người dùng xem.


HTML, CSS và Javascript bổ trợ cho nhau như thế nào?
Tuy HTML được đánh giá là khung sườn cho website nhưng nó vẫn chưa đủ khả năng xây dựng một trang web chuyên nghiệp. Do đó, các lập trình viên thường chỉ sử dụng HTML để thêm các element dạng văn bản và xây dựng giao diện cấu trúc cho phần nội dung trên trang.

Với khả năng tương thích cao, HTML khi kết hợp cùng CSS và Javascript sẽ có thể giúp tăng trải nghiệm cho người dùng và thiết lập được các chức năng cao cấp khác. Cụ thể:

CSS đóng vai trò chính trong việc thiết kế, xây dựng background, màu sắc và các hiệu ứng cho trang
CSS (Cascading Style Sheets) lại là một ngôn ngữ giúp định hình phong cách cho website. Chúng ta sử dụng CSS để định dạng phần nội dung được chỉ định trong tài liệu HTML. Nói thêm, CSS được phát triển bởi W3C vào năm 1996 nhằm hỗ trợ nhiều tính năng mà HTML chưa thể làm được, ví dụ như gắn tag để định dạng trang web.

Javascript có nhiệm vụ giúp tạo ra các chức năng động như: thư viện hình ảnh, slider, pop-up…
Website có hai loại chính:

Website tĩnh (static web) – Là một website không giao tiếp với máy chủ web để gửi nhận dữ liệu mà chỉ có các dữ liệu được khai báo sẵn bằng HTML và trình duyệt đọc.
Website động (dynamic web) – Là một website sẽ giao tiếp với một máy chủ để gửi nhận dữ liệu, các dữ liệu đó sẽ gửi ra ngoài cho người dùng bằng văn bản HTML và trình duyệt sẽ hiển thị nó. Để một website có thể giao tiếp với máy chủ web thì sẽ dùng một số ngôn ngữ lập trình dạng server-side như PHP, ASP.NET, Ruby,..để thực hiện. Ví dụ như một website làm bằng WordPress là website động.
Các phần mềm để lập trình HTML
Để lập trình web hiệu quả và tiết kiệm thời gian, công sức, bạn có thể sử dụng các phần mềm lập trình HTML miễn phí và hiệu quả dưới đây:

Sublime Text
Visual Studio Code (VS Code)
Atom
Tài nguyên tham khảo HTML
HTML là thành phần cực kỳ quan trọng của một website. Các thiết lập và cấu trúc HTML được vận hành và phát triển bởi World Wide Web Consortium (W3C). Bạ