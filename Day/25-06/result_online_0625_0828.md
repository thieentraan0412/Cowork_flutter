# Kết quả kiểm thử — ONLINE (Đặt online)

- Menu: online (Đặt online) — route `#/pos-shell-route/pos-booking-route`
- Ngày giờ: 25/06/2026 08:47 (+07)
- Người/agent thực hiện: Claude (Cowork) — trình duyệt Chrome
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Cashier — Phiên bản 1.0.0+77

## Phát hiện chính
> ⚠️ **Menu "Đặt online" CHƯA ĐƯỢC TRIỂN KHAI.** Trang chỉ hiển thị placeholder: **"Tính năng 'booking' đang phát triển"** (kèm icon ô vuông). Không có danh sách đơn online, không có chức năng nhận/từ chối/cập nhật trạng thái.

→ Toàn bộ checklist Online ở trạng thái **BLOCKED** do tính năng đang phát triển.

## Bảng kết quả
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.1 (Hiển thị đơn online) | BLOCKED | Tính năng "booking" đang phát triển — không có danh sách đơn |
| 1.1.1 / 1.1.2 | BLOCKED | Không có dữ liệu/giao diện đơn online |
| 1.2 (Thông báo đơn mới) | BLOCKED | Không áp dụng |
| 2.1 / 2.1.1 (Nhận đơn) | BLOCKED | Không có chức năng |
| 2.2 (Từ chối đơn) | BLOCKED | Không có chức năng |
| 2.3 / 2.3.1 (Cập nhật trạng thái) | BLOCKED | Không có chức năng |
| 3.1 / 3.2 (Chi tiết đơn) | BLOCKED | Không có chức năng |
| 4.1 (Đồng bộ History) | BLOCKED | Không có đơn online để đồng bộ |
| 4.2 (Doanh thu online) | BLOCKED | Không áp dụng |
| 5.1 / 5.2 (Hiệu năng) | BLOCKED | Không áp dụng |

## Tổng hợp
- PASS: 0
- FAIL: 0
- BLOCKED: tất cả (tính năng đang phát triển)
- N/A: 0

## Danh sách lỗi / phát hiện
1. **[Tính năng] Đặt online chưa triển khai** — trang hiển thị "Tính năng 'booking' đang phát triển". Không thể kiểm thử bất kỳ luồng đơn online nào ở phiên bản 1.0.0+77. Mô tả: `screenshot/0625_0828_online/note.md`.
