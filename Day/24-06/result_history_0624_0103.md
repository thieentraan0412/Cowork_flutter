# Kết quả kiểm thử — HISTORY (Lịch sử)

- Menu: history
- Ngày giờ chạy: 24/06/2026 ~01:03
- Người/agent thực hiện: Claude
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — user `admin` — vai trò **Thu ngân (Cashier)** — chi nhánh **CN1** — app **1.0.0+67** — trình duyệt Chrome
- Tài liệu: `run/run_history.md` + `Checklist/checklist_history.md`

> **Lưu ý kỹ thuật:** App là **Flutter CanvasKit**. Tương tác tự động (qua trình duyệt) hoạt động được với *tab lọc, dropdown bàn, hộp thoại ngày, menu "...", modal chi tiết* nhưng **ô tìm kiếm (text input) không nhận ký tự** qua mọi cách thử. Vì vậy các testcase tìm kiếm (1.2.1, 1.2.2, 1.2.3, 1.2.19) và tạo đơn cần nhập số tiền (phần lớn 1.5) **bị BLOCKED** trong phiên này. Ảnh lỗi không lưu được ra đĩa → mô tả bằng văn bản trong `screenshot/0624_0103_history/note.md`.

## Bối cảnh dữ liệu
- **Hôm nay (24/06/2026): 1 đơn** lúc mở trang (ban9, `POS15062081CN2`, Chưa thanh toán, 10.000) — dùng kiểm tra bộ lọc mặc định.
- Để kiểm thử bộ lọc dùng phạm vi **"Tháng này" (01/06–24/06) = 499 đơn**.
- Phân bố theo trạng thái (lọc trong tháng): Đã thanh toán **207** + Chưa thanh toán **8** + (Đã hủy + Công nợ + Đã xử lý trả hàng) **284** = **499** ✓.
- Loại đơn: **Mang về 27**; Tại bàn (đúng phải 472, nhưng tab hiển thị 499 — xem BUG-01).

## Bảng kết quả

### 1.1 Bộ lọc loại đơn
| Mục | Testcase | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.1.1 | Tab "Tất cả" | PASS | 499 đơn, đủ mọi loại/trạng thái |
| 1.1.2 | Tab "Tại bàn" | **FAIL** | Tab "Tại bàn" = **499 đơn** (bằng tab Tất cả) và vẫn hiện đơn **"Bàn mang về"** (POS15062069CN2). Đúng phải 499−27=472. **BUG-01** |
| 1.1.3 | Tab "Mang về" | PASS | 27 đơn |
| 1.1.4 | Tab "Đặt online" | N/A | Trang chỉ có **3 tab**: Tất cả / Tại bàn / Mang về — không có tab "Đặt online" |
| 1.1.5 | Dropdown "Chọn bàn" | PASS | Chọn "ban 1" (mục đầu) → 118 đơn, tất cả là ban 1 |
| 1.1.6 | Bàn không trùng tên | **FAIL** | "ban 1" & "ban 2" mỗi tên xuất hiện **2 lần** trong dropdown. **BUG-04** |
| 1.1.7 | Tab "Tại bàn" loại đúng đơn mang về | **FAIL** | Trùng **BUG-01** |

### 1.2 Tìm kiếm & bộ lọc
| Mục | Testcase | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.2.1 | Tìm theo mã đơn | **BLOCKED** | Ô tìm kiếm Flutter không nhận input qua automation (xem lưu ý kỹ thuật) |
| 1.2.2 | Tìm theo SĐT | **BLOCKED** | nt |
| 1.2.3 | Tìm không khớp | **BLOCKED** | nt |
| 1.2.4 | Trạng thái: Đã thanh toán | PASS | → **207 đơn**, thẻ xanh lá |
| 1.2.5 | Trạng thái: Chưa thanh toán | PASS | → **8 đơn**, thẻ xám |
| 1.2.6 | Trạng thái: Đã hủy | KHÔNG HOÀN TẤT | Dropdown trạng thái phản hồi chập chờn; mục có tồn tại; danh sách đơn "Đã hủy" (thẻ đỏ) chiếm đa số (ước ~280) |
| 1.2.7 | Trạng thái: Đã xử lý trả hàng | KHÔNG HOÀN TẤT | Mục có tồn tại; phỏng đoán 0 đơn (không thấy đơn trả hàng) |
| 1.2.8 | Trạng thái: Công nợ | PASS* | Mục tồn tại; có đơn công nợ thực tế (POS15062070CN2, thẻ cam) — xác nhận trạng thái hoạt động |
| 1.2.9 | Lọc theo Tài khoản | CHƯA KIỂM | Dropdown "Tài khoản" có trên thanh lọc; chưa mở được ổn định |
| 1.2.10 | Khoảng ngày: Hôm nay | PASS | 24/06 → 1 đơn (ban9) |
| 1.2.11 | Khoảng ngày: Hôm qua | CHƯA KIỂM | (phiên trước: rỗng) |
| 1.2.12 | Khoảng ngày: Tuần này | CHƯA KIỂM | (phiên trước: rỗng) |
| 1.2.13 | Khoảng ngày: Tháng này | PASS | 01–24/06 → **499 đơn**, đủ trạng thái |
| 1.2.14 | Khoảng ngày: Tùy chọn | CHƯA KIỂM | (lịch chọn ngày hoạt động — xem 1.2.23) |
| 1.2.15 | Kết hợp nhiều bộ lọc | PASS* | "ban 1" + "Tháng này" → 118 đơn (các bộ lọc cộng dồn đúng) |
| 1.2.16 | Ngày bắt đầu > kết thúc | CHƯA KIỂM | |
| 1.2.17 | Lọc khoảng nhiều ngày trả đúng đơn | PASS | Tháng này = 499 = tổng các trạng thái (không bỏ sót) |
| 1.2.18 | Lọc theo trạng thái thực tế | PASS* | Tập trạng thái khớp: Đã thanh toán / Chưa thanh toán / Đã hủy / Đã xử lý trả hàng / Công nợ (không có "Đang xử lý/Hoàn thành/Chờ thanh toán") |
| 1.2.19 | Tìm theo tên khách hàng | **BLOCKED** | Không nhập được; phiên trước ghi nhận **lỗi** (0 đơn). Cần kiểm thủ công |
| 1.2.20 | Nút "Xuất Excel" | CHƯA KIỂM | Nút tồn tại; không bấm để tránh tải file khi chưa được phép |
| 1.2.21 | Khoảng ngày: Quý này | PASS* | **Mục "Quý này" có trong hộp thoại thời gian** (xác nhận tồn tại; chưa áp dụng ổn định để đếm) |
| 1.2.22 | Khoảng ngày: Năm nay | PASS* | **Mục "Năm nay" có trong hộp thoại** (xác nhận tồn tại) |
| 1.2.23 | Lịch chặn chọn ngày tương lai | PASS | Khi hôm nay 23/06: các ngày 24–30/06 bị làm mờ, **không chọn được**; bấm "24" không đổi lựa chọn (vẫn "23") |
| 1.2.24 | Hộp thoại ngày — nút "Hủy" | PASS | Chọn "Tháng này" rồi "Hủy" → đóng, giữ nguyên "Hôm nay" (1 đơn) |
| 1.2.25 | Hộp thoại ngày — nút "Áp dụng" | PASS | Chọn "Tháng này" → "Áp dụng" → nhãn đổi "01/06–24/06", danh sách = 499 |
| 1.2.26 | Bộ lọc mặc định khi mở trang | PASS | Mặc định: tab "Tất cả", Trạng thái "Tất cả", "Tất cả bàn", thời gian "Hôm nay"; danh sách chỉ đơn hôm nay |
| 1.2.27 | Dropdown "Trạng thái" đủ mục | PASS | Đúng **6 mục**: Tất cả / Đã thanh toán / Chưa thanh toán / Đã hủy / Đã xử lý trả hàng / Công nợ |

### 1.3 Danh sách đơn
| Mục | Testcase | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.3.1 | Thẻ đủ thông tin | PASS* | Có: tên bàn, **tên khách hàng** (Khách lẻ/tranvana/trannaca…), ngày giờ, mã đơn, số tiền, Trạng thái, HĐĐT. **KHÔNG hiển thị tài khoản nhân viên** trên thẻ |
| 1.3.2 | Trạng thái TT hiển thị đúng | PASS | Chưa thanh toán / Đã thanh toán / Đã hủy / Công nợ |
| 1.3.3 | Trạng thái HĐĐT | PASS | "Chờ ký" (đơn đã TT) / "Không xác định" (đơn hủy/chưa TT) |
| 1.3.4 | Màu thẻ theo trạng thái | PASS* | Chưa TT = **xám**; Đã TT = **xanh lá**; Đã hủy = **đỏ**; Công nợ = **cam**. (Checklist gốc ghi đã TT=xanh dương — thực tế xanh lá; có thêm màu cam cho Công nợ) |
| 1.3.5 | Số tiền thẻ khớp chi tiết | PASS | Thẻ POS15062070CN2 = 521.000 = "Tổng tiền thanh toán" trong modal = 521.000 |
| 1.3.6 | Bộ đếm "Tổng: X đơn" | PASS | Cập nhật đúng mỗi lần đổi lọc: 1 → 499 → 27 (Mang về) → 207 (Đã TT) → 8 (Chưa TT) → 118 (ban 1) |

### 1.4 Chi tiết đơn hàng
> Kiểm trên 2 đơn: `POS15062081CN2` (Chưa TT, 1 món) và `POS15062070CN2` (Công nợ, 3 món, có VAT).

| Mục | Testcase | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.4.1 | Mở modal chi tiết | PASS | Mở qua **"..." → "Chi tiết"**. Tiêu đề "Chi tiết hóa đơn", đúng mã đơn |
| 1.4.2 | Thông tin đơn | PASS | Bàn, Khách hàng, Người tạo (Admin master), Ngày tạo, Hình thức TT, SĐT — đầy đủ |
| 1.4.3 | Danh sách món | PASS | POS15062070CN2: coca cola 5% (10.000×1), tran chau (10.000×1), Món chế biến (500.000×1) — tên/SL/đơn giá/thành tiền đúng |
| 1.4.4 | Tổng tiền hàng | PASS | 520.000 = 10.000+10.000+500.000 ✓ |
| 1.4.5 | Phụ thu/Giảm/Điểm/VAT | PASS | Phụ thu 0đ; Giảm giá 0đ; Tích điểm 5210; VAT 1.000đ — đều hiển thị |
| 1.4.6 | Tổng tiền thanh toán | PASS | 521.000 = 520.000 (hàng) + 0 − 0 + 1.000 (VAT) ✓ |
| 1.4.7 | Phương thức thanh toán | PASS | "Tiền mặt" |
| 1.4.8 | Bấm "Đóng" thoát modal | PASS | Nút "Đóng" (xanh, dưới) đóng modal; có cả icon X góc phải |
| 1.4.9 | Bấm thân thẻ không mở chi tiết | PASS* | Bấm thân thẻ KHÔNG mở modal; chỉ mở chi tiết qua menu "..." → "Chi tiết" |
| 1.4.10 | Menu "..." của đơn chưa thanh toán | PASS | Chỉ có **1 mục "Chi tiết"** |
| 1.4.11 | Modal hiển thị "Số khách" | PASS | Số khách: 1 |
| 1.4.12 | Modal hiển thị "Ghi chú" | PASS | Có ô "Ghi chú" (để trống nếu đơn không ghi chú) |
| 1.4.13 | Tiêu đề & badge trạng thái | PASS | Tiêu đề "Chi tiết hóa đơn"; badge góc phải khớp trạng thái ("Chưa thanh toán" / "Công nợ") |

### 1.5 Tạo đơn từ Trang chủ và kiểm tra trong Lịch sử
> Phần lớn 1.5 cần **tạo đơn + nhập số tiền** trên Trang chủ → bị BLOCKED do ô nhập liệu Flutter không nhận input. Chỉ kiểm được qua dữ liệu sẵn có.

| Mục | Testcase | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.5.1 | Đơn chưa TT xuất hiện trong Lịch sử | PASS* (gián tiếp) | Đơn ban9 `POS15062081CN2` trạng thái "Chưa thanh toán", thẻ xám — hiển thị đúng |
| 1.5.2 | Đơn đã TT xuất hiện | PASS* (gián tiếp) | Nhiều đơn "Đã thanh toán" (thẻ xanh) hiển thị đúng, vd POS15062080CN2 = 9.450 |
| 1.5.3 | Đơn công nợ xuất hiện | PASS* (gián tiếp) | POS15062070CN2 trạng thái "Công nợ", số tiền thẻ = 521.000 = tổng đơn |
| 1.5.4 | Chi tiết đơn công nợ đúng phần đã trả/còn nợ | PASS | Modal: Tổng tiền thanh toán **521.000**; Khách đưa **21.000**; Tiền khách còn nợ **500.000** (= 521.000 − 21.000 ✓) |
| 1.5.5 | Mã đơn/tên bàn/số tiền khớp | PASS* (gián tiếp) | Thông tin trên thẻ khớp modal chi tiết |
| 1.5.7 | Lọc "Chưa TT" không lẫn công nợ | PASS* | Lọc "Chưa thanh toán" = 8 đơn (đơn công nợ KHÔNG nằm trong nhóm này) |
| 1.5.8 | Lọc "Công nợ" chỉ trả đơn công nợ | KHÔNG HOÀN TẤT | Dropdown chập chờn; đã xác nhận có nhóm "Công nợ" riêng |

## Tổng hợp
- **PASS: 33** mục (gồm PASS*).
- **FAIL: 3** — 1.1.2, 1.1.6, 1.1.7 (BUG-01 & BUG-04).
- **BLOCKED: 5** — 1.2.1, 1.2.2, 1.2.3, 1.2.19 (tìm kiếm), 1.5.6 (do không nhập được text).
- **N/A: 1** — 1.1.4 (không có tab Đặt online).
- **Chưa hoàn tất/Chưa kiểm: ~9** — 1.2.6, 1.2.7, 1.2.9, 1.2.11, 1.2.12, 1.2.14, 1.2.16, 1.2.20, 1.5.8 (dropdown trạng thái/tài khoản phản hồi chập chờn hoặc tránh tải file).

## Danh sách lỗi (chi tiết & cách tái hiện)

1. **[BUG-01 / 1.1.2, 1.1.7] Tab "Tại bàn" không loại đơn mang về**
   - Tái hiện: Lịch sử → "Tháng này" → bấm tab "Tại bàn".
   - Kỳ vọng: 472 đơn (499 − 27), không có "Bàn mang về".
   - Thực tế: **499 đơn** (= tab Tất cả) và vẫn có thẻ **"Bàn mang về"** (POS15062069CN2). Tab "Mang về" thì lọc đúng (27).

2. **[BUG-04 / 1.1.6] Dropdown "Tất cả bàn" có bàn trùng tên**
   - Tái hiện: mở dropdown "Tất cả bàn".
   - Thực tế: `ban 1, ban 2, ban 1, ban 2, ban kiem tra ten dai, ban_qr, ban3…ban10` — "ban 1"/"ban 2" lặp 2 lần (trùng tên, khác ID; mục "ban 1" đầu → 118 đơn).

3. **[BUG-02 / 1.2.19] Tìm theo tên khách hàng — chưa kiểm thử lại được**
   - Ô tìm kiếm Flutter không nhận input qua automation phiên này. Phiên trước: nhập "tranvana" → 0 đơn (lỗi). **Cần kiểm thủ công.**

## Đề xuất bổ sung checklist (đã thêm vào `Checklist/checklist_history.md`)
Phát hiện mới khi test: **menu "..." khác nhau theo trạng thái đơn** → đã bổ sung mục **1.4.14–1.4.17** (menu của đơn đã TT / công nợ / đã hủy; dòng "Tích điểm" trong modal).
