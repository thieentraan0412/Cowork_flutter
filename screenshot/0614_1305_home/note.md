# Ghi chú lỗi — phiên 0614_1305_home

> ⚠️ Trong phiên này, công cụ điều khiển trình duyệt **không lưu được ảnh PNG ra thư mục dự án** (ảnh chụp do extension trả về, sandbox không ghi được ra đĩa). Vì vậy lỗi được mô tả bằng **văn bản + dữ liệu đối chứng** thay cho ảnh, giống phiên 0613.

## BUG-01 (FAIL — 1.8.4) — Chuyển bàn cho chọn cả bàn ĐANG SỬ DỤNG làm bàn đích
- **Bàn nguồn:** ban_qr (đơn comboo 10 ×2, tổng tiền hàng 1.338.820đ).
- **Các bước tái hiện:**
  1. Mở 1 bàn đang có đơn → màn hình Order.
  2. Bấm menu `...` → **Chuyển bàn** → hộp "Chọn bàn chuyển đến".
  3. Bấm chọn một bàn **đang sử dụng** (VD: **ban 2 — 2.232.141đ, 1 khách**).
- **Thực tế:** thẻ ban 2 (đang dùng) được tô đậm (chọn được), nút **"Chọn" sáng/kích hoạt** → hệ thống cho phép chuyển sang bàn đang sử dụng.
- **Kỳ vọng:** chỉ cho chọn **bàn trống** làm đích (hoặc chặn/mờ bàn đang dùng).
- **Mức độ:** Trung bình. **Lặp lại** từ phiên 0613 và 0612.
- (Đối chứng tích cực: chuyển ban_qr → **ban4 (trống)** chạy đúng — toast "Chuyển bàn thành công", ban4 nhận đủ đơn 1.338.820đ, ban_qr về trống.)

## BLOCKED (1.6.x) — Đặt món QR không tạo được đơn "Chờ xác nhận"
- **Link QR (ban10):** `https://table1.klkim.com/v2/order/qr?store_id=order_table_thientester&table=ab4393c747f4f3f38a8d904e1602863c&package_id=3&locale=vi`
- **Thực tế:** trang QR mở được (hiện menu + hộp "Tạo đơn mới"), nhưng **ngay sau khi bấm "Tạo đơn mới" thì renderer bị treo** (chụp màn hình/điều khiển time-out liên tục). Không thêm/gửi được món → phía Thu ngân **"Chờ xác nhận" vẫn = 0**.
- **Hệ quả:** không kiểm trực tiếp được 1.6.2/1.6.3/1.6.4/1.6.5/1.6.7, 1.1.11 (nút "Xác nhận" trên thẻ), 1.14.4.
- **Khuyến nghị:** kiểm lại luồng đặt món QR trên thiết bị/QR thật.

## Lưu ý nhỏ (không phải bug chặn)
- **Quẹt thẻ (1.5.5):** luồng đúng (chọn "Máy quẹt thẻ độc lập" → Gửi) nhưng trả lỗi **"Faild 400: Gửi lệnh xuống máy quẹt thẻ thất bại"** vì môi trường test không có máy quẹt thẻ vật lý. (Chuỗi lỗi có lỗi chính tả "Faild".)
- **1.14.2:** mở đơn "Chờ thanh toán" (mang về POS00002407CN2 530.000đ) bằng nút "Thanh toán" → màn Order hiện **giỏ trống** (chưa nạp lại món của đơn). Cần kiểm lại.
