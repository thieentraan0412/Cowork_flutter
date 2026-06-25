# Phát hiện RESERVE (Bàn đặt) — 25/06/2026 08:45

> Công cụ chụp màn hình không ghi ảnh ra đĩa trong phiên này → mô tả văn bản.

## Phát hiện — Render trắng trang khi vào lần đầu (intermittent)
- **Bước tái hiện:** bấm menu "Bàn đặt" từ một trang khác.
- **Hiện tượng:** vùng nội dung trắng hoàn toàn ~10s (chỉ còn thanh nav).
- **Khắc phục:** tải lại trang (về URL gốc) → trang Bàn đặt hiển thị đầy đủ (tab ngày, danh sách, panel tra cứu, nút Đặt bàn).
- Liên quan lỗi ổn định renderer Flutter (HOME 1.20.2, HISTORY).

## Đối chiếu tốt (không lỗi)
- Form "Đặt bàn" validate đúng: bỏ trống → "Vui lòng chọn khách hàng, giờ và bàn".
