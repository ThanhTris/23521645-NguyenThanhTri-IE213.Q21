**Mục tiêu bài thực hành**
- Thiết lập backend cho ứng dụng Movie bằng Node.js và ExpressJS.
- Kết nối backend tới MongoDB Atlas.
- Xây dựng API cơ bản theo luồng Route -> Controller -> DAO để truy xuất dữ liệu phim.

**Công cụ / Môi trường sử dụng**
- Node.js.
- Trình soạn thảo mã nguồn: Visual Studio Code (hoặc công cụ tương đương).
- Dependency chính: `express`, `cors`, `dotenv`, `mongodb`.
- Công cụ hỗ trợ chạy phát triển: `nodemon`.
- Cơ sở dữ liệu: MongoDB Atlas Cloud.

**Cách chạy**
- **Bước 1:** Tạo thư mục dự án `movie-reviews/backend` và khởi tạo npm bằng `npm init`.
- **Bước 2:** Cài package cần thiết bằng `npm install express cors dotenv mongodb`.
- **Bước 3:** Cài `nodemon` để tự động restart server khi code thay đổi.
- **Bước 4:** Tạo các file chính:
	- `server.js` để khởi tạo Express app và middleware.
	- `.env` để cấu hình `MOVIEREVIEWS_DB_URI`, `MOVIEREVIEWS_NS`, `PORT`.
	- `index.js` để kết nối MongoDB Atlas và chạy server.
	- `api/movies.route.js` để định tuyến API.
	- `dao/moviesDAO.js` để truy xuất dữ liệu collection `movies`.
	- `api/movies.controller.js` để nhận request và trả response.
- **Bước 5:** Chạy backend bằng `npm run dev` hoặc `node index.js`.
- **Bước 6:** Truy cập `http://localhost:3000/api/v1/movies` để kiểm tra kết quả.

**Kết quả đầu ra (mong đợi)**
- Backend chạy thành công trên cổng được cấu hình (ví dụ `3000`).
- API `GET /api/v1/movies` trả dữ liệu JSON.
- Hoàn thiện cấu trúc backend theo mô hình tách lớp:
	- route xử lý định tuyến.
	- controller xử lý request/response.
	- DAO thao tác truy xuất dữ liệu MongoDB.

**Các phần chính đã thực hiện**
- **Khởi tạo server:** Dùng Express, bật `cors` và parse JSON.
- **Kết nối cơ sở dữ liệu:** Dùng MongoClient với URI trong `.env` để kết nối MongoDB Atlas.
- **Thiết lập DAO:**
	- `injectDB()` nhận kết nối và lấy collection `movies`.
	- `getMovies()` trả về `moviesList` và `totalNumMovies` với mặc định `filters = null`, `page = 0`, `moviesPerPage = 20`.
- **Thiết lập Controller:** Nhận request từ route, gọi DAO để lấy dữ liệu, trả JSON cho client.
- **Thiết lập Routing:** Ánh xạ endpoint `/api/v1/movies` vào controller.

**Hình ảnh minh họa**

**Bài 1 — Chuẩn bị môi trường**

![1.1 install Node.js](images/step1_1_install_nodejs.png)

![1.2 install code editor](images/step1_2_install_editor.png)

![1.3 init project tree](images/step1_3_init_project_tree.png)

![1.4 npm init](images/step1_4_npm_init.png)

![1.5 install dependencies](images/step1_5_install_dependencies.png)

![1.6 install nodemon](images/step1_6_install_nodemon.png)

**Bài 2 — Xây dựng backend và API**

![2.1 server.js](images/step2_1_server_js.png)

![2.2 env](images/step2_2_env_file.png)

![2.3 index.js](images/step2_3_index_js.png)

![2.4 movies route](images/step2_4_movies_route.png)

![2.4.1 endpoint result](images/step2_4_1_endpoint_result.png)

![2.5 movies dao](images/step2_5_movies_dao.png)

![2.5.1 inject dao](images/step2_5_1_injectdb_index.png)

![2.6 movies controller](images/step2_6_movies_controller.png)

![2.7 route + controller](images/step2_7_route_controller.png)

![2.8 final browser result](images/step2_8_final_browser_result.png)
