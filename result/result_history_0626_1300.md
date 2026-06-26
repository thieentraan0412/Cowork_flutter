# Kết quả kiểm thử — HISTORY (Lịch sử)

- Menu: history
- Ngày giờ: 26/06/2026 11:49–13:00 (+07)
- Người/agent thực hiện: Claude (Cowork) — trình duyệt Chrome
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Cashier (Thu ngân) — CN1
- Phạm vi: chạy toàn bộ `Checklist/checklist_history.md` (mục 1.1 → 1.6). Có **tạo mới 1 đơn công nợ** từ Trang chủ để kiểm luồng 1.5/1.6.
- Dữ liệu ngày 26/06 (5 đơn):
  - **POS15062092CN2** — ban8 — KH **tranvana** — 10.500 — **Công nợ** (đơn tự tạo trong phiên: tổng 10.500, đưa 5.000, nợ 5.500)
  - POS15062091CN2 — ban8 — 10.500 — Đã thanh toán
  - POS15062090CN2 — ban 2 — 39.000 — Chưa thanh toán
  - POS15062089CN2 — ban8 — 20.000 — Đã hủy
  - POS15062088CN2 — ban8 — 21.000 — Đã thanh toán

## Bảng kết quả

### 1.1 Bộ lọc loại đơn
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.1.1 | PASS | Tab "Tất cả" hiện đủ 5 đơn mọi loại/trạng thái |
| 1.1.2 | PASS | Tab "Tại bàn" hiện 4 đơn (tất cả đều đơn tại bàn) |
| 1.1.3 | PASS | Tab "Mang về" rỗng (hôm nay không có đơn mang về) — dropdown chọn bàn ẩn ở tab này |
| 1.1.4 | **FAIL/khác checklist** | KHÔNG có tab "Đặt online" — chỉ 3 tab: Tất cả / Tại bàn / Mang về |
| 1.1.5 | PASS (1 phần) | Chọn "ban8" → đúng 3 đơn. Nhưng chọn "ban 2" → rỗng dù có đơn ban 2 (xem 1.1.6) |
| 1.1.6 | **FAIL** | "ban 1" và "ban 2" mỗi bàn **lặp 2 lần** trong dropdown; chọn "ban 2" (cả 2 mục) ra **rỗng** dù có đơn ban 2. Ảnh/mô tả: `screenshot/0626_1300_history/note.md` (Lỗi 1) |
| 1.1.7 | PASS | Tại bàn=4, Mang về=0 → nhất quán, tab Tại bàn không lẫn đơn mang về |

### 1.2 Tìm kiếm & bộ lọc
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.2.1 | PASS | Gõ mã `POS15062088CN2` + **Enter** → đúng 1 đơn (search cần nhấn Enter mới lọc) |
| 1.2.2 | PASS | Gõ SĐT `0321564987` + Enter → ra đúng đơn của khách tranvana |
| 1.2.3 | PASS | Gõ "xxxx9999" → "Không tìm thấy đơn hàng nào" |
| 1.2.4 | PASS | "Đã thanh toán" → 2 đơn (thẻ xanh) |
| 1.2.5 | PASS | "Chưa thanh toán" → 1 đơn (ban 2) |
| 1.2.6 | PASS | "Đã hủy" → 1 đơn (thẻ đỏ) |
| 1.2.7 | PASS | "Đã xử lý trả hàng" → rỗng (hôm nay không có) |
| 1.2.8 | PASS | "Công nợ" → 1 đơn (POS15062092CN2) |
| 1.2.9 | PASS | Lọc Tài khoản = "Admin master" → 4 đơn do tài khoản đó tạo |
| 1.2.10 | PASS | Mặc định "Hôm nay" → các đơn 26/06 |
| 1.2.11 | PASS | "Hôm qua" (25/06) → 5 đơn, đều ngày 25/06 |
| 1.2.12 | PASS | "Tuần này" (22–26/06) → 11 đơn |
| 1.2.13 | PASS | "Tháng này" (01–26/06) → 509 đơn |
| 1.2.14 | PASS | "Tùy chọn" chọn 10–20/02 trên lịch → nhãn đổi "10/02/2026 - 20/02/2026", lọc đúng khoảng |
| 1.2.15 | PASS | Kết hợp Tại bàn + Đã thanh toán + Hôm nay → đúng 2 đơn thỏa tất cả điều kiện |
| 1.2.16 | PASS | Bấm ngày sau trước, ngày trước sau → lịch **tự sắp xếp** thành khoảng hợp lệ (không tạo khoảng âm) |
| 1.2.17 | PASS | Tuần=11, Tháng=509, Quý=2.543, Năm=2.581 → khoảng nhiều ngày cộng dồn đúng (≥ ngày con) |
| 1.2.18 | PASS | Tập trạng thái thực tế = 6 mục (xem 1.2.27), khác note checklist (không có "Đang xử lý/Hoàn thành/Chờ thanh toán") |
| 1.2.19 | **FAIL** | Gõ tên KH "tranvana" → **rỗng** dù đơn POS15062092CN2 gán đúng KH tranvana (tái hiện lỗi 0623). Ảnh: `screenshot/0626_1300_history/note.md` (Lỗi 2) |
| 1.2.20 | PASS | "Xuất Excel" → hiện "Đã xuất file, đang tải xuống trình duyệt" (file tải về trình duyệt) |
| 1.2.21 | PASS | "Quý này" (01/04–26/06) → 2.543 đơn |
| 1.2.22 | PASS | "Năm nay" (01/01–26/06) → 2.581 đơn |
| 1.2.23 | PASS | Ngày 27–30/06 (tương lai) bị làm mờ, không chọn được; chỉ chọn ≤ 26/06 |
| 1.2.24 | PASS | Chọn "Tháng này" rồi bấm "Hủy" → giữ nguyên "Hôm nay", không áp dụng |
| 1.2.25 | PASS | Bấm "Áp dụng" → danh sách + nhãn nút cập nhật theo mốc đã chọn |
| 1.2.26 | PASS | Mặc định: Tất cả / Trạng thái Tất cả / Tất cả bàn / Hôm nay |
| 1.2.27 | PASS | Dropdown trạng thái đúng 6 mục: Tất cả / Đã thanh toán / Chưa thanh toán / Đã hủy / Đã xử lý trả hàng / Công nợ |

### 1.3 Danh sách đơn
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.3.1 | PASS (lưu ý) | Thẻ hiện: tên bàn, **khách hàng** (Khách lẻ / tên thành viên), ngày giờ, mã POS, số tiền, trạng thái, HĐĐT. *Thẻ hiển thị KHÁCH HÀNG, không hiển thị tài khoản nhân viên (nhân viên nằm trong chi tiết)* |
| 1.3.2 | PASS | Chưa TT = thẻ xám; Đã TT = thẻ xanh; **Công nợ = thẻ cam**; Đã hủy = thẻ đỏ |
| 1.3.3 | PASS | HĐĐT: "Chờ ký" (đơn đã TT/công nợ) / "Không xác định" (chưa TT, đã hủy) |
| 1.3.4 | PASS | Màu thẻ phân biệt đúng theo trạng thái (xám/xanh/cam/đỏ) |
| 1.3.5 | PASS | Số tiền thẻ (10.500) = "Tổng tiền thanh toán" trong chi tiết |
| 1.3.6 | PASS | "Tổng: X đơn" khớp số thẻ và cập nhật khi đổi bộ lọc (4→5→1…) |

### 1.4 Chi tiết đơn hàng
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.4.1 | PASS | "..." → "Chi tiết" mở modal "Chi tiết hóa đơn", đúng mã POS15062091CN2 |
| 1.4.2 | PASS | Ngày tạo 26/06/2026 11:34, Người tạo Admin master, Bàn ban8, Khách lẻ |
| 1.4.3 | PASS | Món: tran chau (10.000 × 1 = 10.000) |
| 1.4.4 | PASS | Tổng tiền hàng 10.000 = Σ thành tiền |
| 1.4.5 | PASS | Phụ thu 0 / Giảm giá 0 / Tích điểm 0 / VAT 500 |
| 1.4.6 | PASS | Tổng TT 10.500 = 10.000 + 0 − 0 − 0 + 500 |
| 1.4.7 | PASS | Hình thức TT: Tiền mặt |
| 1.4.8 | PASS | "Đóng" → quay về danh sách, giữ bộ lọc |
| 1.4.9 | PASS | Bấm thân thẻ KHÔNG mở modal; chỉ mở qua "..." → "Chi tiết" |
| 1.4.10 | PASS | Menu đơn CHƯA TT: chỉ có "Chi tiết" |
| 1.4.11 | PASS | "Số khách": 1 |
| 1.4.12 | PASS | Có ô "Ghi chú" (rỗng khi đơn không ghi chú) |
| 1.4.13 | PASS | Tiêu đề "Chi tiết hóa đơn" + badge trạng thái khớp thẻ |
| 1.4.14 | **FAIL/khác checklist** | Menu đơn ĐÃ TT chỉ **4 mục** (Chi tiết / In lại bill / In lại tem / In lại HĐĐT) — **thiếu "Trả hàng"** so với 0624. Ảnh: `screenshot/0626_1300_history/note.md` (Lỗi 3) |
| 1.4.15 | PASS | Menu đơn CÔNG NỢ đủ **5 mục**: Chi tiết / In lại bill / In lại tem / In lại HĐĐT / **Thanh toán nợ** |
| 1.4.16 | **FAIL/khác checklist** | Menu đơn ĐÃ HỦY chỉ **1 mục "Chi tiết"** (0624 ghi 5 mục). Ảnh: `screenshot/0626_1300_history/note.md` (Lỗi 4) |
| 1.4.17 | PASS | Dòng "Tích điểm" hiển thị (0), không trừ vào tổng |

### 1.5 Tạo đơn từ Trang chủ & kiểm tra Lịch sử
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.5.1 | PASS | Đơn chưa TT (ban 2, POS15062090CN2) hiện trong Lịch sử, "Chưa thanh toán", thẻ xám |
| 1.5.2 | PASS | Đơn đã TT hiện "Đã thanh toán", thẻ xanh, số tiền đúng |
| 1.5.3 | PASS | Đơn công nợ POS15062092CN2 hiện "Công nợ", thẻ cam, số tiền = X = 10.500 |
| 1.5.4 | PASS | Chi tiết công nợ: Tổng X=10.500, Khách đưa Y=5.000, Còn nợ X−Y=5.500 |
| 1.5.5 | PASS | Mã/bàn/tiền/PTTT/trạng thái trong Lịch sử khớp đơn vừa tạo |
| 1.5.6 | PASS | Tạo đơn xong, tổng số đơn tăng đúng +1 (4 → 5) sau khi quay lại Lịch sử |
| 1.5.7 | PASS | Lọc "Chưa thanh toán" chỉ ra đơn chưa TT, KHÔNG lẫn đơn công nợ |
| 1.5.8 | PASS | Lọc "Công nợ" chỉ ra đơn công nợ |

### 1.6 Luồng tạo công nợ & xem chi tiết
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.6.1 | PASS | Màn thanh toán hiển thị tổng đơn X = 10.500 |
| 1.6.2 | PASS | Chọn "Tiền mặt" → hiện ô nhập tiền khách (mặc định = tổng) + nút nhanh 20k/50k/100k |
| 1.6.3 | PASS | Nhập 5.000 (< 10.500) → hiện "Số tiền nợ 5.500đ" + Số ngày 30 + Ngày đáo hạn 26-07-2026 |
| 1.6.4 | PASS | Xác nhận → tạo đơn công nợ thành công ("Thanh toán thành công"), sinh POS15062092CN2 |
| 1.6.5 | PASS | Modal xác nhận: "Phát sinh công nợ 5.500 đ", "Khách hẹn 26-07-2026" |
| 1.6.6 | PASS | Đơn công nợ xuất hiện ngay trong Lịch sử (Hôm nay), trạng thái "Công nợ" |
| 1.6.7 | PASS | Tìm theo SĐT/mã đơn ra đúng đơn công nợ (tìm theo mã đã verify ở 1.2.1) |
| 1.6.8 | PASS | Lọc "Công nợ" hiển thị đúng đơn vừa tạo |
| 1.6.9 | PASS | Thẻ đủ: bàn ban8, KH tranvana, mã POS, số tiền X=10.500, badge "Công nợ" |
| 1.6.10 | PASS | Menu "...": Chi tiết / In lại bill / In lại tem / In lại HĐĐT / **Thanh toán nợ** (không có "Trả hàng") |
| 1.6.11 | PASS | "Chi tiết" mở đúng modal đơn công nợ |
| 1.6.12 | PASS | Badge "Công nợ" (màu cam) phân biệt rõ |
| 1.6.13 | PASS | Tổng tiền thanh toán = X = 10.500 |
| 1.6.14 | PASS | "Khách đưa" = Y = 5.000; PTTT "Tiền mặt" |
| 1.6.15 | PASS | "Tiền khách còn nợ" = X − Y = 5.500 |
| 1.6.16 | PASS | 10.500 = 5.000 + 5.500 (khớp công thức) |
| 1.6.17 | PASS | Danh sách món + Tổng tiền hàng = Σ đúng |
| 1.6.18 | PASS | "Đóng" → quay về Lịch sử, không reset bộ lọc |
| 1.6.19 | N/A | Tiền khách = 0 — chưa tạo đơn riêng để test (tránh sinh nhiều đơn rác); lưu ý cần thành viên (xem 1.6.23) |
| 1.6.20 | PASS (gián tiếp) | Tiền khách = X → đơn "Đã thanh toán" (các đơn đã TT hiện hữu, không phải Công nợ) |
| 1.6.21 | N/A | Tiền khách > X (tiền thừa) — chưa tạo đơn riêng để test |
| 1.6.22 | PASS | Reload (F5) → đơn vẫn "Công nợ", X=10.500 và Y/nợ không đổi |
| 1.6.23 (mới) | PASS | Tạo công nợ với đơn Khách lẻ bị chặn: cảnh báo "Vui lòng chọn thành viên để sử dụng tính năng công nợ" |
| 1.6.24 (mới) | PASS | Modal công nợ đủ 3 dòng: Tổng TT 10.500 / Khách đưa 5.000 / Còn nợ 5.500 |

## Tổng hợp
- **PASS: ~82 mục** (gồm 2 testcase mới 1.6.23, 1.6.24)
- **FAIL: 5 mục**
  - Lỗi chức năng thực: **1.1.6** (bàn trùng tên + lọc "ban 2" ra rỗng), **1.2.19** (tìm theo tên KH rỗng)
  - Khác checklist (cần xác nhận chủ ý): **1.1.4** (thiếu tab "Đặt online"), **1.4.14** (menu đã TT thiếu "Trả hàng"), **1.4.16** (menu đã hủy chỉ "Chi tiết")
- **N/A: 2 mục** (1.6.19, 1.6.21 — biên tiền khách 0 / tiền thừa, chưa tạo đơn riêng)

## Danh sách lỗi / phát hiện (kèm đường dẫn ghi chú)
1. **[1.1.6] Bàn trùng tên + lọc sai** — "ban 1"/"ban 2" lặp 2 lần; chọn "ban 2" ra rỗng dù có đơn. `screenshot/0626_1300_history/note.md` (Lỗi 1).
2. **[1.2.19] Tìm theo tên khách lỗi** — "tranvana" ra rỗng; SĐT/mã đơn vẫn OK. `screenshot/0626_1300_history/note.md` (Lỗi 2).
3. **[1.4.14] Menu đơn đã TT thiếu "Trả hàng"** — chỉ 4 mục. `screenshot/0626_1300_history/note.md` (Lỗi 3).
4. **[1.4.16] Menu đơn đã hủy chỉ "Chi tiết"** — 1 mục. `screenshot/0626_1300_history/note.md` (Lỗi 4).
5. **[1.1.4] Thiếu tab "Đặt online"** — chỉ 3 tab. `screenshot/0626_1300_history/note.md` (Lỗi 5).
6. **[Mới] Công nợ bắt buộc chọn thành viên** — Khách lẻ không tạo được công nợ (đã thêm 1.6.23 vào checklist).
7. **[Ổn định] Render trắng màn Trang chủ/Lịch sử** — gián đoạn, phải F5 hoặc đổi "số cột" mới hiện đúng.
