# Ghi chú ảnh lỗi — Coordination (Điều phối ca) — 0623_1540

> Công cụ chụp màn hình **không lưu được file ảnh ra đĩa** trong phiên này (đã xác nhận: `save_to_disk` không có tác dụng — giống các phiên History/Cashboot/Coordination trước). Dưới đây mô tả bằng văn bản + số liệu đối chứng để tái hiện từng lỗi/độ lệch.

> Phiên bản app khi test: **1.0.0+67** (các phiên trước là +65). Route: `#/pos-shell-route/pos-shift-route`.

## FAIL-01 — 1.1.8: Không có nút "Mở màn hình phụ"
- **Panel ca đang mở (SCR00000098CN2):** góc phải chỉ có **"Đóng ca"** + **"Đóng và in phiếu"**. Không có "Mở màn hình phụ".
- **Hộp CA HIỆN TẠI (cột trái):** chỉ thông tin ca (mã ca, nhân viên, người mở, giờ vào ca, tiền mặt đầu ca). Không có nút phụ.
- **Menu ☰ (góc trên phải):** liệt kê đầy đủ = `CN1` · `Thu ngân` (đang chọn, có ✓) · `Bật âm thanh` · `Tải lại cấu hình` · `Đặt máy chạy printcenter` · `Hiện thông tin device_id` · `Ngôn ngữ hiển thị` (cờ VN/EN/KO). → **KHÔNG** có "Mở màn hình phụ".
- **Kết luận:** nút không tồn tại ở mọi vị trí hợp lý. Trùng FAIL các phiên 0617 & 0623_0124.

## LỆCH-01 — 1.3.5: Không có nút "..." trên 4 thẻ tổng hợp
- 4 thẻ (Bán hàng / Trả hàng / Phiếu thu / Phiếu chi) **hiển thị sẵn** breakdown phương thức (Tiền mặt / Chuyển khoản / Quẹt thẻ / QR tự động) ngay trên thẻ.
- Không có nút "..." để bung chi tiết → checklist mô tả thao tác cũ. Vẫn đạt mục tiêu xem chi tiết.

## FIND-01 — 1.6.2: Lệch nhãn "Tiền mặt" giữa modal Chi tiết ca và panel (ca SCR97)
- Modal "Chi tiết ca" → bảng **"Phương thức thanh toán"**: Tiền mặt **1.287.700** · Chuyển khoản **2.786.950** (tổng = Gross bán hàng 4.074.650).
- Panel → thẻ **"Phiếu thu"**: Tiền mặt **1.202.700** · Chuyển khoản **2.786.950** (tổng 3.989.650).
- Lệch phần Tiền mặt = **85.000**. CK khớp tuyệt đối. "Tổng tiền mặt cuối ca" (modal) = "Tổng tiền mặt trong ca" (panel) = **1.202.700** → **tổng quỹ vẫn đúng**.
- Nguyên nhân nghi: modal nhóm theo **doanh thu bán hàng (gross) theo phương thức**; panel nhóm theo **tiền mặt thực thu vào két** (sau công nợ/VAT). Đề nghị thống nhất nhãn. Trùng FIND phiên 0623_0124.

## FIND-02 — Nhãn chi nhánh CN1 vs hậu tố mã CN2
- Menu ☰ và role-picker hiển thị chi nhánh **"CN1"**; cột "Tên chi nhánh" trong Thu chi cũng ghi **CN1**.
- Nhưng **mọi mã** (ca SCR…CN2, phiếu thu PC…CN2, phiếu chi PT…CN2, bán hàng POS…CN2) đều mang hậu tố **CN2**.
- Nhất quán giữa Điều phối ca và Thu chi (không mâu thuẫn nội bộ), nhưng nhãn hiển thị (CN1) ≠ hậu tố mã (CN2). Đề nghị làm rõ quy ước (CN1 = tên hiển thị, CN2 = mã chi nhánh?).

## BLOCKED-TECH — 1.12.2/1.12.3/1.12.4 (tăng realtime khi tạo đơn mới) & tạo phiếu thu/chi/trả mới
- **Hạn chế kỹ thuật của môi trường tự động (Flutter canvas):** sau khi điều hướng giữa các menu trên thanh nav, các thao tác click trong trang (chọn bàn ở Trang chủ, mở đơn) **không phản hồi** ổn định. Thanh nav chỉ bấm được **ngay sau khi reload trang** (phải reload trước mỗi lần chuyển menu).
- → Không tạo/thanh toán được **đơn bán mới** ở Trang chủ để xem bộ đếm tăng +1 trực tiếp.
- **Lưu ý:** lõi đồng bộ realtime vẫn được chứng minh gián tiếp (xem 1.12.1, 1.13) — đơn POS bán ở Home đã hiện trong giao dịch ca; phiếu PC/PT khớp tuyệt đối với menu Thu chi; reload giữ số liệu nhất quán. Ngoài ra thấy 1 đơn **chưa thanh toán POS15062081CN2 (10.000đ, bàn "ban9", tạo 23/06 11:53)** đang luân chuyển trong hệ thống.

## BLOCKED-FEATURE — 1.5.5: Trả hàng (returns)
- Không tạo được phiếu trả hàng tiền mặt để kiểm giảm tổng (cần vào menu Trả hàng — cùng hạn chế điều hướng + tính năng returns nhiều khả năng đang phát triển như phiên trước).

## HÀNH ĐỘNG THAY ĐỔI DỮ LIỆU ĐÃ THỰC HIỆN (được người dùng cho phép "Thực thi toàn bộ")
- **ĐÓNG CA THẬT** ca đang mở **SCR00000098CN2**: nhập "Tiền mặt bàn giao thực tế" = **1.462.986đ** (khớp "Tiền mặt trong ca" → chênh lệch 0), ghi chú "Test QA dong ca - Claude", bấm **ĐÓNG CA** → toast **"Đóng ca thành công"**.
- Sau đóng: header ca = **"Đã đóng"**, **Giờ đóng ca 2026-06-23 15:39:30**; hộp CA HIỆN TẠI biến mất → thay bằng nút **"+ MỞ CA"**; panel chỉ còn **"In phiếu ca"** (mất "Đóng ca"/"Đóng và in phiếu").
- ⚠️ **Store hiện KHÔNG còn ca mở.** Người dùng có thể bấm **"Mở ca"** để mở ca mới khi cần.
