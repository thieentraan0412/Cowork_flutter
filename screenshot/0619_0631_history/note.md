# Ghi chú lỗi & quan sát — Menu HISTORY (phiên 0619_0631)

> Công cụ chụp ảnh **không xuất được file PNG ra đĩa** trong phiên này (giống các phiên trước).
> Các lỗi được mô tả bằng văn bản kèm dữ liệu đối chứng để tái hiện. Tham chiếu chi tiết: `result/result_history_0619_0631.md`.

Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin`, vai trò **Thu ngân**, chi nhánh **CN1**, app **1.0.0+58**, Chrome.

Dữ liệu hôm nay (19/06/2026): **10 đơn** = 1 Đã thanh toán (mang về `POS15062069CN2`, khách `tranvana`, 826.486) + 9 Đã hủy (ban1/ban2, khách lẻ).

---

## BUG-01 (NEW) — Tab "Tại bàn" không loại đơn mang về
Bấm tab **"Tại bàn"** → vẫn ra **10 đơn**, gồm cả đơn "Bàn mang về" (`POS15062069CN2`). Đúng phải là 9 đơn. Tab "Mang về" lọc đúng (1 đơn) ⇒ riêng "Tại bàn" lỗi.

## BUG-02 (NEW) — Tìm kiếm theo TÊN khách hàng không hoạt động
- Tìm `tranvana` (tên khách của đơn 069) → **0 đơn** (SAI).
- Tìm `0321564987` (SĐT của chính đơn đó) → **1 đơn** (đúng).
- Tìm `POS15062068CN2` (mã đơn) → **1 đơn** (đúng).
⇒ Search theo **mã đơn** và **SĐT** OK, nhưng **tên khách hàng** không chạy (dù placeholder ghi "Tìm kiếm theo mã đơn, tên khách hàng").

## BUG-03 (NẶNG) — Bộ lọc khoảng NHIỀU NGÀY chỉ trả đơn "Đã thanh toán", bỏ sót đơn hủy
- "Hôm nay" (1 ngày, 19/06) → **10 đơn** (đủ, gồm 9 đơn hủy). ĐÚNG.
- "Hôm qua" (1 ngày, 18/06) → **rỗng** (không có đơn). ĐÚNG.
- "Tuần này" (15–21/06, chứa hôm nay) → **1 đơn** (chỉ đơn đã thanh toán). SAI — phải ≥ 10.
- "Tháng này" (01–30/06) → **4 đơn, toàn bộ Đã thanh toán** (12/06, 14/06, 19/06). SAI — bỏ sót 9 đơn hủy của hôm nay.
⇒ Khoảng **nhiều ngày** lọc rớt đơn **Đã hủy / Chưa thanh toán**; chỉ mốc **1 ngày** trả đầy đủ.
(So với 0616: trước báo khoảng nhiều ngày trả về RỖNG; nay trả paid-only — vẫn lỗi, biểu hiện đổi.)

## BUG-04 — Dropdown "Tất cả bàn" có bàn trùng tên
Danh sách bàn: Tất cả bàn, **ban 1, ban 2, ban 1, ban 2**, ban kiem tra ten dai, ban_qr, ban3, ban4, …, ban10.
⇒ "ban 1" và "ban 2" lặp 2 lần (trùng tên, khác ID).

## FIND-05 (UX) — Dropdown bộ lọc chập chờn
Dropdown "Trạng thái"/"Chọn bàn": thường phải bấm 2 lần mới chọn được; để lại lớp phủ "ma" che danh sách sau khi chọn.

## FIND-06 (UX) — Popup lịch không tự đóng
Sau "Áp dụng"/"Hủy", popup lịch đôi khi không đóng; phải bấm ra ngoài hoặc Escape.

---

## Quan sát hữu ích (không phải lỗi)
- Tập trạng thái nay **đủ & khớp checklist**: Đã thanh toán / Chưa thanh toán / Đã hủy / Đã xử lý trả hàng / Công nợ (khác hẳn 0616).
- Lọc theo bàn cụ thể "ban 1" phiên này ra **đúng 6 đơn** (không tái hiện lỗi rỗng 0616).
- Thẻ đơn hiển thị **tên khách hàng** (không phải tài khoản nhân viên) ở dòng đầu; số tiền thẻ = **Thực thu** (gồm VAT).
- Màu thẻ: Đã thanh toán = xanh lá; Đã hủy = đỏ.
- Chi tiết mở qua **menu "..." → "Chi tiết"**; tiêu đề **"Chi tiết hóa đơn"**; đóng bằng **icon X** (không có nút "Đóng").
- Tính toán chi tiết hóa đơn chính xác: Tổng tiền hàng 739.510 = 10.000 + 729.510; Thực thu 826.486 = 739.510 + 50.000 (phụ thu) + 36.976 (VAT ≈5%).
- Bộ lọc có thêm mốc **"Quý này", "Năm nay"** ngoài checklist; tìm kiếm áp dụng khi nhấn **Enter**.
