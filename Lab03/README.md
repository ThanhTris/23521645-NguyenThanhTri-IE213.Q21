**Mục tiêu bài thực hành**
- Hoàn thiện back-end cho ứng dụng Movie Reviews theo mô hình Route -> Controller -> DAO.
- Xây dựng các API phục vụ thêm, sửa, xóa review và tra cứu dữ liệu phim.
- Kết nối backend với MongoDB Atlas và kiểm thử các endpoint bằng Insomnia hoặc công cụ tương đương.

**Công cụ / Môi trường sử dụng**
- Node.js và JavaScript ES6.
- Trình soạn thảo mã nguồn: Visual Studio Code.
- Thư viện chính: `express`, `cors`, `dotenv`, `mongodb`, `nodemon`.
- Cơ sở dữ liệu: MongoDB Atlas Cloud.
- Công cụ kiểm thử API: Insomnia.

**Cách chạy**
- **Bước 1:** Mở thư mục `movie-reviews/backend` và cài các package cần thiết bằng `npm install`.
- **Bước 2:** Kiểm tra file `.env` với các biến `MOVIEREVIEWS_DB_URI`, `MOVIEREVIEWS_NS`, `PORT`.
- **Bước 3:** Chạy backend bằng `npm run dev` hoặc `node index.js`.
- **Bước 4:** Gửi các request đến các endpoint sau để kiểm thử:
	- `GET /api/v1/movies`
	- `GET /api/v1/movies/id/:id`
	- `GET /api/v1/movies/ratings`
	- `POST /api/v1/movies/review`
	- `PUT /api/v1/movies/review`
	- `DELETE /api/v1/movies/review`

**Kết quả đầu ra**
- Backend khởi động thành công và lắng nghe tại cổng cấu hình trong `.env`.
- API trả về dữ liệu phim, danh sách review theo phim, và danh sách các rating hiện có.
- Người dùng có thể thêm, sửa, xóa review thông qua API `/api/v1/movies/review`.

**Giải thích ngắn gọn phần chính đã thực hiện**
- **Routing:** Dùng `express.Router()` để định tuyến các yêu cầu đến đúng controller tương ứng.
- **Controller:** Nhận dữ liệu từ `req.body` hoặc `req.params`, gọi xuống DAO và trả phản hồi JSON cho client.
- **DAO:** Thao tác trực tiếp với MongoDB bằng các hàm như `insertOne`, `updateOne`, `deleteOne`, `aggregate` và `distinct`.
- **Kết nối dữ liệu:** `index.js` khởi tạo MongoClient, kết nối đến MongoDB Atlas, rồi inject collection cho các DAO trước khi chạy server.
- **Kiểm thử:** Dùng Insomnia để gửi request và kiểm tra phản hồi của từng endpoint.

**Bài 1: Thiết lập định tuyến (Routing) cho Review**

**Mục tiêu bài thực hành**
- Thiết lập các đường dẫn (route) để điều hướng các yêu cầu HTTP liên quan đến review đến đúng hàm xử lý trong controller.

**Công cụ / Môi trường sử dụng**
- JavaScript ES6.
- Thư viện `express`.
- Tệp `api/movies.route.js`.

**Cách chạy**
- Import `ReviewsController` vào tệp router.
- Sử dụng `router.route('/review')` để khai báo các phương thức `post`, `put`, `delete`.

**Kết quả đầu ra**
- Một hệ thống định tuyến hoàn chỉnh tại `http://localhost:3000/api/v1/movies/review` sẵn sàng tiếp nhận các yêu cầu thêm, sửa, xóa review.

**Giải thích ngắn gọn phần chính đã thực hiện**
- Sử dụng `express.Router()` để ánh xạ các phương thức HTTP vào các hàm xử lý trong `ReviewsController`.

**Bài 2: Thiết lập Controller cho Review**

**Mục tiêu bài thực hành**
- Tạo lớp điều khiển để quản lý logic nghiệp vụ, tiếp nhận dữ liệu từ yêu cầu của người dùng và gửi phản hồi về máy khách.

**Công cụ / Môi trường sử dụng**
- JavaScript ES6.
- Tệp `api/reviews.controller.js`.

**Cách chạy**
- Định nghĩa các phương thức tĩnh `apiPostReview`, `apiUpdateReview`, `apiDeleteReview`.
- Lấy dữ liệu từ `req.body` và gọi xuống tầng DAO tương ứng.

**Kết quả đầu ra**
- Các phản hồi JSON trả về trạng thái `success` hoặc thông báo lỗi nếu có sự cố xảy ra.

**Giải thích ngắn gọn phần chính đã thực hiện**
- Controller đóng vai trò trung gian: trích xuất dữ liệu từ yêu cầu, gọi hàm tương ứng trong `ReviewsDAO` để tương tác với cơ sở dữ liệu và trả kết quả cho khách hàng.

**Bài 3: Thiết lập DAO (Data Access Object) cho Reviews**

**Mục tiêu bài thực hành**
- Xây dựng tầng giao tiếp trực tiếp với cơ sở dữ liệu MongoDB để thực hiện các thao tác CRUD trên collection `reviews`.

**Công cụ / Môi trường sử dụng**
- Thư viện `mongodb`.
- Tệp `dao/reviewsDAO.js`.

**Cách chạy**
- Sử dụng phương thức `injectDB` để kết nối collection.
- Dùng các hàm của MongoDB như `insertOne`, `updateOne`, `deleteOne`.

**Kết quả đầu ra**
- Dữ liệu review được lưu trữ, cập nhật hoặc xóa bỏ thực sự trong cơ sở dữ liệu MongoDB.

**Giải thích ngắn gọn phần chính đã thực hiện**
- Chuyển đổi các tham số dạng chuỗi thành `ObjectId` và thực hiện truy vấn xuống DB.
- Kiểm tra điều kiện `user_id` trùng khớp trước khi cho phép sửa hoặc xóa để đảm bảo tính bảo mật.

**Bài 4: Hoàn thiện Back-end và Kiểm thử**

**Mục tiêu bài thực hành**
- Bổ sung các tính năng tra cứu nâng cao như lấy phim theo ID kèm review, lấy danh sách các loại rating, và kiểm tra toàn bộ API.

**Công cụ / Môi trường sử dụng**
- Insomnia hoặc công cụ tương đương để test API.
- Toán tử `$lookup` và `aggregate` trong MongoDB.

**Cách chạy**
- Thêm route mới trong router.
- Thêm phương thức xử lý trong controller và DAO.
- Dùng Insomnia gửi yêu cầu đến các endpoint đã tạo để kiểm thử.

**Kết quả đầu ra**
- Dữ liệu trả về đầy đủ thông tin phim kèm danh sách các review liên quan.
- Trả về mảng các loại rating hiện có trong cơ sở dữ liệu.

**Giải thích ngắn gọn phần chính đã thực hiện**
- Sử dụng `aggregate` và `$lookup` để gộp dữ liệu từ hai collection `movies` và `reviews` dựa trên ID phim, giúp lấy thông tin tổng hợp trong một lần gọi API.
