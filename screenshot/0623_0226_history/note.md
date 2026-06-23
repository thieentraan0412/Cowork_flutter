# Ảnh lỗi — HISTORY (0623_0226)

> Công cụ chụp màn hình trình duyệt trong phiên này không lưu được file ảnh ra đĩa workspace (giống các phiên trước). Lỗi được mô tả bằng văn bản kèm dữ liệu đối chứng.

## LỖI CHẶN — Đăng nhập thất bại (server-side DB error)

- Trang: https://order-flutter.nasys.vn/#/auth-route
- Nhập đúng: ID cửa hàng `thientester`, Tên đăng nhập `admin`, Mật khẩu `12345678` → bấm **Đăng nhập**.
- Toast đỏ **"Thất bại"** hiện ra mỗi lần bấm (tái hiện ≥5 lần liên tiếp):

```
Thất bại
SQLSTATE[42S02]: Base table or view not found: 1146
Table 'order_table_thientester.hrm_employees' doesn't exist
(SQL: select * from `hrm_employees`
 where `email` = admin or `code` = admin or `username` = admin limit 1)
```

- API gọi: `POST https://table1.klkim.com/v2/api/m/login` (preflight OPTIONS trả 204; POST trả lỗi DB trên).
- Nguyên nhân: bảng `hrm_employees` trong database `order_table_thientester` KHÔNG tồn tại ở backend ⇒ hệ thống không xác thực được tài khoản ⇒ không vào được Cashier/History.
- Đây là lỗi cấu hình **phía server (database)**, không phải lỗi nhập sai thông tin; không thể khắc phục từ phía client.
