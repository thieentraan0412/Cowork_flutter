# Ghi chú lỗi — phiên 0615_0204_home

> ⚠️ Phiên này công cụ điều khiển trình duyệt **không lưu được ảnh PNG ra thư mục dự án** (extension trả ảnh inline, sandbox không ghi ra đĩa). Vì vậy lỗi được mô tả bằng **văn bản + dữ liệu đối chứng** thay cho ảnh (giống các phiên 0613/0614).

## BUG-01 (FAIL — 1.8.4) — Chuyển bàn cho chọn cả bàn ĐANG SỬ DỤNG làm bàn đích
- **Bàn nguồn:** ban6 (đơn 2 món: setmenu hoa hồng 500.000 + comboo 10 672.141; có phụ thu + giảm giá).
- **Các bước tái hiện:**
  1. Mở 1 bàn đang có đơn → màn hình Order.
  2. Menu `...` → **Chuyển bàn** → hộp "Chọn bàn chuyển đến".
  3. Bấm chọn một bàn **đang sử dụng** (VD: **ban3 — đang dùng, "1 khách"**).
- **Thực tế:** thẻ ban3 (đang dùng) được tô đậm/chọn được, nút **"Chọn" sáng/kích hoạt** → hệ thống cho phép chuyển sang bàn đang sử dụng.
- **Kỳ vọng:** chỉ cho chọn **bàn trống** làm đích (hoặc chặn/mờ bàn đang dùng).
- **Mức độ:** Trung bình. **Lặp lại** từ phiên 0612 / 0613 / 0614.
- (Đối chứng tích cực: chuyển ban1 → **ban6 (trống)** chạy đúng — toast "Chuyển bàn thành công", ban6 nhận đủ đơn 1.172.141, ban1 về trống.)

## BLOCKED-01 (1.6.x, 1.14.4) — Đặt món QR không gửi được đơn "Chờ xác nhận"
- **Link QR (ban10):** `https://table1.klkim.com/v2/order/qr?store_id=order_table_thientester&table=ab4393c747f4f3f38a8d904e1602863c&package_id=3&locale=vi`
- **Thực tế phiên này:**
  1. Trang QR **tải được** (menu danh mục, "Gọi phục vụ", "Gọi thanh toán", Bàn ban10, mã POS00002473CN2).
  2. Mở món "comboo 10" → modal tùy chọn hiện đủ → bấm "Thêm vào giỏ hàng - 669.410đ" → toast **"Thêm sản phẩm thành công"**, badge giỏ hàng = **1**.
  3. Mở giỏ hàng ("Thông tin giỏ hàng") → hiển thị **"Giỏ hàng trống"** (mâu thuẫn với badge = 1) → không có nút gửi đơn.
  4. Renderer trang QR **đôi lúc treo/timeout** khi thao tác (CDP screenshot timeout ~30s rồi tự hồi).
- **Hệ quả:** không tạo được đơn → phía Thu ngân **"Chờ xác nhận" = 0** → không kiểm trực tiếp 1.6.1–1.6.7, 1.1.11 (nút "Xác nhận" trên thẻ), 1.14.4.
- **Khuyến nghị:** kiểm lại việc giỏ hàng QR không lưu món + tình trạng renderer treo trên thiết bị/QR thật.

## LƯU Ý-02 (1.8.6) — Mất gắn khách hàng sau chuyển bàn
- Trước chuyển: đơn ban1 gắn khách "tranvana".
- Sau chuyển sang ban6: dropdown khách về **"Khách lẻ"**.
- Món / số lượng / tùy chọn / ghi chú / phụ thu / giảm giá / tổng tiền **vẫn giữ đúng** (1.172.141). Chỉ riêng khách hàng bị mất.

## LƯU Ý-03 (1.12) — Khuyến mãi không cộng dồn với giảm giá trực tiếp
- Khi đơn đã áp **giảm giá trực tiếp** ("giảm giá hằng tuần"), mục **"Khuyến mãi"** trong menu `...` bị **mờ/vô hiệu**.
- Trên đơn chưa có giảm giá, "Khuyến mãi" hoạt động bình thường (áp "KHUYEN MAI THEO SO LUONG KHACH HANG" → giảm 50.000). → Có vẻ là ràng buộc không cho cộng dồn (cần xác nhận có đúng thiết kế).

## Điểm TÍCH CỰC so với phiên trước
- **1.11.3 (Hàng tặng):** Giữ **lý do mặc định** ("Khách hàng thân thiết") rồi xác nhận → món tặng **vẫn được thêm** (0đ). Khác với lỗi LƯU Ý-03 của phiên 0614 (giữ lý do mặc định thì không thêm được) → có vẻ **đã được fix** ở bản 1.0.0+46.
