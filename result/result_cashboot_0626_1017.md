# Kết quả kiểm thử — CASHBOOT (Thu chi)

- Menu: cashboot
- Ngày giờ: 26/06 10:17
- Người/agent thực hiện: Claude
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — CN1 — vai trò Thu ngân
- Route: `pos-cashbook-route`

## Bảng kết quả

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| (load) | Trang Thu chi render | PASS* | Render trắng ban đầu, hiện sau khi resize cửa sổ (cùng lỗi paint Flutter như Lịch sử) |
| 1.1 | Bộ lọc | PASS | Mã phiếu, Chi nhánh CN1, Thời gian (Hôm nay/Hôm qua/Tuần này/Tuần trước/Tháng này/Tháng trước + khoảng ngày), Người tạo, Loại thu chi, Phân loại, Loại |
| 1.1 | Bộ lọc "Tháng này" tải dữ liệu | **FAIL** | Spinner > 13s, không tải, 4 thẻ tổng 0đ — xem ảnh |
| 1.1 | Bộ lọc "Hôm nay" tải dữ liệu | PASS | Tải ngay sau khi đổi |
| 1.2 | Tổng quan quỹ (4 thẻ) | PASS | TỒN QUỸ ĐẦU KỲ 9.042.245.176đ; TỔNG THU 21.000đ; TỔNG CHI 0đ; SỐ DƯ CUỐI CA 9.042.266.176đ (= đầu kỳ + thu − chi, đúng) |
| 1.3 | Danh sách phiếu | PASS | Cột: STT, Mã phiếu, Loại thu chi, Số tiền, Tên chi nhánh, Người nộp/nhận, Người tạo, Phân loại, PTTT, Đính kèm, Thời gian, Mô tả, Hành động |
| 1.3 | Dữ liệu phiếu | PASS | PC00001653CN2 — Thu — 21.000đ — CN1 — Admin master — Tiền mặt — 26/06 09:53 (đúng = phiếu thu của đơn POS15062088CN2 đã thanh toán) |
| 1.4 | Thêm phiếu (form) | PASS | Modal "Thêm phiếu": Mã phiếu (tự sinh), Loại thu chi*, Phân loại*, Loại nhân sự, Người nộp/nhận + nút Tạo, Số tiền*, PTTT, Đính kèm, Mô tả |
| 1.11 | Sinh mã phiếu | PASS | "Mã tăng tự động" |
| 1.11 | Định dạng số tiền | PASS | Dấu phân cách + "đ" |
| 1.12 | Kiểm thử biên — required field | PASS | Lưu rỗng bị chặn: "Số tiền" báo đỏ "Nhập số tiền" |
| 1.13 | Phương thức thanh toán | PASS (UI) | Mặc định "Tiền mặt" trong form thêm phiếu |
| 1.6 | Xuất Excel | PASS (UI) | Nút "Xuất Excel" hiển thị |
| 1.7 | Tab Công nợ | PASS (UI) | Tab "Quản lý công nợ" hiển thị |
| 1.5 | Ghi nhận các loại phiếu | PARTIAL | Form đầy đủ; chưa lưu phiếu mới thực tế (dropdown loại/phân loại Flutter mở chập chờn) |

\* PASS có điều kiện do lỗi render chung của Flutter.

## Tổng hợp
- PASS: 12
- FAIL: 1
- PARTIAL: 1

## Danh sách lỗi

1. **[1.1] Bộ lọc "Tháng này" treo — danh sách phiếu không tải**
   - Bước tái hiện: vào "Thu chi". Mặc định bộ lọc "Tháng này" (01-06 → 26-06).
   - Kỳ vọng: danh sách phiếu + thẻ tổng quan tải trong vài giây.
   - Thực tế: spinner quay > 13 giây, 4 thẻ tổng đều 0đ, bảng không tải. Đổi sang "Hôm nay" thì tải ngay (TỔNG THU 21.000đ, phiếu PC00001653CN2). → Lọc khoảng ngày rộng/tháng bị treo hoặc rất chậm.
   - Ảnh: `screenshot/0626_1017_cashboot/error_month_filter_hang.png`

## Ghi chú thêm
- Tính toán quỹ đúng: TỒN QUỸ ĐẦU KỲ + TỔNG THU − TỔNG CHI = SỐ DƯ CUỐI CA.
- Liên kết nghiệp vụ đúng: thanh toán tiền mặt ở Trang chủ → sinh Phiếu thu (PC…) đúng số tiền trong Thu chi và Điều phối ca.
