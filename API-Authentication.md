# vấn đề xác thực khi sử dụng API

khi tiến hành xây dựng hệ thống api thì vấn đề đầu tiên chúng ta phải quan tâm là cho phép những ai sử dụng và truy cập api của chúng ta khi truy cập vào rồi thì người đó được quyền sử dụng tài nguyên gì trong hệ thống api đó của chúng ta 


như các bạn đã biết thì việc tạo nên api nghĩa là chúng ta đang gửi đi tài nguyên của chúng ta dưới dạng tài nguyên có thể là jsion có thể là xml hoặc một cái gì đó như vậy 

do đó để làm việc hiệu quả và đảm về an toàn tài nguyên chúng ta có 2 loại 
# 1. **Authentication**
### Authentication trong API

**Authentication (Xác thực)** trong API là quá trình xác minh danh tính của người dùng hoặc hệ thống muốn truy cập vào API. Đây là bước đầu tiên và quan trọng để đảm bảo rằng chỉ những đối tượng được ủy quyền mới có thể truy cập các tài nguyên bảo mật của API.

### Tại Sao Authentication Quan Trọng?

1. **Bảo Mật**: Ngăn chặn truy cập trái phép vào dữ liệu nhạy cảm hoặc chức năng quan trọng.
2. **Kiểm Soát Truy Cập**: Xác định và quản lý quyền truy cập cho các người dùng hoặc ứng dụng khác nhau.
3. **Theo Dõi và Ghi Lại**: Giám sát và ghi lại hoạt động của người dùng để phát hiện và đối phó với các hành vi bất thường.

### Các Phương Thức Authentication Thông Dụng

1. **API Key**:
   - **Mô Tả**: Một chuỗi ký tự duy nhất được cấp phát cho mỗi người dùng hoặc ứng dụng.
   - **Cách Hoạt Động**: Client gửi API key cùng với mỗi yêu cầu. Server xác minh key để cho phép truy cập.
   - **Ưu Điểm**: Đơn giản, dễ triển khai.
   - **Nhược Điểm**: Ít an toàn hơn nếu không được bảo vệ đúng cách (ví dụ: nếu bị lộ key).

   ```http
   GET /api/resource
   Headers:
     Authorization: Api-Key YOUR_API_KEY
   ```

2. **Basic Authentication**:
   - **Mô Tả**: Sử dụng tên người dùng và mật khẩu được mã hóa theo base64.
   - **Cách Hoạt Động**: Client gửi chuỗi mã hóa base64 của tên người dùng và mật khẩu trong header của yêu cầu.
   - **Ưu Điểm**: Đơn giản, dễ hiểu.
   - **Nhược Điểm**: Không an toàn nếu không sử dụng HTTPS, dễ bị tấn công nếu mật khẩu yếu.

   ```http
   GET /api/resource
   Headers:
     Authorization: Basic BASE64_ENCODED_CREDENTIALS
   ```

3. **OAuth 2.0**:
   - **Mô Tả**: Một giao thức xác thực mạnh mẽ và phức tạp hơn, thường được sử dụng cho các ứng dụng web và di động.
   - **Cách Hoạt Động**: Client nhận được mã thông báo (token) sau khi xác thực và sử dụng token này để truy cập API.
   - **Ưu Điểm**: Bảo mật cao, hỗ trợ các quyền phức tạp, phù hợp cho ứng dụng lớn.
   - **Nhược Điểm**: Phức tạp hơn để triển khai.

   ```http
   GET /api/resource
   Headers:
     Authorization: Bearer YOUR_ACCESS_TOKEN
   ```

4. **Token-Based Authentication (JSON Web Tokens - JWT)**:
   - **Mô Tả**: Sử dụng mã thông báo JSON Web Token (JWT) để xác thực người dùng.
   - **Cách Hoạt Động**: Sau khi người dùng đăng nhập, server phát hành một JWT. Client gửi JWT này kèm theo mỗi yêu cầu.
   - **Ưu Điểm**: Bảo mật cao, token tự chứa thông tin người dùng và thời gian hết hạn.
   - **Nhược Điểm**: Phức tạp hơn so với API key hoặc Basic Auth.

   ```http
   GET /api/resource
   Headers:
     Authorization: Bearer YOUR_JWT_TOKEN
   ```

### Hoạt Động của Authentication trong API

1. **Client Gửi Yêu Cầu**:
   - Client gửi yêu cầu HTTP đến server API, kèm theo thông tin xác thực (như API key, token) trong header hoặc body.

2. **Server Xác Minh Thông Tin Xác Thực**:
   - Server nhận yêu cầu và kiểm tra thông tin xác thực.
   - Nếu thông tin hợp lệ, server tiếp tục xử lý yêu cầu.
   - Nếu thông tin không hợp lệ hoặc thiếu, server trả về lỗi xác thực (thường là mã trạng thái HTTP `401 Unauthorized` hoặc `403 Forbidden`).

3. **Trả Về Phản Hồi**:
   - Nếu xác thực thành công, server trả về dữ liệu hoặc kết quả yêu cầu.
   - Nếu xác thực thất bại, server trả về thông báo lỗi và mã trạng thái thích hợp.

### Ví Dụ về Authentication

#### Sử Dụng API Key

Client gửi yêu cầu kèm theo API key:

```http
GET /api/books
Headers:
  Authorization: Api-Key abc123
```

Server xác minh API key:

- Nếu key `abc123` hợp lệ, server trả về danh sách sách.
- Nếu key không hợp lệ, server trả về mã lỗi `401 Unauthorized`.

#### Sử Dụng OAuth 2.0

1. **Client Yêu Cầu Token**:
   - Client gửi yêu cầu tới server OAuth để nhận token.

   ```http
   POST /oauth/token
   Headers:
     Content-Type: application/x-www-form-urlencoded
   Body:
     grant_type=client_credentials&client_id=YOUR_CLIENT_ID&client_secret=YOUR_CLIENT_SECRET
   ```

2. **Server Phát Hành Token**:
   - Nếu thông tin xác thực hợp lệ, server phát hành token.

   ```json
   {
     "access_token": "YOUR_ACCESS_TOKEN",
     "token_type": "Bearer",
     "expires_in": 3600
   }
   ```

3. **Client Sử Dụng Token Để Truy Cập API**:
   - Client sử dụng token để truy cập các tài nguyên bảo mật.

   ```http
   GET /api/books
   Headers:
     Authorization: Bearer YOUR_ACCESS_TOKEN
   ```

### Tóm Lại

Authentication là quá trình không thể thiếu trong việc bảo vệ API khỏi truy cập trái phép. Việc lựa chọn phương thức authentication phụ thuộc vào yêu cầu bảo mật và cấu trúc của ứng dụng. Các phương thức phổ biến như API key, Basic Auth, OAuth 2.0, và JWT đều có ưu và nhược điểm riêng, nhưng đều hướng tới mục tiêu đảm bảo rằng chỉ những đối tượng được ủy quyền mới có thể truy cập và sử dụng các tài nguyên API một cách an toàn.






# làm rõ về Token-Based Authentication
Để giải thích chi tiết hơn về các thành phần và khái niệm liên quan đến JWT, hãy cùng đi sâu vào từng phần của một JSON Web Token, các thành phần của nó, và cách nó hoạt động trong quá trình xác thực.

### JSON Web Token (JWT) là gì?

JWT là một tiêu chuẩn mở (RFC 7519) để tạo token an toàn và nhỏ gọn, sử dụng để truyền thông tin giữa các bên như một đối tượng JSON. Token này thường được sử dụng để xác thực và ủy quyền trong các hệ thống phân tán, như các ứng dụng web và API.

### Cấu Trúc của JWT

JWT bao gồm ba phần chính: Header, Payload và Signature. Các phần này được mã hóa theo Base64URL và được kết hợp lại thành một chuỗi với dấu chấm (.) làm ký tự phân tách.

```
HEADER.PAYLOAD.SIGNATURE
```

#### 1. Header

**Header** của JWT chứa hai phần:

- **`alg` (algorithm)**: Thuật toán dùng để ký token, ví dụ như HMAC SHA256 (`HS256`).
- **`typ` (type)**: Loại token, thường là `JWT`.

Ví dụ Header:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

Header này sau đó được mã hóa bằng Base64URL.

#### 2. Payload

**Payload** chứa các claims, là các thông tin về thực thể (thường là người dùng) và các dữ liệu khác. Các claims có thể được chia thành ba loại:

- **Registered Claims**: Các claims chuẩn được định nghĩa bởi đặc tả JWT để cung cấp tập hợp thông tin phổ biến. Ví dụ:
  - `iss` (issuer): Người phát hành token.
  - `sub` (subject): Chủ đề của token (thường là ID của người dùng).
  - `aud` (audience): Người nhận token.
  - `exp` (expiration time): Thời gian hết hạn của token.
  - `nbf` (not before): Thời gian trước khi token chưa hợp lệ.
  - `iat` (issued at): Thời gian phát hành token.
  - `jti` (JWT ID): ID duy nhất của token, để tránh việc sử dụng lại token.

- **Public Claims**: Các claims tùy chỉnh được định nghĩa bởi người dùng. Cần phải đăng ký để tránh xung đột với các claims đã được chuẩn hóa.

- **Private Claims**: Các claims tùy chỉnh sử dụng cho các mục đích riêng tư giữa hai bên trao đổi thông tin.

Ví dụ Payload:

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true,
  "iat": 1516239022
}
```

Payload này sau đó được mã hóa bằng Base64URL.

#### 3. Signature

**Signature** được tạo để bảo vệ token khỏi bị thay đổi. Signature được tạo bằng cách mã hóa header và payload đã mã hóa với một khóa bí mật hoặc khóa riêng, sử dụng thuật toán chỉ định trong header.

Ví dụ với HMAC SHA256:

```
HMACSHA256(
  base64UrlEncode(header) + "." + base64UrlEncode(payload),
  secret
)
```

Signature giúp đảm bảo tính toàn vẹn và xác thực của token. Nếu bất kỳ phần nào của token bị thay đổi, signature sẽ không hợp lệ.

### Hoạt Động của JWT trong

quá trình xác thực

#### Quá Trình Xác Thực Sử Dụng JWT

1. **Người Dùng Đăng Nhập**:
   - Người dùng cung cấp thông tin đăng nhập (username và password) và gửi đến server.
   - Server xác thực thông tin đăng nhập và nếu hợp lệ, server tạo một JWT chứa các thông tin về người dùng (claims) và gửi lại cho client.

   Ví dụ yêu cầu đăng nhập:

   ```http
   POST /login
   Content-Type: application/json
   {
     "username": "user",
     "password": "password"
   }
   ```

   Phản hồi từ server:

   ```json
   {
     "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
   }
   ```

2. **Client Lưu Trữ Token**:
   - Client lưu trữ JWT (thường trong localStorage hoặc sessionStorage nếu là ứng dụng web) để sử dụng trong các yêu cầu tiếp theo.

3. **Client Gửi Yêu Cầu Với JWT**:
   - Trong mỗi yêu cầu tới API, client gửi JWT trong header Authorization.

   Ví dụ yêu cầu với JWT:

   ```http
   GET /api/resource
   Headers:
     Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
   ```

4. **Server Xác Thực Token**:
   - Server nhận yêu cầu từ client, lấy JWT từ header, và xác minh tính hợp lệ của token.
   - Server kiểm tra signature của token để đảm bảo rằng token chưa bị thay đổi.
   - Server kiểm tra thời gian hết hạn (`exp`) và các claims khác nếu có.

   Nếu token hợp lệ, server xử lý yêu cầu và trả về phản hồi. Nếu token không hợp lệ hoặc đã hết hạn, server trả về lỗi `401 Unauthorized`.

### Ví Dụ Chi Tiết

#### Tạo và Sử Dụng JWT trong Node.js với Express

Giả sử bạn có một ứng dụng Node.js sử dụng Express và JSON Web Token để xác thực. Dưới đây là cách tạo và sử dụng JWT trong một số tình huống cơ bản.

1. **Cài Đặt Các Gói Cần Thiết**:

   ```bash
   npm install express jsonwebtoken body-parser
   ```

2. **Tạo JWT Khi Người Dùng Đăng Nhập**:

   ```javascript
   const express = require('express');
   const jwt = require('jsonwebtoken');
   const bodyParser = require('body-parser');

   const app = express();
   app.use(bodyParser.json());

   const SECRET_KEY = 'your_secret_key';

   app.post('/login', (req, res) => {
     const { username, password } = req.body;

     // Giả sử chúng ta có một phương thức để xác thực người dùng
     if (username === 'user' && password === 'password') {
       const token = jwt.sign({ username }, SECRET_KEY, { expiresIn: '1h' });
       res.json({ token });
     } else {
       res.status(401).send('Invalid credentials');
     }
   });

   app.listen(3000, () => {
     console.log('Server is running on port 3000');
   });
   ```

3. **Sử Dụng JWT Để Truy Cập API Bảo Vệ**:

   ```javascript
   app.get('/api/resource', (req, res) => {
     const authHeader = req.headers['authorization'];
     const token = authHeader && authHeader.split(' ')[1];

     if (token == null) return res.sendStatus(401);

     jwt.verify(token, SECRET_KEY, (err, user) => {
       if (err) return res.sendStatus(403);
       req.user = user;
       res.json({ message: 'Here is your protected resource', user });
     });
   });
   ```

### Tóm Tắt

JWT là một phương pháp mạnh mẽ và linh hoạt để thực hiện xác thực và ủy quyền trong các ứng dụng web và API. Với cấu trúc bao gồm Header, Payload, và Signature, JWT cung cấp khả năng bảo mật cao bằng cách đảm bảo tính toàn vẹn và xác thực của dữ liệu. Việc sử dụng JWT giúp giảm tải công việc của server và tạo ra một phương thức xác thực hiệu quả, đặc biệt trong các hệ thống phân tán. Tuy nhiên, cần quản lý và bảo vệ token đúng cách để tránh các lỗ hổng bảo mật.






# 2. **authorization**

**Authorization (Ủy quyền)** là quá trình xác định và cấp phép quyền truy cập của người dùng hoặc thực thể đến các tài nguyên, dịch vụ hoặc dữ liệu trong một hệ thống. Nó đảm bảo rằng chỉ những người dùng có quyền hạn hợp lệ mới được phép truy cập vào các tài nguyên hoặc thực hiện các hành động nhất định.

### Sự Khác Biệt Giữa Authentication và Authorization

- **Authentication (Xác thực)**: Là quá trình xác nhận danh tính của người dùng. Nó trả lời câu hỏi "Bạn là ai?" Ví dụ: nhập tên người dùng và mật khẩu để xác thực rằng bạn là người dùng hợp lệ.

- **Authorization (Ủy quyền)**: Là quá trình kiểm tra xem người dùng đã được xác thực có quyền truy cập vào một tài nguyên cụ thể hay không. Nó trả lời câu hỏi "Bạn được phép làm gì?"

### Quy Trình Authorization

1. **Xác Thực Người Dùng**:
   - Trước tiên, người dùng cần phải được xác thực (authentication) để xác nhận danh tính. Điều này thường được thực hiện thông qua việc nhập tên người dùng và mật khẩu, hoặc sử dụng các phương thức xác thực khác như token hoặc chứng chỉ số.

2. **Kiểm Tra Quyền Hạn**:
   - Sau khi người dùng được xác thực, hệ thống sẽ kiểm tra quyền hạn của người dùng để xác định xem họ có quyền truy cập vào tài nguyên hoặc thực hiện hành động yêu cầu hay không.

3. **Cấp Quyền Hoặc Từ Chối**:
   - Dựa trên quyền hạn đã được cấu hình, hệ thống sẽ quyết định cấp phép (grant) hoặc từ chối (deny) yêu cầu truy cập của người dùng.

### Các Phương Thức Authorization

1. **Role-Based Access Control (RBAC)**:
   - Quyền hạn được gán cho các vai trò cụ thể. Người dùng sẽ được gán một hoặc nhiều vai trò và kế thừa quyền hạn của các vai trò đó.
   - Ví dụ: Một hệ thống quản lý nội dung có các vai trò như "Admin", "Editor", và "Viewer". Admin có quyền quản lý người dùng và nội dung, Editor có quyền chỉnh sửa nội dung, và Viewer chỉ có quyền xem nội dung.

2. **Attribute-Based Access Control (ABAC)**:
   - Quyền hạn được cấp dựa trên các thuộc tính của người dùng, tài nguyên, và môi trường. Các thuộc tính này có thể bao gồm vai trò, cấp bậc, phòng ban, thời gian trong ngày, v.v.
   - Ví dụ: Một tài liệu chỉ có thể được truy cập bởi người dùng thuộc phòng ban "Nhân sự" trong giờ hành chính.

3. **Access Control Lists (ACLs)**:
   - Mỗi tài nguyên có một danh sách các quyền hạn chỉ định cụ thể những ai có thể truy cập và làm gì với tài nguyên đó.
   - Ví dụ: Một file có thể có ACL cho phép người dùng "Alice" đọc và ghi, trong khi người dùng "Bob" chỉ được đọc.

### Authorization Trong API

Trong các hệ thống API, authorization thường được thực hiện thông qua việc sử dụng token. Dưới đây là một ví dụ về cách authorization hoạt động trong một API RESTful:

1. **Client Đăng Nhập và Nhận Token**:
   - Client gửi yêu cầu đăng nhập với thông tin xác thực.
   - Server xác thực thông tin và nếu hợp lệ, tạo một token (thường là JWT) chứa các thông tin về người dùng và quyền hạn, sau đó gửi lại token cho client.

2. **Client Gửi Yêu Cầu Với Token**:
   - Client lưu trữ token và gửi token này trong header của các yêu cầu API tiếp theo.

   ```http
   GET /api/resource
   Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
   ```

3. **Server Xác Thực Token và Kiểm Tra Quyền Hạn**:
   - Server nhận yêu cầu, kiểm tra tính hợp lệ của token và xác minh các thông tin trong token.
   - Dựa trên quyền hạn được lưu trữ trong token, server quyết định có cho phép truy cập tài nguyên hay không.

### Ví Dụ Thực Tế

Giả sử bạn có một hệ thống quản lý nhân sự với các vai trò và quyền hạn khác nhau. Một nhân viên có thể yêu cầu xem hồ sơ của mình, nhưng chỉ quản trị viên (Admin) mới có thể chỉnh sửa hồ sơ của nhân viên khác.

#### Cấu hình vai trò và quyền hạn:

```javascript
const roles = {
  admin: ['view_profile', 'edit_profile', 'delete_profile'],
  employee: ['view_profile']
};

const users = [
  { username: 'alice', role: 'admin' },
  { username: 'bob', role: 'employee' }
];
```

#### Kiểm tra quyền hạn trong API:

```javascript
const express = require('express');
const app = express();

app.use(express.json());

app.post('/login', (req, res) => {
  const { username } = req.body;
  const user = users.find(u => u.username === username);

  if (user) {
    // Giả sử tạo JWT chứa thông tin về người dùng và quyền hạn
    const token = jwt.sign({ username: user.username, role: user.role }, 'secret_key');
    res.json({ token });
  } else {
    res.status(401).send('Unauthorized');
  }
});

const authorize = (role, action) => (req, res, next) => {
  const token = req.headers['authorization'].split(' ')[1];
  const user = jwt.verify(token, 'secret_key');
  
  if (roles[user.role].includes(action)) {
    next();
  } else {
    res.status(403).send('Forbidden');
  }
};

app.get('/profile', authorize('employee', 'view_profile'), (req, res) => {
  res.send('Profile Information');
});

app.put('/profile', authorize('admin', 'edit_profile'), (req, res) => {
  res.send('Profile Updated');
});

app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

Trong ví dụ này:
- Người dùng sẽ đăng nhập và nhận được token.
- Yêu cầu API sẽ bao gồm token trong header Authorization.
- Middleware `authorize` sẽ kiểm tra quyền hạn của người dùng dựa trên vai trò và hành động yêu cầu, đảm bảo chỉ người dùng có quyền hạn hợp lệ mới được phép thực hiện hành động đó.




# thông tin bổ xung 

HMAC SHA256 là gì?
HMAC SHA256 là một phương thức mã hóa kết hợp giữa HMAC (Hash-based Message Authentication Code) và SHA256 (Secure Hash Algorithm 256-bit). Đây là một kỹ thuật mã hóa được sử dụng rộng rãi để đảm bảo tính toàn vẹn và xác thực của dữ liệu.

Các thành phần chính:
HMAC (Hash-based Message Authentication Code):

HMAC là một cơ chế sử dụng hàm băm để tạo ra một mã xác thực tin nhắn. Nó kết hợp một khóa bí mật với thông điệp cần mã hóa và sau đó sử dụng hàm băm để tạo ra một mã xác thực.
HMAC đảm bảo rằng chỉ những ai có khóa bí mật mới có thể tạo ra mã xác thực hợp lệ, giúp bảo vệ dữ liệu khỏi sự giả mạo.
SHA256 (Secure Hash Algorithm 256-bit):

SHA256 là một hàm băm thuộc gia đình SHA-2, tạo ra một chuỗi băm có độ dài cố định 256-bit (32-byte) từ bất kỳ dữ liệu đầu vào nào.
SHA256 được coi là một trong những hàm băm an toàn nhất hiện nay, được sử dụng rộng rãi trong các ứng dụng bảo mật như chứng chỉ số, chữ ký số, và mã hóa dữ liệu.
HMAC SHA256 hoạt động như thế nào?
HMAC SHA256 kết hợp cả HMAC và SHA256 để tạo ra một mã xác thực mạnh mẽ. Dưới đây là các bước cơ bản của quá trình này:

Chuẩn bị khóa bí mật:

Khóa bí mật được chia thành hai phần: ipad (inner padding) và opad (outer padding), mỗi phần đều có độ dài bằng băm của SHA256.
Tạo mã xác thực:

Bước 1: Kết hợp khóa bí mật với ipad, sau đó nối thêm thông điệp cần mã hóa.
Bước 2: Sử dụng SHA256 để băm kết quả của bước 1.
Bước 3: Kết hợp khóa bí mật với opad, sau đó nối thêm kết quả của bước 2.
Bước 4: Sử dụng SHA256 để băm kết quả của bước 3, tạo ra mã xác thực cuối cùng.
Ứng dụng của HMAC SHA256:
Xác thực và bảo vệ dữ liệu:

HMAC SHA256 thường được sử dụng để đảm bảo rằng dữ liệu truyền tải giữa các bên không bị thay đổi và được gửi từ nguồn tin cậy.
Tạo chữ ký số:

Nó cũng được sử dụng để tạo chữ ký số, đảm bảo tính xác thực và tính toàn vẹn của tài liệu điện tử.
Xác thực token trong API:

Trong các ứng dụng web và API, HMAC SHA256 thường được sử dụng để ký các token như JWT (JSON Web Token) để xác thực và trao quyền truy cập tài nguyên.
Ví dụ thực tế:
Dưới đây là một ví dụ về cách sử dụng HMAC SHA256 để tạo chữ ký cho một thông điệp trong Node.js:

javascript
Sao chép mã
const crypto = require('crypto');

// Khóa bí mật
const secret = 'your_secret_key';

// Thông điệp cần mã hóa
const message = 'Hello, World!';

// Tạo mã xác thực sử dụng HMAC SHA256
const hash = crypto.createHmac('sha256', secret)
                   .update(message)
                   .digest('hex');

console.log('HMAC SHA256:', hash);
Trong ví dụ này, chúng ta sử dụng module crypto của Node.js để tạo mã xác thực cho thông điệp "Hello, World!" với khóa bí mật "your_secret_key". Kết quả là một chuỗi băm được tạo ra bằng HMAC SHA256, đảm bảo rằng chỉ những ai có khóa bí mật mới có thể tạo ra hoặc xác minh mã xác thực này.

Tổng kết:
HMAC SHA256 là một phương pháp mã hóa mạnh mẽ và an toàn, kết hợp giữa HMAC và SHA256 để tạo ra mã xác thực, đảm bảo tính toàn vẹn và tính xác thực của dữ liệu. Với các ứng dụng từ bảo vệ dữ liệu truyền tải đến tạo chữ ký số và xác thực token, HMAC SHA256 đóng vai trò quan trọng trong các hệ thống bảo mật hiện đại.





### Claims trong JWT là gì?

**Claims** trong JWT (JSON Web Token) là các thông tin hoặc thuộc tính được nhúng vào trong phần Payload của token. Claims chứa các thông tin về thực thể (thường là người dùng) và các dữ liệu khác. Chúng giúp xác định và truyền đạt thông tin cần thiết về chủ thể của token và các quyền hạn liên quan.

### Phân loại Claims

Claims trong JWT được chia thành ba loại chính:

1. **Registered Claims** (Claims Đã Đăng Ký):
   - Các claims chuẩn được định nghĩa bởi đặc tả JWT để cung cấp tập hợp thông tin phổ biến.
   - Các claims này có ý nghĩa đặc biệt và được định nghĩa trước trong tiêu chuẩn JWT, ví dụ:
     - `iss` (issuer): Người phát hành token.
     - `sub` (subject): Chủ đề của token (thường là ID của người dùng).
     - `aud` (audience): Người nhận token.
     - `exp` (expiration time): Thời gian hết hạn của token.
     - `nbf` (not before): Thời gian trước khi token chưa hợp lệ.
     - `iat` (issued at): Thời gian phát hành token.
     - `jti` (JWT ID): ID duy nhất của token, để tránh việc sử dụng lại token.

   Ví dụ Payload với Registered Claims:
   ```json
   {
     "iss": "auth.example.com",
     "sub": "1234567890",
     "aud": "example.com",
     "exp": 1609459200,
     "nbf": 1609455600,
     "iat": 1609455600,
     "jti": "unique-jwt-id"
   }
   ```

2. **Public Claims** (Claims Công Khai):
   - Các claims tùy chỉnh được định nghĩa bởi người dùng, nhưng cần phải đăng ký để tránh xung đột với các claims đã được chuẩn hóa.
   - Các claims này có thể được sử dụng để thêm các thông tin cụ thể tùy thuộc vào yêu cầu của ứng dụng.

   Ví dụ Payload với Public Claims:
   ```json
   {
     "user_id": "abc123",
     "role": "admin",
     "permissions": ["read", "write", "delete"]
   }
   ```

3. **Private Claims** (Claims Riêng Tư):
   - Các claims tùy chỉnh sử dụng cho các mục đích riêng giữa hai bên trao đổi thông tin.
   - Các claims này được định nghĩa bởi các bên trao đổi và không cần đăng ký.

   Ví dụ Payload với Private Claims:
   ```json
   {
     "customClaim1": "value1",
     "customClaim2": "value2"
   }
   ```

### Ví dụ chi tiết về JWT với các Claims

Giả sử bạn có một ứng dụng web mà người dùng cần đăng nhập để truy cập các tài nguyên. Sau khi người dùng đăng nhập thành công, bạn tạo một JWT chứa các claims để xác thực người dùng.

#### Ví dụ Payload với Registered, Public và Private Claims:

```json
{
  "iss": "auth.example.com",         // Issuer
  "sub": "user123",                  // Subject (user ID)
  "aud": "example.com",              // Audience
  "exp": 1609459200,                 // Expiration time
  "iat": 1609455600,                 // Issued at
  "user_id": "user123",              // Public claim
  "role": "admin",                   // Public claim
  "customClaim1": "value1"           // Private claim
}
```

JWT này sẽ được tạo ra và gửi đến client sau khi đăng nhập. Client sẽ lưu trữ token và gửi token này trong các yêu cầu tiếp theo để truy cập các tài nguyên bảo vệ trên server.

#### Tạo JWT với claims trong Node.js

Dưới đây là cách tạo JWT với claims sử dụng Node.js và gói `jsonwebtoken`:

1. **Cài đặt gói `jsonwebtoken`**:

   ```bash
   npm install jsonwebtoken
   ```

2. **Tạo JWT với claims**:

   ```javascript
   const jwt = require('jsonwebtoken');

   const payload = {
     iss: "auth.example.com",
     sub: "user123",
     aud: "example.com",
     exp: Math.floor(Date.now() / 1000) + (60 * 60), // Token hết hạn sau 1 giờ
     iat: Math.floor(Date.now() / 1000),
     user_id: "user123",
     role: "admin",
     customClaim1: "value1"
   };

   const secret = "your_secret_key";

   const token = jwt.sign(payload, secret);

   console.log("Generated JWT:", token);
   ```

### Tổng kết

Claims là thành phần quan trọng trong JWT, chứa các thông tin về thực thể và các quyền hạn liên quan. Claims giúp xác định và truyền đạt các thông tin cần thiết giữa client và server trong quá trình xác thực và ủy quyền. Việc sử dụng claims đúng cách giúp tăng cường bảo mật và tính toàn vẹn của hệ thống.