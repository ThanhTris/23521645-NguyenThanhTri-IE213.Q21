**Mục tiêu bài thực hành**
- **Mục tiêu:** Thực hành thao tác cơ bản với MongoDB (CRUD) và sử dụng Aggregation để tính toán thống kê.

**Công cụ / Môi trường sử dụng**
- **Dịch vụ:** MongoDB Atlas (cluster đám mây).
- **Công cụ:** MongoDB Compass (và MONGOSH / Mongo Shell tích hợp trong Compass).

**Cách chạy**
- **Chuẩn bị:** Kết nối đến cluster Atlas bằng MongoDB Compass hoặc `mongosh`.
- **Chạy lệnh trong file:** Mở [Lab01/lab01.js](Lab01/lab01.js) để xem các lệnh mẫu; các bước chính thực hiện lần lượt là:
	- `use 23521645-IE213` — chuyển sang cơ sở dữ liệu (thay `23521645` bằng mã số sinh viên nếu khác).
	- `db.employees.insertMany([...])` — thêm các document mẫu vào collection `employees`.
	- `db.employees.createIndex({ id: 1 }, { unique: true })` — tạo index để đảm bảo `id` là duy nhất.
	- Các phép truy vấn mẫu: `db.employees.find({...})`, `db.employees.aggregate([...])`, `db.employees.updateMany(...)`.

**Kết quả đầu ra (mong đợi)**
- **Collection:** Một database có tên `23521645-IE213` chứa collection `employees`.
- **Index:** Trường `id` có ràng buộc `unique` — không thể chèn trùng `id`.
- **Truy vấn:** Kết quả trả về từ các lệnh `find()` theo bộ lọc (ví dụ tên, tuổi, tồn tại `middle` name).
- **Aggregation:** Kết quả `totalAge` và `avgAge` nhóm theo `organization` từ `db.employees.aggregate()`.
- **Cập nhật:** Trường `name.middle` đã được xóa (nếu cần) và trường `organization` được thêm/sửa cho các document.

**Giải thích ngắn gọn các phần chính đã thực hiện**
- **Tạo DB/Collection:** `use 23521645-IE213` chuyển ngữ cảnh DB; `insertMany()` thêm nhiều document mẫu.
- **Đảm bảo tính duy nhất của `id`:** `createIndex({ id: 1 }, { unique: true })` tránh trùng lặp id khi chèn mới.
- **Truy vấn cơ bản:**
	- Tìm theo tên: `db.employees.find({ "name.first": "John", "name.last": "Doe" })`.
	- Tìm theo khoảng tuổi: `db.employees.find({ $and: [ { age: { $gt: 30 } }, { age: { $lt: 60 } } ] })`.
	- Tìm document có `middle` name: `db.employees.find({ "name.middle": { $exists: true } })`.
- **Cập nhật dữ liệu:**
	- Xoá `middle` name: `db.employees.updateMany({ "name.middle": { $exists: true } }, { $unset: { "name.middle": "" } })`.
	- Thêm trường `organization` cho tất cả: `db.employees.updateMany({}, { $set: { organization: "UIT" } })`.
	- Điều chỉnh `organization` cho `id` 5 và 6: `db.employees.updateMany({ id: { $in: [5,6] } }, { $set: { organization: "USSH" } })`.
- **Aggregation (thống kê):** `db.employees.aggregate([{ $group: { _id: "$organization", totalAge: { $sum: "$age" }, avgAge: { $avg: "$age" } } }])` — nhóm theo `organization` để tính tổng và trung bình tuổi.

**Ghi chú & sửa lỗi nhỏ**
- **Tên database chính xác:** Sửa lỗi gõ nhầm trong phiên bản trước — tên DB phải là `23521645-IE213` (không phải `235231645-IE213`).
- **Đảm bảo chạy theo thứ tự:** Tạo index `unique` chỉ nên thực hiện sau khi không còn giá trị `id` trùng lặp trong collection, nếu không lệnh sẽ lỗi.

Nếu bạn muốn, tôi có thể:
- Chạy kiểm tra nhanh các lệnh trong `lab01.js` (tôi sẽ hướng dẫn cách thực hiện trong `mongosh`).
- Ghi thêm ví dụ đầu ra mẫu cho từng truy vấn.

Tệp lệnh tham khảo: [Lab01/lab01.js](Lab01/lab01.js)