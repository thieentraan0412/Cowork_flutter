# Kết quả kiểm thử — HISTORY

- Menu: history
- Ngày giờ: 24/06 05:55 (UTC)
- Người/agent thực hiện: Claude (Cowork)
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Thu ngân — CN1
- Trình duyệt: Chrome (qua tiện ích điều khiển) — Browser 1
- Thư mục ảnh lỗi: `screenshot/0624_0555_history/`

## Ghi chú chung
- Bộ lọc mặc định khi vào: tab **Tất cả**, **Trạng thái: Tất cả**, **Tất cả bàn**, **Tài khoản** (tất cả), thời gian **Hôm nay**. Có nút **Xuất Excel**.
- "Hôm nay" chỉ có **1 đơn**: bàn **ban 2**, mã **POS15062082CN2**, 10.000đ, **Chưa thanh toán**.
- Giới hạn công cụ (Flutter web): **ô tìm kiếm không nhập được text**; **menu "..." và dropdown lọc mở chập chờn** (thường không ăn click); app **đơ/giật** vài lần (screenshot time-out).

---

## 1.1 Bộ lọc loại đơn

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.1.1 | Lọc tab "Tất cả" | PASS | Hiển thị đơn ban 2 (POS15062082CN2). "Tổng: 1 đơn" |
| 1.1.2 | Lọc tab "Tại bàn" | **FAIL** | Bấm "Tại bàn" → vùng danh sách hiện **"Đã có lỗi xảy ra"** + nút "Thử lại"; bấm "Thử lại" vẫn lỗi (tái hiện). Trong khi đơn ban 2 là đơn TẠI BÀN, đáng lẽ phải hiện. (Caveat: app đang bất ổn — nên xác minh lại; nhưng "Tất cả" và "Mang về" hoạt động đúng nên nghi lỗi riêng của tab "Tại bàn") |
| 1.1.3 | Lọc tab "Mang về" | PASS | Hiển thị empty state đúng: **"Không tìm thấy đơn hàng nào"** + nút "Làm mới" (hôm nay không có đơn mang về). Khi ở tab này, dropdown "Tất cả bàn" tự ẩn (hợp lý) |
| 1.1.4 | Lọc tab "Đặt online" | KHÔNG KIỂM THỬ | Tập tab thực tế chỉ có Tất cả / Tại bàn / Mang về (không thấy tab "Đặt online" riêng trong thanh tab loại đơn) |
| 1.1.5 | Dropdown "Chọn bàn" | PASS (một phần) | Có dropdown **"Tất cả bàn"** trên thanh lọc; chưa mở chọn bàn cụ thể (dropdown mở chập chờn) |

## 1.2 Tìm kiếm & bộ lọc

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.2.1–1.2.3 | Tìm theo mã đơn / SĐT / không khớp | **BLOCKED (giới hạn công cụ)** | Ô "Tìm kiếm theo mã đơn, tên khách hàng..." có hiển thị nhưng **không nhập được text** qua điều khiển tự động (Flutter). Cần kiểm thử tay |
| 1.2.4–1.2.8 | Lọc theo Trạng thái | PASS (một phần) | Dropdown **"Trạng thái: Tất cả"** hiển thị; chưa mở chọn từng trạng thái (overlay mở chập chờn) |
| 1.2.9 | Lọc theo Tài khoản (nhân viên) | PASS (một phần) | Dropdown **"Tài khoản"** hiển thị trên thanh lọc |
| 1.2.10–1.2.14 | Khoảng ngày (Hôm nay/Hôm qua/Tuần/Tháng/Tùy chọn) | PASS (một phần) | Nút lọc thời gian **"Hôm nay"** hiển thị (mặc định); chưa mở hộp chọn mốc khác (overlay chập chờn) |
| 1.2.20 | Nút "Xuất Excel" | PASS (một phần) | Nút **"Xuất Excel"** hiển thị trên thanh lọc; chưa bấm xuất (tránh tải file) |
| 1.2.26 | Bộ lọc mặc định khi mở trang | PASS | Mặc định: Tất cả / Trạng thái Tất cả / Tất cả bàn / Tài khoản / **Hôm nay**; chỉ hiện đơn hôm nay (1 đơn) |

## 1.3 Danh sách đơn

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.3.1 | Thẻ đơn hiển thị đủ thông tin | PASS | Thẻ "ban 2": tên bàn **ban 2**, khách **Khách lẻ**, ngày giờ **24-06-2026 10:15**, mã **POS15062082CN2**, số tiền **10.000** |
| 1.3.2 | Trạng thái thanh toán hiển thị đúng | PASS | "Trạng thái: **Chưa thanh toán**" (thẻ màu xám) |
| 1.3.3 | Trạng thái HĐĐT hiển thị đúng | PASS | "Hóa đơn điện tử: **Không xác định**" (chữ cam) |
| 1.3.6 | Bộ đếm "Tổng: X đơn" | PASS | "Tổng: **1 đơn**" khớp số thẻ hiển thị |

## 1.4 Chi tiết đơn hàng

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.4.1 | Mở modal chi tiết | KHÔNG KIỂM THỬ | Bấm "..." trên thẻ đơn **không mở được menu** (overlay chập chờn, thử 2 lần không ăn). Theo checklist, chi tiết mở qua "..." → "Chi tiết" |
| 1.4.9 | Bấm thân thẻ không mở chi tiết | KHÔNG KIỂM THỬ | Chưa xác nhận được do menu "..." không mở |

## 1.5 / 1.6 Tạo đơn & công nợ — kiểm chéo

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.5.x / 1.6.x | Luồng tạo đơn / công nợ và đối chiếu Lịch sử | KHÔNG KIỂM THỬ | Phụ thuộc luồng thanh toán thật (chọn bàn → thêm món → thanh toán/nhập tiền) — không nhập được số tiền tự động & tránh tạo dữ liệu công nợ thật. Khuyến nghị kiểm thử tay |

---

## Tổng hợp
- **PASS:** 1.1.1, 1.1.3, 1.1.5(một phần), 1.2.4–1.2.8(một phần), 1.2.9(một phần), 1.2.10(một phần), 1.2.20(một phần), 1.2.26, 1.3.1, 1.3.2, 1.3.3, 1.3.6  → **~12 mục PASS (gồm một phần)**
- **FAIL: 1** — **1.1.2 Tab "Tại bàn"**: bấm vào hiện **"Đã có lỗi xảy ra"**, "Thử lại" vẫn lỗi (không tải được danh sách đơn tại bàn dù có đơn ban 2)
- **BLOCKED (giới hạn nhập liệu): ** 1.2.1–1.2.3 (ô tìm kiếm không nhập được)
- **KHÔNG KIỂM THỬ:** 1.1.4, 1.4.x (menu "..."/chi tiết không mở), 1.5.x/1.6.x (luồng tạo đơn/công nợ thật), các giá trị dropdown cụ thể (Trạng thái/Tài khoản/Khoảng ngày) — do overlay mở chập chờn + không nhập text

## Danh sách lỗi chính
1. **[1.1.2] Tab "Tại bàn" báo lỗi** — Chọn tab "Tại bàn" → "Đã có lỗi xảy ra", bấm "Thử lại" vẫn lỗi. Đơn ban 2 (tại bàn) đáng lẽ phải hiển thị. Trong khi "Tất cả" hiện đúng đơn và "Mang về" hiện empty state đúng → nghi lỗi riêng của bộ lọc "Tại bàn".
   - *Bước tái hiện:* Lịch sử → bấm tab "Tại bàn" → quan sát vùng danh sách → bấm "Thử lại".
   - *Kỳ vọng:* hiện đơn ban 2 (loại tại bàn).
   - *Thực tế:* màn hình lỗi "Đã có lỗi xảy ra".
   - *Caveat:* app Flutter đang bất ổn (đơ/giật) — nên kiểm chứng lại trên thiết bị thật trước khi kết luận chắc chắn là lỗi sản phẩm.

## Quan sát tích cực
- Thẻ đơn hiển thị đầy đủ, đúng thông tin (bàn/khách/giờ/mã/tiền/trạng thái/HĐĐT).
- "Mang về" cho empty state thân thiện đúng; dropdown bàn tự ẩn khi lọc Mang về.
- Bộ đếm "Tổng: 1 đơn" khớp; bộ lọc mặc định đúng (Hôm nay).
