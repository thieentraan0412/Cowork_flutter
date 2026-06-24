# Kết quả kiểm thử — RESERVE (Đặt bàn)

- Menu: reserve
- Ngày giờ: 24/06 05:55 (UTC)
- Người/agent thực hiện: Claude (Cowork)
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Thu ngân — CN1
- Trình duyệt: Chrome (qua tiện ích điều khiển) — Browser 1
- Thư mục ảnh lỗi: `screenshot/0624_0555_reserve/`

## Ghi chú chung
- Trang Reserve hiện **"Bàn đặt (0)"** — hiện **không có đặt bàn nào**.
- Bố cục: bên trái là **lịch theo ngày** (Mon 22/06 · Tue 23/06 · **Hôm nay** · Thu 25/06 · Fri 26/06 · Sat 27/06 · Sun 28/06); bên phải là **form tra cứu đặt bàn**.
- Giới hạn công cụ (Flutter web): **không nhập được text** vào các ô (Họ và tên, SĐT, Thời gian) → không tạo/sửa/tra cứu được bằng dữ liệu nhập; app **đơ/giật** (screenshot time-out ~1 lần ở menu này).

---

## 1. Hiển thị danh sách đặt bàn

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.1.1 | Hiển thị danh sách đặt bàn theo ngày | PASS | Có thanh chọn ngày (Mon→Sun), mặc định "Hôm nay". Vùng danh sách hiện empty state đúng: **"Chưa có lịch đặt bàn"** (0 đặt bàn) |
| 1.1.2 | Mỗi đặt bàn có: tên khách, SĐT, số người, thời gian, bàn | N/A | Không có đặt bàn nào để đối chiếu. Tuy nhiên **form tra cứu** xác nhận hệ thống quản lý các trường: Thời gian (Từ/Đến), Chọn bàn, Trạng thái, Họ và tên, Số điện thoại |

## 2. Tạo đặt bàn mới

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 2.1.1 | Nhập đủ thông tin bắt buộc | **BLOCKED (giới hạn công cụ)** | Form có các ô Họ và tên / SĐT / Thời gian / Chọn bàn / Trạng thái, nhưng **không nhập được text** qua điều khiển tự động (Flutter). Cần kiểm thử tay |
| 2.1.2 | Ràng buộc dữ liệu (SĐT hợp lệ, thời gian không quá khứ) | BLOCKED | Phụ thuộc nhập liệu |
| 2.2.1 | Đặt bàn xuất hiện trong danh sách sau khi lưu | BLOCKED | Phụ thuộc tạo được đặt bàn |
| 2.3 | Cảnh báo trùng bàn / trùng giờ | BLOCKED | Phụ thuộc tạo được đặt bàn |

## 3. Sửa / Hủy đặt bàn

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 3.1 | Sửa thông tin và lưu | N/A / BLOCKED | Không có đặt bàn để sửa (0 bản ghi) |
| 3.2.1 | Hủy → trạng thái "đã hủy" | N/A / BLOCKED | Không có đặt bàn để hủy |
| 3.2.2 | Bàn được giải phóng | N/A / BLOCKED | — |

## 4. Chuyển đặt bàn thành order

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 4.1.1 | Check-in → mở order, trạng thái "đã nhận bàn" | N/A / BLOCKED | Không có đặt bàn để check-in |

## 5. Hiệu năng & ổn định

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 5.1 | Thao tác không gây lỗi | KHÔNG KIỂM THỬ | Chưa thực hiện được thao tác tạo/sửa/hủy (nhập liệu bị chặn) |
| 5.2 | Dữ liệu cập nhật ngay | KHÔNG KIỂM THỬ | — |
| — | Ổn định render | Lưu ý | App đơ/giật, screenshot time-out 1 lần khi mở trang (giống các menu khác) |

---

## Tổng hợp
- **PASS: 1** — 1.1.1 (hiển thị lịch theo ngày + empty state đúng)
- **N/A: 1** — 1.1.2 (0 đặt bàn)
- **BLOCKED:** toàn bộ mục 2 (tạo mới — không nhập được text), mục 3 & 4 (không có dữ liệu để sửa/hủy/check-in)
- **KHÔNG KIỂM THỬ:** 5.1, 5.2

## Kết luận / khuyến nghị
- Trang hiển thị đúng cấu trúc (lịch theo ngày + empty state + form tra cứu với đủ trường tên/SĐT/thời gian/bàn/trạng thái).
- **Không thể kiểm thử luồng tạo/sửa/hủy/check-in bằng tự động** vì (1) cần **nhập text** (Flutter chặn) và (2) hiện **không có đặt bàn nào**. Khuyến nghị **kiểm thử tay**: tạo 1 đặt bàn thử (tên/SĐT giả), kiểm tra ràng buộc, cảnh báo trùng, sửa/hủy, và check-in chuyển thành order.
