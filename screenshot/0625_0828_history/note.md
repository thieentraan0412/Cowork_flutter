# Phát hiện HISTORY — 25/06/2026 08:28

> Công cụ chụp màn hình không ghi ảnh ra đĩa trong phiên này → mô tả văn bản.

## Phát hiện #1 — [1.1.4] Thiếu tab "Đặt online"
- Trang Lịch sử chỉ có 3 tab loại đơn: **Tất cả / Tại bàn / Mang về**.
- Checklist gốc kỳ vọng có thêm tab **"Đặt online"** → không thấy. Cần xác nhận đây là thay đổi thiết kế hay thiếu sót.

## Phát hiện #2 — Render trắng trang khi vào từ màn Order (intermittent)
- **Bước tái hiện:** đang ở màn Order của 1 bàn → bấm "Lịch sử" trên thanh nav.
- **Hiện tượng:** vùng nội dung Lịch sử trắng/đen hoàn toàn (chỉ còn thanh nav) ~14s; lệnh chụp màn hình từng timeout.
- **Khắc phục:** tải lại trang → Lịch sử hiển thị đầy đủ danh sách. Liên quan lỗi ổn định renderer (HOME 1.20.2).
