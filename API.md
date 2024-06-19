# API là gì ???
## API: là viết tắt của 'Application Programing Interface' hay còn gọi là giao diện lập trình ứng dụng
API cho phép 2 phần mềm 'nói chuyện' với nhau qua hệ thống giao thức và tập hợp các định nghĩa. Chúng ta cũng có thể coi API là các hàm build-in trong các hệ thống ngôn ngữ trả về cho chúng ta thông tin mà chúng ta cần tại một lĩnh vực liên quan đến phầm mềm nào đó.

Khi chúng ta sử dụng API cùng tương tư như việc chúng ta đứng ở phần mêm A và gọi đến phần mêm B để yêu câu: "này t đang cần 1 số thông tin như này như này, m gửi trả lại cho t". Khi phầm mềm B lúc đó sẽ quyết định có trả về thông tin cho phần mềm A hay ko nếu có phần mềm B sẽ trả về cho phần mềm A một JSON có chứa đầy đủ thông tin mà phần mềm A cần 

# API Hoạt động như thế nào 











# Xử lý data nhận được từ API

Khi API trả về kết quả, phản hồi đó không phải lúc nào cũng chỉ là một chuỗi đơn giản. Dưới đây là lý do và cách mà phản hồi từ API thường được xử lý:

Cấu Trúc Của Một Phản Hồi API
Phản hồi từ một API thường chứa nhiều thông tin hơn chỉ là dữ liệu cần thiết. Phản hồi này có thể chứa:

Headers: Thông tin meta về phản hồi (ví dụ: loại nội dung, mã trạng thái HTTP).
Status Code: Mã trạng thái HTTP (200, 404, 500, v.v.) cho biết kết quả của yêu cầu.
Data: Dữ liệu thực sự mà bạn muốn nhận được (thường là JSON).
Ví Dụ Về Một Phản Hồi API
Một phản hồi từ API có thể trông giống như sau:

```json
Sao chép mã
{
  "data": {
    "activity": "Go for a walk",
    "type": "recreational",
    "participants": 1,
    "price": 0,
    "link": "",
    "key": "3452678",
    "accessibility": 0
  },
  "status": 200,
  "statusText": "OK",
  "headers": {
    "content-type": "application/json"
  },
  "config": { ... },
  "request": { ... }
}
```
Trích Xuất Dữ Liệu Cần Thiết
Trong đoạn mã bạn cung cấp, bạn thấy dòng:

javascript
Sao chép mã
const result = response.data;
Đây là cách để trích xuất dữ liệu cần thiết từ phản hồi của API. Hãy xem tại sao:

response: Đây là đối tượng chứa toàn bộ phản hồi từ API, bao gồm nhiều thuộc tính khác nhau (headers, status, data, v.v.).
response.data: Đây là thuộc tính của đối tượng response chứa dữ liệu thực sự mà bạn muốn sử dụng. Trong trường hợp API trả về JSON, đây là phần JSON đã được phân tích cú pháp (parsed).
Tại Sao Phải Trích Xuất?
Bạn cần trích xuất dữ liệu từ response.data vì:

Phản Hồi Toàn Bộ: Phản hồi từ API bao gồm cả thông tin meta (như headers, mã trạng thái) không phải là dữ liệu chính bạn muốn xử lý.
Sử Dụng Dữ Liệu: Bạn chỉ cần phần dữ liệu thực tế để xử lý hoặc hiển thị trong ứng dụng của mình.
Ví Dụ Thực Tế
Đây là một ví dụ thực tế về cách bạn có thể gọi một API và sử dụng dữ liệu trả về:

```javascript
Sao chép mã
const axios = require('axios');

axios.get('https://bored-api.appbrewery.com/random')
  .then(response => {
    // Trích xuất dữ liệu từ phản hồi
    const result = response.data;
    // Sử dụng dữ liệu
    console.log(result);
  })
  .catch(error => {
    console.error('Failed to make request:', error.message);
  });
  ```
Trong ví dụ này:

**response**: Đối tượng chứa toàn bộ phản hồi từ API.
**response.data**: Dữ liệu thực sự từ API, ví dụ: 
``` json
{"activity": "Go for a walk", "type": "recreational", ...}.
```
Kết Luận
Phản hồi từ API thường chứa nhiều thông tin hơn là chỉ dữ liệu cần thiết. Việc trích xuất response.data giúp bạn lấy đúng phần dữ liệu mà bạn cần để sử dụng trong ứng dụng của mình. Điều này giúp đơn giản hóa quá trình xử lý và hiển thị dữ liệu.










# await và hàm bất đồng bộ 

Khi bạn sử dụng từ khóa `await` trong JavaScript, đặc biệt là trong các hàm bất đồng bộ (asynchronous functions), nó cho phép bạn "đợi" cho một lời hứa (promise) được giải quyết (resolve) hoặc bị từ chối (reject) trước khi tiếp tục thực thi mã. Điều này giúp viết mã bất đồng bộ dễ đọc hơn và tránh phải sử dụng nhiều callback hoặc `.then()`.
### Điều Gì Thực Sự Xảy Ra Khi Sử Dụng `await`

1. **Đợi Cho Promise Được Giải Quyết**:
   - `await` được sử dụng trước một promise và làm cho hàm bao bọc nó (một hàm đánh dấu là `async`) tạm dừng cho đến khi promise đó được giải quyết.
   - Nếu promise được giải quyết thành công (resolve), `await` sẽ trả về giá trị giải quyết.
   - Nếu promise bị từ chối (reject), `await` sẽ ném ra lỗi đó, điều này có thể được bắt (catch) trong khối `try-catch`.

2. **Không Chặn (Non-Blocking)**:
   - Mặc dù `await` dường như làm cho mã tạm dừng, nhưng nó không chặn toàn bộ luồng thực thi của chương trình. Các phần khác của chương trình vẫn tiếp tục chạy.
   - JavaScript vẫn xử lý các sự kiện và callback khác trong khi chờ đợi promise được giải quyết.

### Ví Dụ

Giả sử bạn có một hàm bất đồng bộ gọi một API và trả về kết quả:

```javascript
async function fetchData() {
  try {
    const response = await axios.get('https://api.example.com/data');
    console.log(response.data);
  } catch (error) {
    console.error('Error fetching data:', error);
  }
}

fetchData();
```

Trong ví dụ này:

1. **Khi Hàm `fetchData` Chạy**:
   - Hàm `axios.get('https://api.example.com/data')` trả về một promise.

2. **`await` Tạm Dừng Hàm `fetchData`**:
   - `await` tạm dừng việc thực thi của hàm `fetchData` cho đến khi promise được giải quyết.
   - Trong khi đó, các phần khác của chương trình vẫn tiếp tục chạy bình thường.

3. **Nếu Promise Được Giải Quyết Thành Công**:
   - `response` sẽ chứa kết quả từ API.
   - `console.log(response.data)` in ra dữ liệu từ API.

4. **Nếu Promise Bị Từ Chối**:
   - Lỗi sẽ được bắt trong khối `catch`, và `console.error('Error fetching data:', error)` sẽ in ra thông báo lỗi.

### Mô Tả Bằng Biểu Đồ:

```text
async function fetchData() {
  try {
    |-------------------------------|       |----------------------|
    | Call axios.get                |       | Wait for promise     |
    |-------------------------------|       |----------------------|
               ↓                                           ↓
    |-------------------------------|       |----------------------|
    | Await response                |       | Other code runs      |
    |-------------------------------|       |----------------------|
               ↓                                           ↓
    |-------------------------------|       |----------------------|
    | Promise resolved/rejected     |       | Continue execution   |
    |-------------------------------|       |----------------------|
               ↓                                           ↓
    |-------------------------------|       |----------------------|
    | Handle response or error      |       | End of function      |
    |-------------------------------|       |----------------------|
  } catch (error) {
    // Handle error
  }
}
```

### Tổng Kết

- `await` tạm dừng việc thực thi hàm cho đến khi promise được giải quyết.
- Nó giúp viết mã bất đồng bộ dễ đọc hơn và tránh sử dụng callback hoặc `.then()`.
- Trong khi `await` đợi, các phần khác của chương trình vẫn tiếp tục chạy, không bị chặn. 

Điều này giúp quản lý mã bất đồng bộ một cách hiệu quả và dễ dàng hơn trong các ứng dụng JavaScript.





# Axios libary
### Axios trong Express.js

**Axios** là một thư viện HTTP client dựa trên promise cho Node.js và trình duyệt. Nó giúp bạn thực hiện các yêu cầu HTTP (như GET, POST, PUT, DELETE) một cách dễ dàng. Khi kết hợp với **Express.js**, Axios có thể được sử dụng để thực hiện các yêu cầu HTTP tới các dịch vụ bên ngoài hoặc các API khác từ một ứng dụng Express.

### Các Thành Phần Chính của Axios

1. **Cấu Hình Yêu Cầu (Request Configuration)**:
   - `url`: Địa chỉ URL của tài nguyên bạn muốn truy cập.
   - `method`: Phương thức HTTP (GET, POST, PUT, DELETE, etc).
   - `headers`: Các headers của yêu cầu HTTP.
   - `params`: Các query parameters được thêm vào URL.
   - `data`: Payload cho các yêu cầu POST, PUT, DELETE.

2. **Phương Thức Yêu Cầu (Request Methods)**:
   - `axios.get(url, config)`
   - `axios.post(url, data, config)`
   - `axios.put(url, data, config)`
   - `axios.delete(url, config)`

3. **Xử Lý Phản Hồi (Response Handling)**:
   - `then()`: Xử lý khi yêu cầu thành công.
   - `catch()`: Xử lý khi yêu cầu thất bại.
   - `finally()`: Thực hiện tác vụ bất kể yêu cầu thành công hay thất bại.

### Cách Sử Dụng Axios với Express.js

#### Bước 1: Cài Đặt Axios

Trước tiên, bạn cần cài đặt `axios` và `express` nếu chưa có.

```bash
npm install axios express
```

#### Bước 2: Tạo Ứng Dụng Express.js

Tạo một tệp `app.js` với nội dung sau:

```javascript
const express = require('express');
const axios = require('axios');
const app = express();

// Endpoint GET để thực hiện một yêu cầu HTTP tới một API bên ngoài
app.get('/get-data', async (req, res) => {
  try {
    const response = await axios.get('https://api.example.com/data');
    res.json(response.data);
  } catch (error) {
    console.error('Error fetching data:', error);
    res.status(500).json({ error: 'Failed to fetch data' });
  }
});

// Endpoint POST để gửi dữ liệu tới một API bên ngoài
app.post('/post-data', async (req, res) => {
  try {
    const payload = { key: 'value' }; // Payload cho yêu cầu POST
    const response = await axios.post('https://api.example.com/data', payload);
    res.json(response.data);
  } catch (error) {
    console.error('Error posting data:', error);
    res.status(500).json({ error: 'Failed to post data' });
  }
});

// Khởi động máy chủ Express
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

#### Giải Thích Mã

1. **Khởi Tạo Express và Axios**:
   - Khai báo và khởi tạo Express.js và Axios.

2. **Endpoint GET**:
   - `app.get('/get-data', async (req, res) => { ... })`: Tạo một endpoint GET tại `/get-data`.
   - `axios.get('https://api.example.com/data')`: Thực hiện một yêu cầu GET tới một API bên ngoài.
   - `res.json(response.data)`: Gửi dữ liệu nhận được từ API bên ngoài trở lại client.

3. **Endpoint POST**:
   - `app.post('/post-data', async (req, res) => { ... })`: Tạo một endpoint POST tại `/post-data`.
   - `axios.post('https://api.example.com/data', payload)`: Thực hiện một yêu cầu POST tới một API bên ngoài với payload.
   - `res.json(response.data)`: Gửi phản hồi nhận được từ API bên ngoài trở lại client.

4. **Khởi Động Máy Chủ**:
   - `app.listen(PORT, () => { ... })`: Khởi động máy chủ Express tại cổng được chỉ định (mặc định là 3000).

### Tổng Kết

- **Axios**: Thư viện HTTP client dựa trên promise giúp thực hiện các yêu cầu HTTP một cách dễ dàng.
- **Express.js**: Một framework mạnh mẽ để xây dựng các ứng dụng web và API với Node.js.
- **Kết Hợp Axios và Express.js**: Sử dụng Axios để thực hiện các yêu cầu HTTP tới các dịch vụ bên ngoài hoặc API khác từ một ứng dụng Express, giúp xử lý dữ liệu và phản hồi lại client một cách hiệu quả.

Bạn có thể sử dụng cấu trúc và phương pháp tương tự để thực hiện các yêu cầu HTTP phức tạp hơn hoặc kết hợp với các dịch vụ bên ngoài khác.




# Hàm Bất Đồng Bộ (Asynchronous Function) trong JavaScript

Hàm bất đồng bộ (asynchronous function) trong JavaScript là một hàm cho phép bạn thực hiện các tác vụ không đồng bộ một cách dễ dàng và trực quan bằng cách sử dụng từ khóa `async` và `await`. Các hàm này giúp xử lý các tác vụ như gọi API, đọc/ghi tệp, hoặc thực hiện các thao tác khác mà có thể mất thời gian mà không làm chặn (block) luồng thực thi chính của chương trình.

### Cách Định Nghĩa Hàm Bất Đồng Bộ

Bạn sử dụng từ khóa `async` trước khi khai báo hàm. Ví dụ:

```javascript
async function fetchData() {
  // Mã bất đồng bộ ở đây
}
```

Hoặc với hàm mũi tên:

```javascript
const fetchData = async () => {
  // Mã bất đồng bộ ở đây
};
```

### Cách Sử Dụng `await`

Bên trong một hàm bất đồng bộ, bạn có thể sử dụng từ khóa `await` trước một promise để tạm dừng việc thực thi của hàm cho đến khi promise đó được giải quyết (resolve) hoặc bị từ chối (reject). Điều này giúp mã trông giống như mã đồng bộ, làm cho nó dễ đọc và dễ duy trì hơn.

```javascript
async function fetchData() {
  try {
    const response = await axios.get('https://api.example.com/data');
    console.log(response.data);
  } catch (error) {
    console.error('Error fetching data:', error);
  }
}

fetchData();
```

### Lợi Ích của Hàm Bất Đồng Bộ

1. **Mã Dễ Đọc Hơn**: `async` và `await` giúp mã bất đồng bộ trông giống mã đồng bộ, làm cho nó dễ hiểu hơn.
2. **Xử Lý Lỗi Hiệu Quả Hơn**: Bạn có thể sử dụng `try-catch` để bắt và xử lý lỗi một cách trực quan.
3. **Không Chặn Luồng Thực Thi**: Mặc dù `await` tạm dừng hàm, nó không chặn toàn bộ luồng thực thi của chương trình, cho phép các tác vụ khác tiếp tục chạy.

### Ví Dụ Thực Tế

Dưới đây là một ví dụ đầy đủ về cách sử dụng hàm bất đồng bộ với `async` và `await` để gọi một API và xử lý phản hồi:

```javascript
const axios = require('axios');

async function fetchData() {
  try {
    // Sử dụng await để đợi phản hồi từ API
    const response = await axios.get('https://api.example.com/data');
    // Log dữ liệu nhận được từ API
    console.log(response.data);
  } catch (error) {
    // Bắt và log lỗi nếu có
    console.error('Error fetching data:', error);
  }
}

// Gọi hàm bất đồng bộ
fetchData();
```

Trong ví dụ này:

1. **Khai Báo Hàm Bất Đồng Bộ**:
   - Hàm `fetchData` được khai báo với từ khóa `async`.

2. **Sử Dụng `await`**:
   - `await` được sử dụng trước `axios.get` để đợi cho đến khi phản hồi từ API được trả về.

3. **Xử Lý Lỗi**:
   - Khối `try-catch` được sử dụng để bắt và xử lý lỗi nếu yêu cầu API thất bại.

### Kết Luận

- **Hàm Bất Đồng Bộ**: Cho phép xử lý các tác vụ bất đồng bộ một cách dễ dàng và hiệu quả.
- **Từ Khóa `async`**: Được sử dụng để khai báo một hàm bất đồng bộ.
- **Từ Khóa `await`**: Được sử dụng để tạm dừng việc thực thi của hàm cho đến khi một promise được giải quyết.
- **Lợi Ích**: Giúp mã dễ đọc hơn, quản lý lỗi tốt hơn và không chặn luồng thực thi chính của chương trình.


# Hàm bất đồng bộ và khai báo 


`async` là một từ khóa trong JavaScript được sử dụng để khai báo một hàm bất đồng bộ (asynchronous function). Các hàm này cho phép bạn thực hiện các tác vụ không đồng bộ một cách dễ dàng và trực quan bằng cách sử dụng từ khóa `await` để đợi cho các promise được giải quyết. Đây là một cải tiến quan trọng so với việc sử dụng các callback hoặc promise trực tiếp.

### Công Dụng và Lợi Ích của `async`

1. **Khai Báo Hàm Bất Đồng Bộ**:
   - Khi bạn đặt từ khóa `async` trước một hàm, hàm đó sẽ luôn trả về một promise. Nếu hàm này trả về một giá trị trực tiếp, giá trị đó sẽ được tự động bọc trong một promise đã được giải quyết.
   - Cú pháp:
     ```javascript
     async function myFunction() {
       // mã bất đồng bộ
     }
     ```

2. **Sử Dụng `await`**:
   - Bên trong một hàm `async`, bạn có thể sử dụng từ khóa `await` trước một promise để tạm dừng việc thực thi của hàm cho đến khi promise đó được giải quyết (resolve) hoặc bị từ chối (reject).
   - Điều này giúp viết mã bất đồng bộ mà trông giống như mã đồng bộ, làm cho mã dễ đọc và dễ duy trì hơn.
   - Cú pháp:
     ```javascript
     async function myFunction() {
       const result = await someAsyncOperation();
       console.log(result);
     }
     ```

3. **Xử Lý Lỗi Dễ Dàng**:
   - Bạn có thể sử dụng khối `try-catch` để bắt và xử lý lỗi khi sử dụng `await`, giúp việc quản lý lỗi trở nên dễ dàng và rõ ràng hơn.

### Ví Dụ Thực Tế

#### Ví Dụ 1: Hàm `async` Cơ Bản

```javascript
async function fetchData() {
  return "Hello, world!";
}

fetchData().then(console.log); // In ra: Hello, world!
```

#### Ví Dụ 2: Sử Dụng `await` để Đợi Một Promise

```javascript
async function fetchData() {
  const response = await axios.get('https://api.example.com/data');
  console.log(response.data);
}

fetchData();
```

#### Ví Dụ 3: Xử Lý Lỗi với `try-catch`

```javascript
async function fetchData() {
  try {
    const response = await axios.get('https://api.example.com/data');
    console.log(response.data);
  } catch (error) {
    console.error('Error fetching data:', error);
  }
}

fetchData();
```

### Cách `async` và `await` Hoạt Động

- **Khai Báo Hàm `async`**: Khi bạn khai báo một hàm là `async`, nó sẽ luôn trả về một promise. Ngay cả khi bạn trả về một giá trị thông thường, giá trị đó sẽ được bọc trong một promise đã được giải quyết.
- **Sử Dụng `await`**: Bên trong một hàm `async`, bạn có thể sử dụng `await` trước một promise để tạm dừng việc thực thi hàm cho đến khi promise đó được giải quyết. `await` chỉ có thể được sử dụng bên trong các hàm được khai báo với `async`.

### So Sánh với Promise và Callback

- **Callback**: Trước đây, để xử lý các tác vụ bất đồng bộ, chúng ta thường sử dụng callback, nhưng cách này có thể dẫn đến "callback hell" khi có nhiều lớp lồng nhau.
- **Promise**: Promise giúp cải thiện quản lý mã bất đồng bộ bằng cách sử dụng chuỗi `.then()`, nhưng mã vẫn có thể trở nên phức tạp nếu có nhiều promise lồng nhau.
- **Async/Await**: `async/await` làm cho mã trông giống như mã đồng bộ, giúp dễ đọc và dễ duy trì hơn, đồng thời cho phép quản lý lỗi một cách trực quan hơn bằng cách sử dụng khối `try-catch`.

### Tổng Kết

- **`async`**: Được sử dụng để khai báo một hàm bất đồng bộ, làm cho hàm đó luôn trả về một promise.
- **`await`**: Được sử dụng bên trong các hàm `async` để tạm dừng việc thực thi hàm cho đến khi promise được giải quyết hoặc bị từ chối.
- **Lợi Ích**: Giúp mã bất đồng bộ trở nên dễ đọc, dễ viết và dễ duy trì hơn, đồng thời quản lý lỗi hiệu quả hơn.





# Promises và những vấn đề liên quan khi lấy dữ liệu từ  API

Promises là một tính năng trong JavaScript được sử dụng để quản lý các tác vụ bất đồng bộ. Chúng giúp bạn xử lý các hoạt động như tải tài nguyên từ mạng, đọc/ghi dữ liệu từ tệp, hay thực hiện các tác vụ khác mà có thể mất thời gian mà không làm chặn (block) luồng thực thi chính của chương trình. Dưới đây là giải thích chi tiết về các promise trong JavaScript:

### Promise Là Gì?

Promise là một đối tượng đại diện cho một giá trị có thể chưa có ngay lập tức nhưng sẽ được cung cấp vào một thời điểm nào đó trong tương lai. Một promise có thể ở trong một trong ba trạng thái:

1. **Pending (Đang Chờ)**: Trạng thái ban đầu, chưa hoàn thành cũng như chưa bị từ chối.
2. **Fulfilled (Đã Hoàn Thành)**: Đã hoàn thành và trả về một giá trị.
3. **Rejected (Bị Từ Chối)**: Đã bị từ chối và trả về một lý do (error).

### Cách Sử Dụng Promises

#### Tạo Một Promise

Bạn có thể tạo một promise bằng cách sử dụng từ khóa `new Promise` và truyền vào một hàm thực thi (executor function) với hai đối số: `resolve` và `reject`.

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Thực hiện một tác vụ bất đồng bộ
  let success = true; // Điều kiện thành công giả định

  if (success) {
    resolve('Tác vụ đã hoàn thành!');
  } else {
    reject('Tác vụ thất bại.');
  }
});
```

#### Sử Dụng `.then()`, `.catch()`, và `.finally()`

Bạn có thể xử lý kết quả của promise bằng cách sử dụng các phương thức `.then()`, `.catch()`, và `.finally()`.

```javascript
myPromise
  .then(result => {
    console.log(result); // Xử lý kết quả nếu promise hoàn thành
  })
  .catch(error => {
    console.error(error); // Xử lý lỗi nếu promise bị từ chối
  })
  .finally(() => {
    console.log('Tác vụ đã kết thúc.'); // Thực thi bất kể promise thành công hay thất bại
  });
```

#### Ví Dụ Thực Tế

Giả sử bạn muốn thực hiện một yêu cầu HTTP để lấy dữ liệu từ một API. Đây là cách bạn có thể làm điều đó bằng cách sử dụng promises và thư viện `axios`:

```javascript
const axios = require('axios');

const fetchData = () => {
  return axios.get('https://api.example.com/data');
};

fetchData()
  .then(response => {
    console.log(response.data); // Xử lý dữ liệu từ API
  })
  .catch(error => {
    console.error('Lỗi khi lấy dữ liệu:', error); // Xử lý lỗi nếu yêu cầu thất bại
  });
```

#### Kết Hợp Nhiều Promises

Bạn có thể kết hợp nhiều promises bằng cách sử dụng `Promise.all`, `Promise.race`, `Promise.allSettled`, và `Promise.any`.

- **`Promise.all`**: Chờ cho tất cả promises hoàn thành.
- **`Promise.race`**: Trả về kết quả của promise đầu tiên hoàn thành hoặc bị từ chối.
- **`Promise.allSettled`**: Chờ cho tất cả promises hoàn thành hoặc bị từ chối và trả về kết quả của tất cả.
- **`Promise.any`**: Trả về kết quả của promise đầu tiên hoàn thành thành công.

```javascript
const promise1 = new Promise((resolve, reject) => setTimeout(resolve, 500, 'Promise 1 hoàn thành'));
const promise2 = new Promise((resolve, reject) => setTimeout(resolve, 100, 'Promise 2 hoàn thành'));

Promise.all([promise1, promise2])
  .then(results => {
    console.log(results); // ['Promise 1 hoàn thành', 'Promise 2 hoàn thành']
  })
  .catch(error => {
    console.error(error);
  });
```

### Tóm Tắt

Promises giúp quản lý các tác vụ bất đồng bộ trong JavaScript:

- **Định Nghĩa**: Là đối tượng đại diện cho giá trị có thể chưa có ngay lập tức nhưng sẽ có trong tương lai.
- **Trạng Thái**: Pending, Fulfilled, Rejected.
- **Phương Thức**: `.then()` để xử lý kết quả thành công, `.catch()` để xử lý lỗi, `.finally()` để thực hiện tác vụ bất kể kết quả.
- **Kết Hợp Promises**: `Promise.all`, `Promise.race`, `Promise.allSettled`, `Promise.any` để xử lý nhiều promises.

Promises giúp mã trở nên rõ ràng và dễ bảo trì hơn khi làm việc với các tác vụ bất đồng bộ phức tạp.