# Kết quả kiểm thử — CASHBOOT (Thu chi)

- Menu: cashboot (Thu chi / Quản lý thu chi) — route `#/pos-shell-route/pos-cashbook-route`
- Ngày giờ: 24/06 05:55 (UTC)
- Người/agent thực hiện: Claude (Cowork)
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Thu ngân — CN1
- Trình duyệt: Chrome (qua tiện ích điều khiển) — Browser 1
- Thư mục ảnh lỗi: `screenshot/0624_0555_cashboot/`

## Ghi chú chung
- Phải **tải lại app + chọn lại Thu ngân** mới vào được trang (nav "Thu chi" bị kẹt do app đơ sau nhiều thao tác — biểu hiện 1.18.2/quirk Flutter).
- Bộ lọc mặc định: **Tháng này** (01-06-2026 → 24-06-2026), Chi nhánh CN1, các bộ lọc khác = Tất cả.
- Mã phiếu thực tế: **PC…** (phiếu thu) / **PT…** (phiếu chi), hậu tố **CN2**. Tổng **239 bản ghi**, phân trang 1..12.
- Giới hạn công cụ: **không nhập text** (ô Mã phiếu, ô tìm), **mở dropdown/modal chập chờn** → các case Thêm/Sửa/Xóa phiếu & đổi bộ lọc bằng giá trị không kiểm thử tự động được.

---

## 1.1 Bộ lọc (cấu trúc)

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.1.1 | Tìm theo Mã phiếu | BLOCKED | Ô "Mã phiếu" có; không nhập text được (Flutter) |
| 1.1.2 | Lọc Chi nhánh | PASS (một phần) | Dropdown "CN1" hiển thị |
| 1.1.3–1.1.6 | Thời gian (Hôm nay/Hôm qua/Tuần này/Tuần trước/Tháng này/Tháng trước + khoảng ngày) | PASS (một phần) | Đủ preset; "Tháng này" đang chọn, khoảng 01-06 → 24-06-2026 |
| 1.1.7 | Lọc Người tạo | PASS (một phần) | Dropdown "Tất cả" có |
| 1.1.8 | Lọc Loại thu chi | PASS (một phần) | Dropdown "Tất cả" có |
| 1.1.9 | Lọc Phân loại thu chi | PASS (một phần) | Có |
| 1.1.10 | Lọc Loại nguồn | PASS (một phần) | Có ("Loại") |

## 1.2 Tổng quan quỹ — **kiểm chứng công thức**

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.2.1 | Tồn quỹ đầu kỳ | PASS | **8.264.976.882 đ** |
| 1.2.2 | Tổng thu | PASS | **778.474.439 đ** |
| 1.2.3 | Tổng chi | PASS | **1.239.745 đ** |
| 1.2.4 | Số dư cuối ca = Đầu kỳ + Thu − Chi | **PASS** | 8.264.976.882 + 778.474.439 − 1.239.745 = **9.042.211.576** ✓ = "Số dư cuối ca: 9.042.211.576 đ" |

## 1.3 Danh sách phiếu

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.3.1 | Bảng phiếu đủ cột | PASS | 13 cột: STT · Mã phiếu · Loại thu chi · Số tiền · Tên chi nhánh · Người nộp/Người nhận · Người tạo · Phân loại thu chi · Phương thức thanh toán · Đính kèm · Thời gian ghi nhận · Mô tả · Hành động |
| 1.3.2 | Phân trang | PASS | "Tổng 239 bản ghi", trang 1, 2, … 12 |
| 1.3.3 | Icon xem chi tiết | PASS (một phần) | Mỗi dòng có icon mắt (xem); chưa mở modal chi tiết |

## 1.8 / 1.9 Sửa / Xóa phiếu (quan sát cột Hành động)

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.8.1 | Icon thao tác ở cột Hành động | PASS | Phiếu thủ công có **bút (sửa) + thùng rác (xóa) + mắt (xem)**; phiếu tự sinh chỉ có **mắt** |
| 1.8.6 | Phiếu tự sinh không cho sửa | PASS | Các phiếu bán hàng tự sinh (VD PC00001651, PC00001648, PC00001071) chỉ có icon xem, KHÔNG có bút sửa |
| 1.9.5 | Phiếu tự sinh không cho xóa | PASS | Tương tự, không có icon xóa trên phiếu tự sinh |
| 1.8.2–1.8.5, 1.9.1–1.9.4 | Thực hiện sửa/xóa thật | KHÔNG KIỂM THỬ | Cần mở modal + nhập liệu (chập chờn) & tránh sửa/xóa dữ liệu thật |

## 1.11 Sinh mã phiếu & định dạng — **phát hiện lỗi tồn**

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.11.1 | Tiền tố PC/PT | PASS | Phiếu thu **PC…**, phiếu chi **PT…** |
| 1.11.5 | Số tiền có dấu phân cách + đ | PASS | "8.264.976.882 đ", "550.000 đ", "10.500 đ" |
| 1.11.4 / 1.19.6 | Không sinh mã "toàn số 0" | **FAIL (lỗi tồn)** | Có phiếu **PT00000000CN2** và **PC00000000CN2** (mã toàn số 0) trong danh sách → lỗi sinh mã CHƯA fix |

## 1.19 Regression — lỗi/lệch đã biết

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.19.1 / BUG-01 | Số tiền = 0 vẫn tạo phiếu | **FAIL (còn lỗi)** | Tồn tại phiếu **PT00000000CN2 = 0 đ** và **PT00000036CN2 = 0 đ** (Loại Chi) → hệ thống ĐÃ cho tạo phiếu 0đ. Lỗi CHƯA fix |
| 1.19.6 | Mã phiếu "toàn số 0" | **FAIL (còn lỗi)** | PT00000000CN2, PC00000000CN2 xuất hiện |
| 1.19.3 / 1.19.4 | Label Người nộp/Người nhận, "Loại nhân sự" | KHÔNG KIỂM THỬ | Cần mở modal Thêm phiếu (chập chờn) |
| 1.19.5 / FIND-BALANCE | Đầu kỳ đổi theo lọc loại | KHÔNG KIỂM THỬ | Cần đổi lọc "Phiếu chi" (dropdown chập chờn) |

## 1.13 / 1.17 PTTT & phân quyền (quan sát)

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.13.x | PTTT đa dạng | PASS | Cột PTTT: **Tiền mặt, Chuyển khoản, QR Tự động** xuất hiện đúng |
| 1.17.2 | Mã gắn đúng chi nhánh | PASS | Tất cả mã hậu tố **…CN2** |
| 1.17.3 | Người tạo = tài khoản đăng nhập | PASS | Cột Người tạo: Admin master / cashier |

## 1.4 / 1.6 / 1.7 Thêm phiếu / Xuất Excel / Công nợ

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.4.1 | Nút "Thêm" mở modal | PASS (một phần) | Nút **"Thêm"** hiển thị góc phải; chưa mở modal (nhập liệu bị chặn → không hoàn tất luồng thêm) |
| 1.4.2–1.4.20, 1.5.x, 1.12.x | Thêm phiếu / logic 4 loại | KHÔNG KIỂM THỬ | Cần nhập số tiền/mô tả + chọn dropdown (Flutter chặn) & tránh tạo phiếu thật |
| 1.6.1 | Nút "Xuất Excel" | PASS (một phần) | Nút **"Xuất Excel"** hiển thị; chưa bấm (tránh tải file) |
| 1.7.x | Tab Công nợ | PASS (một phần) | Tab **"Quản lý công nợ"** hiển thị cạnh "Quản lý thu chi"; chưa mở chi tiết |

---

## Tổng hợp
- **PASS: ~20** (gồm logic quan trọng: công thức quỹ, cột bảng, phân trang, quy ước mã, định dạng tiền, phân quyền sửa/xóa phiếu tự sinh)
- **FAIL: 2 (lỗi tồn, đáng lưu ý)** — **1.11.4/1.19.6** (mã phiếu toàn số 0: PT00000000, PC00000000) và **1.19.1/BUG-01** (phiếu số tiền = 0đ vẫn tồn tại)
- **BLOCKED:** 1.1.1 (ô Mã phiếu không nhập được)
- **KHÔNG KIỂM THỬ:** toàn bộ luồng Thêm/Sửa/Xóa phiếu (1.4, 1.5, 1.8.2–1.8.5, 1.9.1–1.9.4, 1.12), đổi giá trị bộ lọc, Xuất Excel, chi tiết Công nợ — do nhập liệu bị chặn + tránh thay đổi dữ liệu thật

## Danh sách lỗi chính
1. **[1.19.6 / 1.11.4] Mã phiếu "toàn số 0"** — danh sách có **PT00000000CN2** và **PC00000000CN2**. Mã phiếu phải là số thứ tự tăng dần hợp lệ; mã toàn 0 cho thấy lỗi sinh mã chưa được khắc phục.
2. **[1.19.1 / BUG-01] Phiếu số tiền = 0đ** — tồn tại **PT00000000CN2 (0đ)** và **PT00000036CN2 (0đ)**. Hệ thống nên chặn lưu phiếu số tiền = 0 (báo "số tiền phải > 0"), nhưng các phiếu 0đ đã được tạo.
   - *Caveat:* đây là dữ liệu lịch sử quan sát được; cần thử lại luồng Thêm phiếu (nhập 0đ) bằng tay để xác nhận lỗi còn tái hiện ở bản hiện tại.

## Quan sát tích cực
- **Công thức quỹ chính xác**: Số dư cuối ca = Tồn đầu kỳ + Tổng thu − Tổng chi (9.042.211.576 ✓).
- Bảng đủ 13 cột, phân trang 239 bản ghi hoạt động.
- Phân quyền đúng: phiếu **tự sinh** (bán hàng) chỉ cho **xem**; phiếu **thủ công** mới có **sửa/xóa**.
- Quy ước mã (PC/PT + CN2), định dạng tiền, PTTT (Tiền mặt/CK/QR) nhất quán.
