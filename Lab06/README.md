**Mục tiêu bài thực hành**
- Bổ sung chức năng đăng nhập để người dùng nhìn thấy Edit/Delete ở review của chính họ.
- Thêm mới và sửa review ngay trên trang chi tiết movie.
- Xoá review của chính user đang đăng nhập và cập nhật giao diện sau khi xoá.

**Cấu trúc thư mục**
```
Lab06/
├─ images/                   # hình ảnh minh họa kết quả Lab06
│  ├─ lab06-pagination-button-code.png
│  ├─ lab06-pagination-getall-code.png
│  ├─ lab06-pagination-search-code1.png
│  ├─ lab06-pagination-search-code2.png
│  ├─ lab06-pagination-result.png
│  └─ lab06-search-result.png
├─ movie-reviews/
│  ├─ backend/               # Backend API Movie Reviews
│  └─ frontend/              # Frontend ReactJS Movie Reviews
│     ├─ src/
│     │  ├─ components/
│     │  │  ├─ add-review.js
│     │  │  ├─ login.js
│     │  │  └─ movies-list.js
│     │  └─ App.js
│     └─ package.json
└─ README.md                 # hướng dẫn chi tiết Lab06
```

**Công cụ / môi trường sử dụng**
- ReactJS.
- React Router Dom.
- React-Bootstrap.

**Cách chạy**
- **Bước 1:** Đảm bảo Backend đang chạy ổn định tại địa chỉ `http://localhost:5000`.
- **Bước 2:** Di chuyển vào thư mục frontend của Lab06 và khởi chạy ứng dụng bằng lệnh `npm start`.
- **Bước 3: Thực hiện Bài 1 (Thêm/Sửa):**
  - Người dùng truy cập trang Login (`/login`), nhập Username và ID để đăng nhập.
  - Hệ thống tự động chuyển hướng (redirect) về trang Home sau khi đăng nhập thành công.
  - Tại trang chi tiết phim, nhấn "Add Review" để thêm mới đánh giá hoặc nhấn "Edit" trên đánh giá của chính mình để chỉnh sửa.
- **Bước 4: Thực hiện Bài 2 (Xóa):**
  - Đăng nhập vào tài khoản, tìm đến đánh giá do chính mình viết và nhấn nút "Delete".
- **Bước 5: Thực hiện Bài 3 (Phân trang):**
  - Tại trang danh sách phim, cuộn xuống dưới cùng để xem số trang hiện tại.
  - Nhấn nút "Get next ... results" để tải thêm dữ liệu của trang tiếp theo.

**Kết quả đầu ra**
- Đăng nhập thành công sẽ quay về trang Home.
- Review của user đăng nhập sẽ hiện Edit/Delete.
- Có thể thêm, sửa, xoá review trực tiếp trên giao diện movie.

**Giải thích ngắn gọn phần chính đã thực hiện**
- **Bài 1: Thêm/Sửa Review**
  - Sử dụng biến trạng thái `editing` (boolean) để xác định xem người dùng đang thêm mới hay sửa dựa trên props truyền vào (`currentReview`).
  - Hàm `saveReview` sẽ kiểm tra biến `editing` để quyết định gọi `createReview` hoặc `updateReview` từ `MovieDataService`.
- **Bài 2: Xoá Review**
  - Khi nhấn "Delete", hàm `deleteReview` được gọi với `reviewId` và `index` của review đó trong mảng.
  - Sau khi API backend phản hồi thành công, sử dụng hàm `splice(index, 1)` để loại bỏ review khỏi mảng `reviews` trong state `movie`, giao diện cập nhật ngay lập tức.
- **Bài 3: Phân trang danh sách phim**
  - Sử dụng `useEffect` lắng nghe sự thay đổi của biến `currentPage`. Mỗi khi `currentPage` thay đổi (tăng lên), hàm `retrieveMovies()` hoặc `retrieveNextPage()` sẽ được gọi lại để lấy dữ liệu trang mới từ server.
  - Thêm biến `currentSearchMode` để quản lý trạng thái đang tìm kiếm theo tiêu chí nào (`"findByTitle"`, `"findByRating"` hoặc `""`), giúp tự động reset `currentPage` về 0 khi người dùng thay đổi cách tìm kiếm.
