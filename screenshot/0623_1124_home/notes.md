# Ảnh lỗi — HOME 0623_1124 (mô tả bằng chữ)

> Công cụ điều khiển Chrome trong phiên này KHÔNG lưu được ảnh ra đĩa (giống các phiên trước).
> Dưới đây là mô tả chi tiết từng lỗi kèm số liệu thực tế để tái hiện. Trạng thái app: Flutter web (canvas), CN1, Thu ngân, ca đang mở.

## LỖI 1 — [1.1.14] Số liệu tab không khớp tổng
- Màn hình: Trang chủ, dropdown khu = "Tất cả", Giao diện 1.
- Quan sát: thanh filter hiện **Tất cả (15)** | Bàn trống (8) | Đang sử dụng (6) | Chờ xác nhận (0) | Chờ thanh toán (0).
- Tính: 8 + 6 + 0 + 0 = **14** ≠ **15**.
- Nguyên nhân: thẻ **"BÀN MANG VỀ"** (đầu danh sách, cam đậm, 549.000đ, 2 hóa đơn, timer 307:xx) được tính vào "Tất cả" nhưng KHÔNG thuộc nhóm "Đang sử dụng".
- Đối chiếu: trong modal "Chọn bàn chuyển đến" (không có thẻ mang về) → Tất cả (14) = Đang sử dụng (7) + Bàn trống (7), khớp.

## LỖI 2 — [1.16.2] Số đếm tab trạng thái là TOÀN CỤC
- Bước: dropdown khu → chọn "khu 2".
- Quan sát: lưới chỉ hiện **2 bàn** (BAN 1, BAN 2 — đều trống) nhưng số đếm vẫn **Tất cả (15) / Bàn trống (8) / Đang sử dụng (6)** (không đổi).
- Hệ quả: người dùng dễ hiểu nhầm khu 2 có 15 bàn.

## LỖI 3 — [1.16.4] Tìm món bị giới hạn theo danh mục
- Bước: vào màn Order 1 bàn → bấm danh mục "Lẩu" → gõ "tra" vào ô "Tìm theo mã/tên món ăn...".
- Kết quả: hiển thị **"Không có món"** (vì "Lẩu" không có món chứa "tra").
- Khi về tab "Tất cả" rồi gõ "tra" → ra đầy đủ (tran chau, Trà A hỷ, Kiemtrakho...). → search không tìm toàn thực đơn khi đang ở 1 danh mục.

## LỖI 4 — [1.16.6] Ô "Giá mới" không gõ trực tiếp được
- Bước: dòng món → icon bút (Đơn giá) → modal "Thay đổi giá bán".
- Modal có: Giá gốc (read-only 20000) | Giảm giá (VNĐ/%) | Giá mới.
- Gõ thẳng "15000" vào ô "Giá mới" → Xác nhận → đơn giá KHÔNG đổi (vẫn 20.000).
- Phải nhập qua ô "Giảm giá" (VD 50%) → "Giá mới" tự tính = 10000 → Xác nhận → đơn giá đổi đúng 10.000.
- => Ô "Giá mới" chỉ là output, không phải input.

## LỖI 5 — [1.16.7] Phụ thu nhập tay không áp khi "Không áp dụng"
- Bước: dòng "Phụ thu" → icon bút → modal "Chọn phụ thu".
- Để "Phụ thu trực tiếp" = "Không áp dụng", chuyển VNĐ, gõ 10000 → modal hiện **"Tổng phụ thu: 10.000đ"**.
- Bấm "Áp dụng" → hóa đơn: **Phụ thu vẫn = 0đ**, tổng không đổi.
- Phải CHỌN chương trình ("ngay cuoi tuan"/"giam gia") rồi nhập % → mới áp (VD "ngay cuoi tuan" + 10% → phụ thu 52.000).
- => Preview "Tổng phụ thu" hiển thị nhưng không áp được → gây hiểu nhầm.

## LỖI 6 — [1.16.8] Tổng tiền cập nhật trễ (async)
- Bước: bấm + / − số lượng hoặc xóa món.
- Quan sát: cột "Thành tiền" của dòng đổi NGAY, nhưng "Tổng tiền hàng" / "Tổng tiền thanh toán" trễ ~3–7 giây mới khớp.
- Ví dụ thực tế: sau khi xóa Cơm (còn "Test điều chuyển" 500.000), tổng vẫn kẹt 520.000 nhiều giây; chỉ khớp lại sau một thao tác khác.

## LỖI 7 — [1.16.9] App Flutter đơ khi thao tác liên tục
- Sau chuỗi thao tác (mở/đóng modal, +/-, mở menu "..."), renderer ngừng phản hồi: click nút "...", "Báo bếp", click món, click "Trang chủ" đều không có tác dụng; tổng tiền kẹt.
- Khắc phục: reload trang (về URL gốc) → "Đang kiểm tra thông tin đăng nhập" → chọn lại CN1 + Thu ngân. Trong phiên này phải reload 2 lần.

## GHI CHÚ MÔI TRƯỜNG — Chưa cấu hình máy in
- Khi Chuyển bàn / Báo bếp / In tem → toast "Cảnh báo — Chưa thiết lập cấu hình máy in. Vui lòng vào Cài đặt để thiết lập máy in."
- Không phải lỗi nghiệp vụ; do môi trường test chưa gắn máy in.
