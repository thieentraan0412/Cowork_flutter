# Ghi chú ảnh lỗi — HISTORY 23/06/2026 02:56

Công cụ chụp màn hình trình duyệt trong phiên này **không ghi được file ảnh ra đĩa** (giống các phiên trước). Dưới đây mô tả các khung hình lỗi đã quan sát kèm cách tái hiện.

## BUG-01 — Tab "Tại bàn" không loại đơn mang về (1.1.2, 1.1.7)
- Màn hình: tab "Tại bàn" đang chọn, "Tổng: 498 đơn" (bằng tab Tất cả), và thẻ **"Bàn mang về"** (tranvana, POS15062069CN2, 826.486) vẫn hiển thị trong danh sách.
- Tái hiện: Lịch sử → khoảng "Tháng này" → bấm tab "Tại bàn".
- Kỳ vọng: 471 đơn (loại 27 đơn mang về). Thực tế: 498 đơn, còn cả đơn mang về.

## BUG-02 — Tìm theo tên khách hàng (tranvana) → 0 đơn (1.2.2b/1.2.19)
- Màn hình: ô tìm kiếm "tranvana", danh sách rỗng "Không tìm thấy đơn hàng nào".
- Đối chứng: tìm SĐT 0321564987 → 4 đơn tranvana; tìm mã đơn → đúng.

## BUG-04 — Dropdown "Tất cả bàn" trùng tên (1.1.6)
- Màn hình: dropdown bàn liệt kê: Tất cả bàn, **ban 1, ban 2, ban 1, ban 2**, ban kiem tra ten dai, ban_qr, ban3…ban10.
- "ban 1" mục đầu → 118 đơn; "ban 1" mục hai → 34 đơn (2 bàn khác ID, trùng tên).
