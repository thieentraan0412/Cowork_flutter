# Ghi chú ảnh lỗi — HISTORY 0624_0103

> Công cụ chụp màn hình của trình duyệt trong phiên này **không lưu được file ảnh ra đĩa**
> (`save_to_disk` báo "screenshots are not persisted to disk in this session" — giống các phiên trước).
> Do đó các lỗi được mô tả bằng văn bản + số liệu đối chứng + các bước tái hiện dưới đây.

## BUG-01 — Tab "Tại bàn" KHÔNG loại đơn mang về
- Màn hình: Lịch sử → khoảng "Tháng này" (01/06–24/06) → bấm tab **Tại bàn**.
- Quan sát: bộ đếm **Tổng: 499 đơn** (đúng bằng tab "Tất cả" = 499) và trong danh sách vẫn xuất hiện thẻ **"Bàn mang về"** (đơn `POS15062069CN2`, khách tranvana, 19-06 11:56).
- Kỳ vọng: Tại bàn = 499 − 27 (mang về) = **472 đơn**, KHÔNG có thẻ "Bàn mang về".
- Đối chứng: Tất cả=499, Mang về=27, Tại bàn=499 (sai, đúng phải 472).

## BUG-04 — Dropdown "Tất cả bàn" có bàn TRÙNG TÊN
- Màn hình: mở dropdown "Tất cả bàn".
- Danh sách thực tế: `Tất cả bàn, ban 1, ban 2, ban 1, ban 2, ban kiem tra ten dai, ban_qr, ban3, ban4, ban5, ban6, ban7, ban8, ban9, ban10`.
- "ban 1" và "ban 2" mỗi tên xuất hiện **2 lần** (trùng tên, khác ID). Chọn "ban 1" (mục đầu) → 118 đơn.

## BUG-02 — Tìm theo tên khách hàng (KHÔNG kiểm thử lại được phiên này)
- Ô tìm kiếm Flutter (CanvasKit) không nhận input qua công cụ tự động trong phiên này
  (đã thử: set value + dispatch input event, JS focus + gõ phím CDP, native click + type — đều không vào).
- Các phiên trước ghi nhận: nhập "tranvana" → 0 đơn dù khách có đơn (tìm theo SĐT ra đúng). Cần kiểm thử thủ công.
