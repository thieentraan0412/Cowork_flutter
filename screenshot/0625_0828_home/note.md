# Lỗi HOME — 25/06/2026 08:28

> Lưu ý: Công cụ chụp màn hình trong phiên này KHÔNG ghi được ảnh ra đĩa, nên mô tả lỗi bằng văn bản + các bước tái hiện thay cho ảnh .png/.jpg.

## Lỗi #1 — [1.20.2] Renderer Flutter bị đơ khi thao tác nhanh
- **Bước tái hiện:**
  1. Trang chủ (Cashier).
  2. Bấm dropdown khu ("khu 1") ở thanh công cụ.
  3. Click chọn mục trong dropdown liên tiếp + click thẻ bàn ngay sau đó.
- **Hiện tượng:** overlay dropdown kẹt mở; click không phản hồi; lệnh chụp màn hình báo timeout ~30s: *"CDP Page.captureScreenshot timed out … renderer may be frozen or unresponsive"*.
- **Khắc phục:** điều hướng/tải lại URL gốc `https://order-flutter.nasys.vn/` → app phục hồi, giữ đăng nhập & vai trò Cashier, không mất dữ liệu bàn.
- **Mức độ:** trung bình–cao (ảnh hưởng thao tác thu ngân, buộc reload).
