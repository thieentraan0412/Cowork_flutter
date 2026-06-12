# Kết quả kiểm thử — Menu HOME (phiên 2, dừng giữa chừng theo yêu cầu)
- Ngày giờ chạy: 12/06/2026, ~10:25–11:06 (giờ VN)
- Môi trường: https://order-flutter.nasys.vn (store `thientester`, user `admin`, vai trò Thu ngân/Casher), chi nhánh CN1
- Phiên bản ứng dụng: 1.0.0+39
- Trình duyệt: Chrome (Windows), viewport 1568×733
- Checklist tham chiếu: `Checklist/checklist_home.md`
- Phạm vi đã chạy: **1.1 (toàn bộ), 1.2, 1.3, 1.4 (một phần)**. Các phần 1.5 → 1.15 **chưa chạy** (người dùng yêu cầu dừng).
- Đơn QR phục vụ test: tạo qua link QR bàn ban10 (`table1.klkim.com`), mã `POS00002468CN2`.

## Bảng trạng thái

### 1.1 Sơ đồ bàn — 14 PASS / 1 FAIL
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.1.1 | Hiển thị danh sách bàn theo khu | PASS | 14 bàn + thẻ "Bàn mang về". Khu 1: 12 bàn, khu 2: 2 bàn, tổng khớp 14. Vẫn còn 2 cặp bàn trùng tên ("ban 1", "ban 2") giữa 2 khu (dữ liệu) |
| 1.1.2 | Lọc tab "Bàn trống" | PASS | Hiện đúng 9 bàn trống, khớp số đếm (9) |
| 1.1.3 | Lọc tab "Đang sử dụng" | PASS | Hiện đúng 5 bàn (ban 2, ban kiem tra ten dai, ban3, ban5, ban9), khớp số đếm (5) |
| 1.1.4 | Lọc tab "Chờ xác nhận" | PASS | 0 đơn — empty state "Danh sách bàn thuộc trạng thái 'Chờ xác nhận' rỗng" + nút Tất cả. Sau khi đặt đơn QR: hiện đúng ban10, đếm (1) |
| 1.1.5 | Lọc tab "Chờ thanh toán" | PASS | 0 đơn — empty state đúng. Lưu ý: đơn MANG VỀ đang "Chờ thanh toán" (POS00002407CN2) không được đếm vào tab này |
| 1.1.5b | Lọc theo khu (khu 1 / khu 2) | PASS* | khu 1 → 12 bàn, khu 2 → 2 bàn, cộng khớp 14. *Kèm lỗi nặng về thao tác dropdown: xem BUG-02 (click xuyên popup mở nhầm màn Order của "ban 2" 2 lần) |
| 1.1.6 | Đổi số cột hiển thị | PASS | Chọn "4 cột" → lưới bố trí lại đúng; thiết lập giữ sau F5. Dropdown lúc đầu render trắng (BUG-02) |
| 1.1.7 | Đổi giao diện (1/2/3) | PASS* | Đổi đủ GD1 → GD2 → GD3, kiểu thẻ thay đổi rõ. *Dropdown cực kỳ chập chờn: nhiều cú click không mở, có click bị áp dụng trễ sang lựa chọn khác (BUG-02) |
| 1.1.8 | Thẻ bàn hiển thị thông tin | PASS | Thẻ ban9: tên, timer (18:40), icon hóa đơn (1), icon khách (1), tổng 1.018.999, nhãn "Chưa báo bếp" — đầy đủ |
| 1.1.9 | Tổng tiền trên thẻ bàn | **FAIL** | Thẻ bàn hiển thị tổng CHƯA gồm thuế. Order ban9: Tổng tiền hàng 1.018.999 đ, thuế 81.250 đ, Tổng thanh toán **1.100.249 đ**; thẻ bàn hiện **1.018.999 đ**. Tái xác nhận BUG-01 của phiên 0612_0832 |
| 1.1.10 | Trạng thái "Chưa báo bếp" | PASS | ban9 và ban10 (sau xác nhận đơn QR chưa báo bếp) đều hiện nhãn "Chưa báo bếp" trên thẻ |
| 1.1.11 | Nút "Xác nhận" trên thẻ | PASS | Thẻ ban10 (đơn QR) hiện nút "Xác nhận" → modal "Chọn đơn hàng" → chi tiết POS00002468CN2 (9.000 đ) → Xác nhận → toast "Cập nhật thành công"; Đang sử dụng 5→6, Chờ xác nhận 1→0 |
| 1.1.12 | Bấm vào bàn | PASS* | Mở đúng màn Order. *Có lúc màn Order hiện "Hóa đơn mới"/giỏ trống/"Không có món" thay vì đơn hiện có, phải chờ ~6s hoặc F5 (BUG-03) |
| 1.1.13 | Thêm đơn mang về | PASS | Bấm thẻ "Bàn mang về" → mở màn danh sách ĐƠN MANG VỀ (tab Tất cả/Chờ xác nhận/Đã xác nhận/Chờ thanh toán) → "+ Thêm đơn hàng" → mở Order chế độ Mang về (qua 1 bước danh sách, không mở thẳng Order) |
| 1.1.14 | Số liệu các tab nhất quán | PASS | 3 thời điểm: 9+5+0+0=14 ✓; 8+5+1+0=14 ✓ (sau đơn QR); 8+6+0+0=14 ✓ (sau xác nhận) |

### 1.2 Menu (Thực đơn) — 6 PASS / 1 N/A
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.2.1 | Hiển thị danh mục món | PASS | Đủ tab: Tất cả, Bán chạy, Món mới, Nước ngọt, Nước chế biến, Nước có cồn, Món nước, Món xào, Lẩu, test máy in, banh v1, Test in pc |
| 1.2.2 | Lọc theo danh mục | PASS | Chọn "Nước ngọt" → lưới thay đổi theo danh mục (dữ liệu test gán món khá lộn xộn — "Cơm", "Test Kho 8"… cũng thuộc Nước ngọt) |
| 1.2.3 | Tìm món (F1) | PASS | "tra" (không dấu) → tran chau, Kiemtrakho1-3, kiem tra tra hang, món kiểm tra…; "trà" (có dấu) → đúng "Trà A hỷ". Cả hai đều lọc đúng |
| 1.2.4 | Ẩn/hiện hình ảnh món | PASS | Toggle tắt → thẻ gọn không ảnh; bật lại → có ảnh |
| 1.2.5 | Đổi số cột hiển thị món | PASS* | Chọn "5 cột" → lưới 5 cột đúng (tùy chọn 2–5 cột). *2 lần đầu dropdown render TRẮNG toàn bộ lựa chọn, không chọn được (BUG-02) |
| 1.2.6 | Phân trang (1/5, 2/5...) | N/A | Phiên bản hiện tại không còn chỉ số phân trang; lưới món cuộn dọc liên tục |
| 1.2.7 | Giá món | PASS | Định dạng VND đúng (9.000 đ, 555.000 đ, 999.999 đ…) |

### 1.3 Modal tùy chọn món — 7 PASS / 1 N/A
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.3.1 | Mở modal khi món có tùy chọn | PASS | Bấm "Trà A hỷ" → modal "Chọn món kèm theo" (Size S/M/LL, Ngọt, Đá, Món thêm) |
| 1.3.2 | Chọn thuộc tính | PASS | Chọn Size LL (+3.000) → nút tổng đổi 9.000 → 12.000 ✓ |
| 1.3.3 | Chọn món thêm | PASS | Tích "coca cola 5%" (+5.000) → tổng 17.000 ✓, chỉnh được số lượng món thêm |
| 1.3.4 | Tăng/giảm số lượng | PASS | + → 2 (34.000 ✓); − về 1; bấm − tiếp KHÔNG xuống dưới 1 ✓ |
| 1.3.5 | Nhập ghi chú | N/A | Modal phía thu ngân KHÔNG có ô Ghi chú (bản QR phía khách có). Ghi chú nhập tại dòng món trong hóa đơn (đã test ở 1.4.6) |
| 1.3.6 | Bấm "Chọn" | PASS | "Thêm vào giỏ hàng - 17.000 đ" → dòng món vào hóa đơn, tổng 26.000 ✓ |
| 1.3.7 | Bấm "Đóng" | PASS | Mở modal, không chọn, bấm X → đóng, hóa đơn không đổi |
| 1.3.8 | Tùy chọn hiển thị trong dòng món | PASS | Dòng món hiện: LL +3.000 đ, Đường 20%, Đá 100%, coca cola 5% x1 +5.000 đ; Đơn giá 9.000 + Món thêm +8.000 = 17.000 ✓ |

### 1.4 Hóa đơn / Giỏ hàng — 11 PASS / 2 N/A / 7 CHƯA CHẠY (dừng theo yêu cầu)
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.4.1 | Thêm món vào hóa đơn | PASS | Thêm Trà A hỷ (qua modal) → dòng món xuất hiện, số đếm "Tổng tiền hàng (n)" tăng đúng |
| 1.4.2 | Tăng số lượng (+) | PASS | 9.000 × 2 = 18.000 ✓, tổng 35.000 ✓ |
| 1.4.3 | Giảm số lượng (−) | PASS* | Giảm về 1 đúng; bấm − khi SL=1 → hệ thống chặn (dòng giữ nguyên). *Kèm BUG-05: thuế KHÔNG tính lại khi giảm SL |
| 1.4.4 | Xóa món (nút X) | PASS | Xóa dòng 17.000 → tổng còn 9.000, thuế 450; có thông báo "[khu 1 - ban10 - POS00002468CN2] Hủy món vào lúc 10:57 12/06/2026" |
| 1.4.5 | Sửa đơn giá thủ công | PASS* | Modal "Thay đổi giá bán" (giá gốc/giảm giá/giá mới); đổi 9.000 → 12.000: Thành tiền, Tổng, Thuế (600) đều cập nhật đúng. *Lần nhập đầu giá trị không được ghi nhận, phải mở nhập lại |
| 1.4.6 | Ghi chú từng món | PASS | Nhập "Ít đá, không đường @#!" (200 ký tự max) → lưu hiển thị đúng tại dòng món (kể cả dấu TV + ký tự đặc biệt — đồng thời cover 1.15.6) |
| 1.4.7 | Tổng tiền (tạm tính) | PASS | Tổng tiền hàng = Σ(đơn giá × SL) đúng ở mọi bước (9.000/26.000/35.000/12.000) |
| 1.4.8 | Thuế theo từng món | PASS* | Thuế 5%/món tính đúng (450 cho 9.000; 600 cho 12.000; tính trên giá đã trừ giảm giá: 570 = 5%×11.400). *Cập nhật trễ 1–3s, riêng khi GIẢM SL không tự tính lại (BUG-05) |
| 1.4.9 | Thuế theo cả bill | N/A | Không truy cập được trang admin để xem/cấu hình thuế bill trong phiên này |
| 1.4.10 | Kết hợp thuế món + bill | N/A | Như 1.4.9 |
| 1.4.11 | Tổng tiền thanh toán | PASS | 12.000 + 5.000 (phụ thu) − 600 (giảm) + 570 (thuế) = **16.970 đ** hiển thị đúng ✓ |
| 1.4.12 | Phụ thu | PASS | Modal "Chọn phụ thu" → "ngay cuoi tuan" 5.000 VND → cộng đúng vào tổng |
| 1.4.13 | Giảm giá | PASS (một phần) | Modal "Chọn giảm giá" → giảm giá trực tiếp "giảm giá hằng tuần (5%)" = 600 đ áp đúng tại cashier. CHƯA thực hiện bước thanh toán + đối chiếu trang admin (dừng theo yêu cầu) |
| 1.4.14 | Gợi ý nhanh tiền mặt | CHƯA CHẠY | Màn Order chỉ có ô "Tiền khách đưa" tự điền đúng tổng; nút gợi ý mệnh giá (nếu có) nằm ở màn thanh toán — chưa test |
| 1.4.15 | Combo / Set menu | CHƯA CHẠY | — |
| 1.4.16 | Chọn khách hàng | PASS | Dropdown "Khách lẻ" → modal "Chọn thành viên" (tìm theo tên/SĐT/mã) → chọn "tranvana 0321564987" → gắn vào hóa đơn; dòng giảm giá hiện thêm "Điểm" |
| 1.4.17 | Nhiều hóa đơn / 1 bàn | PASS (một phần) | Nút + cạnh tab hóa đơn tạo được tab "Hóa đơn mới" độc lập (tab cũ POS00002468CN2 giữ nguyên). Chưa kịp thêm món vào tab 2 để đối chiếu tổng riêng. Lưu ý: nút + màu cam cạnh tên khách là "Thêm khách hàng", dễ nhầm |
| 1.4.18 | Đơn các bàn độc lập | CHƯA CHẠY | — |
| 1.4.19 | Hóa đơn trống | PASS | Tab Hóa đơn mới: "Giỏ hàng trống. Hãy chọn món bên trái!", tổng 0 đ, nút Báo bếp bị disable |
| 1.4.20 | Nhân viên phụ trách | CHƯA CHẠY | — |

### 1.5 → 1.15 — CHƯA CHẠY
Toàn bộ các phần In bếp/Thanh toán (1.5), Xác nhận đơn (1.6 — riêng 1.6.3/1.6.7 đã gián tiếp PASS qua 1.1.11), Gửi bếp (1.7), Chuyển bàn (1.8), Gộp bàn (1.9), Tách/ghép (1.10), Hàng tặng (1.11), Khuyến mãi (1.12), Hủy đơn (1.13), Chờ thanh toán (1.14), Đặc thù (1.15 — riêng 1.15.6 đã PASS qua 1.4.6) dừng theo yêu cầu người dùng lúc ~11:05.

## Tổng hợp
- Đã chạy: **45/105** mục checklist (1.1: 15, 1.2: 7, 1.3: 8, 1.4: 13/20, cộng 2 mục cover chéo 1.6.3+1.6.7, 1.15.6)
- **PASS: 38** | **FAIL: 1** (1.1.9) | **N/A: 4** (1.2.6, 1.3.5, 1.4.9, 1.4.10) | Chưa chạy: ~60
- Lỗi ghi nhận: 1 FAIL checklist + 5 lỗi vận hành (BUG-02 → BUG-06)

## Danh sách lỗi

### BUG-01 — Tổng tiền trên thẻ bàn không gồm thuế (testcase 1.1.9) — Trung bình — TÁI XÁC NHẬN (đã ghi ở phiên 0612_0832)
1. Trang chủ → bấm ban9 → màn Order: Tổng tiền hàng 1.018.999, Thuế 81.250, **Tổng thanh toán 1.100.249 đ**.
2. Quay về Trang chủ → thẻ ban9 hiển thị **1.018.999 đ** (chưa thuế).
- Mong đợi: thẻ bàn hiển thị tổng đã gồm thuế.

### BUG-02 — Các dropdown thanh công cụ chập chờn: mở trễ, render trắng, popup kẹt, CLICK XUYÊN — Cao
- **Hiện tượng tổng hợp (1.0.0+39):**
  - Dropdown "khu": bấm 1 lần thường không mở; sau khi mở, click vào item nhiều lần không ăn; popup kẹt hiển thị dù state đã đổi.
  - **Click xuyên popup**: 2 lần click vào item "khu 1" trong popup → hệ thống mở màn Order của bàn "ban 2" nằm PHÍA SAU popup (tái hiện 2/2 lần tại cùng vị trí). Tại màn Order, 1 lần click dropdown "Số cột" lại mở modal "Chọn món kèm theo" của món nằm sau popup.
  - Dropdown "Số cột" (cả Trang chủ và màn Order): nhiều lần mở ra **toàn bộ item trắng**, chỉ item đang chọn có chữ; chọn không ăn, phải mở lại nhiều lần.
  - Dropdown "Giao diện": bấm 4–6 lần mới mở; có lần lựa chọn được áp dụng TRỄ thành lựa chọn khác (chọn GD3 nhưng áp GD2).
- **Tái hiện:** Trang chủ → bấm dropdown "Tất cả"(khu) / "6 cột" / "Giao diện 3" → quan sát; click item trong popup khi popup vừa hiện.
- **Khắc phục tạm:** F5 rồi thao tác chậm; chờ 3–5s giữa các click.

### BUG-03 — Màn Order hiển thị "Hóa đơn mới"/"Không có món" thay vì đơn hiện có — Cao
1. Sau chuỗi thao tác dropdown ở Trang chủ, bấm vào bàn đang có đơn (ban9: 1.018.999; ban10: 9.000).
2. Màn Order mở ra: tab "Hóa đơn mới", giỏ trống, lưới món "Không có món".
3. Đơn thật chỉ hiện sau ~6s hoặc sau F5.
- Rủi ro: thu ngân tưởng bàn trống, order trùng/ghi đè.

### BUG-04 — Nút "Trang chủ" không điều hướng khi đang ở màn Order "Bàn mang về" — Trung bình
1. Trang chủ → Bàn mang về → "+ Thêm đơn hàng" (màn Order Mang về, giỏ trống).
2. Bấm menu "Trang chủ" 3 lần trong ~20s → không có phản hồi, vẫn ở màn Order.
3. Phải F5 mới về được Trang chủ. (Từ màn Order của bàn thường thì nút hoạt động.)

### BUG-05 — Thuế sản phẩm KHÔNG tính lại khi GIẢM số lượng món — Trung bình–Cao (sai tiền)
1. Hóa đơn ban10 có 2 dòng, thuế 1.300 đ (5%×26.000). Tăng SL dòng 1 lên 2 → thuế cập nhật đúng 1.750 (5%×35.000), có trễ ~2s.
2. Giảm SL về 1 (tổng hàng về 26.000) → **thuế vẫn 1.750 đ** (đúng phải 1.300), giữ nguyên >10s; Tổng thanh toán sai theo (27.750 thay vì 27.300).
3. Chỉ khi có thao tác khác (xóa món, sửa giá) thuế mới được tính lại đúng.
- Mong đợi: thuế tính lại ngay khi giảm số lượng.

### BUG-06 — Lệch múi giờ trong modal "Chọn đơn hàng" — Thấp
- Đơn QR đặt lúc **10:39** (giờ VN, hiển thị đúng trên trang QR của khách), nhưng modal "Chọn đơn hàng" phía thu ngân hiển thị "12/06/2026 **03:39**" (giờ UTC). Danh sách Đơn mang về cũng hiển thị "10/06 08:54" cần kiểm tra lại.

## Ảnh màn hình
- Thư mục: `screenshot/0612_1106_home/` (xem README trong đó).
- Phiên này chạy qua trình điều khiển Chrome nên ảnh chụp lỗi được lưu bằng chức năng save-to-disk của extension (3 ảnh: popup kẹt BUG-02, màn Order mang về BUG-04, thuế không tính lại BUG-05) — file nằm trong thư mục Downloads của máy, tên dạng `screenshot_*.jpg`/`claude_screenshot_*`. Nếu không thấy, mô tả chi tiết từng lỗi ở trên đủ để tái hiện.

## Ghi chú thêm & dữ liệu phát sinh do kiểm thử
- Đơn QR **POS00002468CN2** (bàn ban10) được tạo và xác nhận: hiện còn 1 dòng "Trà A hỷ" (M, Đường 20%, Đá 100%, ghi chú "Ít đá, không đường @#!", đơn giá sửa tay 12.000), phụ thu "ngay cuoi tuan" 5.000, giảm giá "giảm giá hằng tuần (5%)" 600, khách hàng "tranvana", **chưa báo bếp, chưa thanh toán** — tổng 16.970 đ.
- Bàn ban10 còn thêm 1 tab "Hóa đơn mới" trống.
- 1 dòng "Trà A hỷ LL + coca cola" (17.000) đã thêm rồi xóa trong quá trình test.
- Toast hệ thống: "Không phát được âm báo thông báo" xuất hiện kèm thông báo hủy món.
- Số liệu bàn của store thay đổi song song giữa các thời điểm (timer các bàn 1369:xx → có đơn tồn rất lâu: ban3 23 hóa đơn, ban5 43 hóa đơn, tổng 0 đ — dữ liệu rác đáng dọn).
