# Ghi chú ảnh lỗi — Coordination (Điều phối ca) — 0623_0124

> Công cụ chụp màn hình của extension **không lưu được file ảnh ra đĩa** trong phiên này (đã xác nhận lại như các phiên trước). Dưới đây mô tả bằng văn bản + số liệu đối chứng cho từng lỗi/độ lệch để tái hiện.

## FAIL-01 — 1.1.8: Không có nút "Mở màn hình phụ"
- **Route:** `#/pos-shell-route/pos-shift-route`
- **Panel ca đang mở (SCR00000098CN2):** góc phải chỉ có 2 nút **"Đóng ca"** và **"Đóng và in phiếu"**. Không có "Mở màn hình phụ".
- **Hộp CA HIỆN TẠI (cột trái):** chỉ có thông tin ca (mã ca, nhân viên, người mở, giờ vào ca, tiền mặt đầu ca). Không có nút phụ.
- **Menu ☰ (góc trên phải):** liệt kê đầy đủ = `CN1` · `Thu ngân` (đang chọn) · `Bật âm thanh` · `Tải lại cấu hình` · `Đặt máy chạy printcenter` · `Hiện thông tin device_id` · `Ngôn ngữ hiển thị`. → KHÔNG có "Mở màn hình phụ".
- **Kết luận:** nút không tồn tại ở mọi vị trí hợp lý.

## LỆCH-01 — 1.3.5: Không có nút "..." trên thẻ tổng hợp
- 4 thẻ (Bán hàng / Trả hàng / Phiếu thu / Phiếu chi) **hiển thị sẵn** breakdown phương thức (Tiền mặt / Chuyển khoản / Quẹt thẻ / QR tự động) ngay trên thẻ.
- Không có nút "..." để bung chi tiết → checklist mô tả thao tác cũ.

## FIND-01 — 1.6.2: Lệch nhãn "Tiền mặt" giữa modal và panel (ca SCR97)
- Modal "Chi tiết ca" → bảng **"Phương thức thanh toán"**: Tiền mặt **1.287.700** · Chuyển khoản **2.786.950** (tổng = Gross 4.074.650).
- Panel → thẻ **"Phiếu thu"**: Tiền mặt **1.202.700** · Chuyển khoản **2.786.950** (tổng 3.989.650).
- Lệch phần Tiền mặt = **85.000**. CK khớp tuyệt đối. "Tổng tiền mặt cuối ca" (modal) = "Tổng tiền mặt trong ca" (panel) = **1.202.700** → tổng quỹ đúng.
- Nguyên nhân nghi: modal nhóm theo **doanh thu bán hàng (gross) theo phương thức**, panel nhóm theo **tiền mặt thực thu vào két** (sau công nợ/VAT). Đề nghị thống nhất nhãn.

## BLOCKED — 1.5.5: Trả hàng đang phát triển
- Menu "Trả hàng" (`#/pos-shell-route/pos-returns-route`) hiển thị: **"Tính năng \"returns\" đang phát triển"**.
- → Không tạo được phiếu trả hàng để kiểm tra giảm tổng tiền mặt trong ca.

## Ghi chú thao tác (môi trường)
- Click vào widget Flutter phải dispatch PointerEvent (down→move→up) trên `flt-glass-pane`; click CDP thường KHÔNG ăn.
- Ô tìm kiếm Flutter không nhận gõ phím tự động → set `value` + dispatch `input` trên `input.flt-text-editing`.
- Dropdown lịch (Thời gian) đôi khi kẹt lớp phủ, phải bấm "Áp dụng" lại.
