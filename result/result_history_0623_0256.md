# Kết quả kiểm thử — HISTORY (Lịch sử)

- Menu: history
- Ngày giờ chạy: 23/06/2026 ~02:56
- Người/agent thực hiện: Claude
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — user `admin` — vai trò **Thu ngân (Cashier)** — chi nhánh **CN1** — app **1.0.0+65** — trình duyệt Chrome
- Tài liệu: `run/run_history.md` + `Checklist/checklist_history.md`

> Ảnh lỗi: công cụ chụp màn hình trình duyệt trong phiên này **không lưu được file ảnh ra đĩa** (giống các phiên trước). Các lỗi được mô tả bằng văn bản kèm số liệu đối chứng + các bước tái hiện. Xem `screenshot/0623_0256_history/note.md`.

## Bối cảnh dữ liệu
- **Hôm nay (23/06/2026): 0 đơn** (Hôm qua 22/06 cũng 0 đơn). Đơn gần nhất là 20/06.
- Để kiểm thử bộ lọc, dùng phạm vi **"Tháng này" (01/06–23/06) = 498 đơn**.
- Phân bố theo trạng thái (lọc trong tháng): Đã thanh toán **206** + Chưa thanh toán **8** + Đã hủy **280** + Đã xử lý trả hàng **0** + Công nợ **4** = **498** ✓ (khớp tab Tất cả).
- Loại đơn: Mang về **27** đơn; còn lại tại bàn.

## Bảng kết quả

### 1.1 Bộ lọc loại đơn
| Mục | Testcase | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.1.1 | Tab "Tất cả" | PASS | Hiển thị đủ 498 đơn |
| 1.1.2 | Tab "Tại bàn" | **FAIL** | Tab "Tại bàn" vẫn = **498 đơn** (bằng tab Tất cả) và **vẫn hiển thị đơn "Bàn mang về"** (POS15062069CN2). Đúng phải = 498−27 = 471. Xem BUG-01 |
| 1.1.3 | Tab "Mang về" | PASS | 27 đơn, tất cả đều "Bàn mang về" |
| 1.1.4 | Tab "Đặt online" | N/A | Trang Lịch sử chỉ có 3 tab: Tất cả / Tại bàn / Mang về — **không có tab "Đặt online"** |
| 1.1.5 | Dropdown "Chọn bàn" | PASS | Chọn "ban 1" (mục đầu) → đúng 118 đơn, tất cả là ban 1 (không tái hiện lỗi "ra rỗng" 0616) |
| 1.1.6 | Bàn không trùng tên | **FAIL** | "ban 1" và "ban 2" mỗi tên **xuất hiện 2 lần** trong dropdown. 2 mục "ban 1" trả về số đơn khác nhau (118 và 34) ⇒ là 2 bàn khác ID nhưng trùng tên. Xem BUG-04 |
| 1.1.7 | Tab "Tại bàn" loại đúng đơn mang về | **FAIL** | Trùng BUG-01: tab "Tại bàn" không loại đơn "Bàn mang về" |

### 1.2 Tìm kiếm & bộ lọc
| Mục | Testcase | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.2.1 | Tìm theo mã đơn | PASS | `POS15062080CN2` → đúng 1 đơn |
| 1.2.2 | Tìm theo SĐT | PASS | `0321564987` → đúng 4 đơn (khách tranvana) |
| 1.2.2b/1.2.19 | Tìm theo **tên khách hàng** | **FAIL** | `tranvana` → **0 đơn** dù có 4 đơn của khách này (tìm bằng SĐT ra đúng). Search theo tên khách KHÔNG hoạt động (placeholder ghi "Tìm theo mã đơn, tên khách hàng"). Xem BUG-02 |
| 1.2.3 | Tìm không khớp | PASS | `xxxx9999` → danh sách rỗng |
| 1.2.4 | Trạng thái: Đã thanh toán | PASS | → 206 đơn, tất cả thẻ xanh "Đã thanh toán" |
| 1.2.5 | Trạng thái: Chưa thanh toán | PASS | → 8 đơn, tất cả thẻ xám "Chưa thanh toán" |
| 1.2.6 | Trạng thái: Đã hủy | PASS | → 280 đơn, tất cả thẻ đỏ "Đã hủy" |
| 1.2.7 | Trạng thái: Đã xử lý trả hàng | N/A | Tùy chọn có tồn tại; lọc → rỗng (không có dữ liệu để đối chiếu) |
| 1.2.8 | Trạng thái: Công nợ | PASS | → 4 đơn, tất cả thẻ cam "Công nợ" |
| 1.2.9 | Lọc theo Tài khoản | PASS | Dropdown nay có nhiều tài khoản (Admin master, tran van a, cashier, ADMIN5, admincn1, casher2…). Chọn "Admin master" → 330 đơn (tập con của 498) |
| 1.2.10 | Khoảng ngày: Hôm nay | PASS | 23/06 → 0 đơn (đúng, hôm nay không có đơn) |
| 1.2.11 | Khoảng ngày: Hôm qua | PASS | 22/06 → rỗng (đúng, không có đơn) — lọc 1-ngày hoạt động đúng |
| 1.2.12 | Khoảng ngày: Tuần này | PASS | 22–23/06 → rỗng (đúng, tuần này chưa có đơn; đơn gần nhất 20/06) |
| 1.2.13 | Khoảng ngày: Tháng này | PASS | 01–23/06 → **498 đơn (đủ mọi trạng thái)**. **BUG-03 của 0616/0619 ĐÃ FIX** (trước đây chỉ trả 4 đơn paid-only) |
| 1.2.14 | Khoảng ngày: Tùy chọn | PASS | Tùy chọn 19–20/06 → 21 đơn gồm đủ trạng thái (xanh/đỏ/xám/cam/mang về) |
| 1.2.15 | Kết hợp nhiều bộ lọc | PASS | Đã chạy tổ hợp: bàn "ban 1" + mã đơn; Tài khoản "Admin master" + Tháng này (330) — các bộ lọc cộng dồn đúng |
| 1.2.16 | Ngày bắt đầu > ngày kết thúc | PASS | Chọn ngày 20 trước rồi ngày 18 → calendar tự sắp xếp thành khoảng 18–20, không tạo khoảng ngược/kết quả sai |
| 1.2.17 | (Mới) Lọc khoảng nhiều ngày trả đúng đơn | PASS | **BUG NẶNG 0616/0619 ĐÃ FIX**: khoảng nhiều ngày nay trả về đủ đơn mọi trạng thái (Tháng này = 498 = tổng các trạng thái; Tùy chọn 19–20 = 21 đơn đủ trạng thái) |
| 1.2.18 | (Mới) Lọc theo trạng thái thực tế | PASS | Tập trạng thái **khớp checklist**: Đã thanh toán / Chưa thanh toán / Đã hủy / Đã xử lý trả hàng / Công nợ |

### 1.3 Danh sách đơn
| Mục | Testcase | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.3.1 | Thẻ đủ thông tin | PASS* | Có: tên bàn, ngày giờ, mã đơn, số tiền, trạng thái TT, trạng thái HĐĐT. **Không hiển thị tài khoản nhân viên** trên thẻ — dòng đầu là **tên khách hàng** (tranvana / "Khách lẻ") |
| 1.3.2 | Trạng thái TT hiển thị đúng | PASS | "Đã thanh toán" / "Chưa thanh toán" / "Đã hủy" / "Công nợ" hiển thị đúng |
| 1.3.3 | Trạng thái HĐĐT | PASS | "Chờ ký" (đơn đã TT) / "Không xác định" (đơn hủy/chưa TT) |
| 1.3.4 | Màu thẻ theo trạng thái | PASS* | Đã thanh toán = **xanh lá**; Đã hủy = **đỏ**; Chưa thanh toán = **xám**; Công nợ = **cam**. (Checklist gốc ghi chưa TT=xám / đã TT=xanh dương — thực tế đã TT = xanh lá, có thêm màu cam cho Công nợ) |
| 1.3.5 | Số tiền thẻ khớp chi tiết | PASS | Thẻ 826.486 = **Thực thu** trong chi tiết = 826.486 |

### 1.4 Chi tiết đơn hàng (đơn `POS15062069CN2`)
| Mục | Testcase | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.4.1 | Mở modal chi tiết | PASS* | Mở qua menu **"..." → "Chi tiết"** (bấm thân thẻ KHÔNG mở modal). Tiêu đề **"Chi tiết hóa đơn"**, hiển thị đúng mã đơn POS15062069CN2 |
| 1.4.2 | Thông tin đơn | PASS | Bàn: Bàn mang về; Khách hàng: tranvana; SĐT: 0321564987; Người tạo: Admin master; Số khách: 1; Ngày tạo: 19/06/2026 11:56; Hình thức TT: Tiền mặt |
| 1.4.3 | Danh sách món | PASS | tran chau (10.000×1=10.000); comboo 10 (đơn giá 499.500, thành tiền 729.510 gồm topping: +FIFO 117.100, +Nuoc trai cay 1.500, +test0 111.410) |
| 1.4.4 | Tổng tiền hàng | PASS | 739.510 = 10.000 + 729.510 ✓ (đã kiểm bằng máy tính) |
| 1.4.5 | Phụ thu/Giảm/Điểm/VAT | PASS | Phụ thu 50.000; Giảm giá 0; Tích điểm 0; VAT 36.976 (=5% × 739.510). Đều hiển thị |
| 1.4.6 | Tổng tiền thanh toán | PASS | Thực thu 826.486 = 739.510 + 50.000 − 0 − 0 + 36.976 ✓ (đúng công thức) |
| 1.4.7 | Phương thức thanh toán | PASS | "Tiền mặt"; dòng dưới Thực thu hiển thị "Tiền mặt 826.486" — khớp |
| 1.4.8 | Đóng modal | PASS | Có **nút "Đóng"** (xanh, dưới cùng) và icon **X** góc phải. Bấm "Đóng" → modal đóng, bộ lọc giữ nguyên (Tất cả / 498 đơn / 01–23/06) |

## Tổng hợp
- **PASS: 28** (gồm các mục PASS*)
- **FAIL: 4** — 1.1.2, 1.1.6, 1.1.7, 1.2.2b/1.2.19 (tìm theo tên khách)
- **N/A: 2** — 1.1.4 (không có tab Đặt online), 1.2.7 (không có dữ liệu trả hàng)

## So sánh với phiên trước (0619)
- ✅ **BUG-03 (lọc khoảng nhiều ngày bỏ sót đơn) — ĐÃ FIX**: Tháng này nay = 498 đơn đủ trạng thái (0619 chỉ trả 4 đơn paid-only).
- ✅ **Lọc theo Tài khoản — nay dùng được**: dropdown có nhiều tài khoản (0619 chỉ 1 tài khoản).
- ✅ **Nút "Đóng" modal — nay đã có** (0619 chỉ có icon X).
- ❌ Còn tồn tại: BUG-01 (tab Tại bàn không loại đơn mang về), BUG-02 (tìm theo tên khách), BUG-04 (bàn trùng tên trong dropdown).

## Danh sách lỗi (chi tiết & cách tái hiện)

1. **[BUG-01 / 1.1.2, 1.1.7] Tab "Tại bàn" không loại đơn mang về**
   - Tái hiện: Lịch sử → đặt khoảng "Tháng này" → bấm tab "Tại bàn".
   - Kỳ vọng: chỉ hiện đơn tại bàn (498 − 27 = 471 đơn), không có đơn "Bàn mang về".
   - Thực tế: tab "Tại bàn" hiển thị **498 đơn** (bằng tab Tất cả) và vẫn có đơn "Bàn mang về" (POS15062069CN2). Tab "Mang về" thì lọc đúng (27 đơn).

2. **[BUG-02 / 1.2.2b / 1.2.19] Tìm theo tên khách hàng không hoạt động**
   - Tái hiện: ô tìm kiếm nhập `tranvana` (tên khách của 4 đơn) → Enter.
   - Kỳ vọng: trả về các đơn của khách "tranvana".
   - Thực tế: **0 đơn**. Trong khi tìm theo **mã đơn** và **SĐT** đều đúng. Placeholder hứa hẹn tìm theo "tên khách hàng" nhưng không chạy.

3. **[BUG-04 / 1.1.6] Dropdown "Tất cả bàn" có bàn trùng tên**
   - Tái hiện: tab "Tại bàn" → mở dropdown "Tất cả bàn".
   - Thực tế: danh sách = Tất cả bàn, **ban 1, ban 2, ban 1, ban 2**, ban kiem tra ten dai, ban_qr, ban3…ban10 ⇒ "ban 1"/"ban 2" lặp 2 lần (trùng tên, khác ID). Chọn "ban 1" mục đầu → 118 đơn; mục thứ hai → 34 đơn ⇒ là 2 bàn riêng nhưng trùng tên, gây nhầm lẫn khi lọc.

## Đề xuất bổ sung checklist
- Đề xuất thêm testcase kiểm "Xuất Excel" (nút "Xuất Excel" có trên thanh bộ lọc nhưng chưa nằm trong checklist) — sẽ bổ sung vào checklist_history.md.
