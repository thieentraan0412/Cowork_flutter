# Ghi chú lỗi & quan sát — phiên 0615_1600_home (bản 1.0.0+50)

> ⚠️ Công cụ điều khiển trình duyệt **không lưu được ảnh PNG ra thư mục dự án** → mô tả bằng văn bản + dữ liệu đối chứng.

## BUG-01 (FAIL — 1.8.4) — VẪN CHƯA FIX ở 1.0.0+50
- **Bàn nguồn:** BAN 2 (đơn QR `PO015062032CN2`, 2 món, 610.000đ).
- **Các bước:** Màn Order → menu `...` → **Chuyển bàn** → hộp "Chọn bàn chuyển đến" → bấm chọn **ban3** (đang sử dụng, nhãn "1 khách").
- **Thực tế:** ban3 (đang dùng) được tô đậm/chọn được, nút **"Chọn" sáng** → cho phép chuyển sang bàn đang dùng.
- **Kỳ vọng:** chỉ cho chọn bàn trống.
- **Lịch sử:** lặp lại ở 0612 / 0613 / 0614 / 0615_0204 / **0615_1600**. Chưa được khắc phục.

## CẢI THIỆN (BLOCKED → PASS) — Mục 1.6 & 1.14.4
- Phiên này môi trường có sẵn **1 đơn "Chờ xác nhận"** trên BAN 2 (`PO015062032CN2`, 560.000đ, đặt 15/06 08:16, gồm: cf sua new x2 + Test Kho 8 x1).
- Luồng đã chạy thành công:
  1. Tab "Chờ xác nhận (1)" → hiện đúng BAN 2 (1.6.1).
  2. Bấm thẻ → hộp "Chọn đơn hàng" (có tab lọc) → bấm "Xác nhận" trên đơn → hộp "Chi tiết" (có nút **Hủy đơn** đỏ + **Xác nhận**).
  3. Bấm "Xác nhận" → toast **"Cập nhật thành công"**; "Chờ xác nhận" 1→0, "Đang sử dụng" 3→4 (1.6.2/1.6.3/1.6.7).
  4. Báo bếp → "Gửi bếp thành công" (1.7.1).
  5. Thanh toán tiền mặt 610.000 → **"Thanh toán thành công"**, bàn về trống (1.5.3, 1.14.4).
- → Mục 1.6.x và 1.14.4 (BLOCKED ở phiên 0615_0204) nay **PASS**.

## LƯU Ý-A (vệ sinh dữ liệu) — BAN3 có 23 hóa đơn 0đ
- Mở "Chọn đơn hàng" của BAN3 → tab "Đang sử dụng (23)": hàng loạt đơn `POS00000402CN2 … POS00000414CN2…`, tất cả **0đ**, ngày **16/04/2026**.
- Không phải lỗi luồng Home, nhưng là rác dữ liệu tồn đọng — nên dọn để trạng thái bàn sạch và để kiểm Gộp/Tách bàn thuận tiện.

## Phạm vi & phương pháp
- Phiên hồi quy trên 1.0.0+50. Đã **chạy lại trực tiếp**: đăng nhập, 1.1 (bản đồ bàn/bộ lọc/thẻ/tổng tiền), **toàn bộ luồng 1.6 xác nhận đơn**, 1.7.1 báo bếp, 1.5.3 thanh toán, **1.14.4**, 1.8.1/1.8.4/1.8.9 (chuyển bàn + bug).
- Các mục hành vi không đổi so với phiên 0615_0204 (đã kiểm rất chi tiết) được **giữ nguyên kết quả**.
- **Thuế theo cả bill (1.4.9/1.4.10):** không chỉnh cấu hình thuế ở trang admin để tránh ảnh hưởng môi trường dùng chung — cần xác nhận của người dùng nếu muốn bật & kiểm.
