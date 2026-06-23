# Kết quả kiểm thử — HISTORY (Lịch sử)

- Menu: history
- Ngày giờ chạy: 19/06/2026 ~06:31
- Người/agent thực hiện: Claude
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — user `admin` — vai trò **Thu ngân (Cashier)** — chi nhánh **CN1** — app **1.0.0+58** — trình duyệt Chrome
- Tài liệu: `run/run_history.md` + `Checklist/checklist_history.md`

> Ảnh lỗi: công cụ chụp màn hình trình duyệt trong phiên này **không lưu được file ảnh ra đĩa** (giống các phiên trước). Vì vậy các lỗi được mô tả bằng văn bản kèm số liệu đối chứng + các bước tái hiện. Xem `screenshot/0619_0631_history/note.md`.

## Bối cảnh dữ liệu (Hôm nay 19/06/2026)
- **Tổng 10 đơn**: 1 đơn **Đã thanh toán** (mang về, `POS15062069CN2`, khách `tranvana`, 826.486) + 9 đơn **Đã hủy** (ban1/ban2, khách lẻ).
- Đơn đã thanh toán trong tháng 6: 4 đơn (12/06, 14/06, 19/06).

## Bảng kết quả

### 1.1 Bộ lọc loại đơn
| Mục | Testcase | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.1.1 | Tab "Tất cả" | PASS | Hiển thị đủ 10 đơn |
| 1.1.2 | Tab "Tại bàn" | **FAIL** | Vẫn hiển thị **10 đơn** gồm cả đơn "Bàn mang về" (mang về). Đúng phải = 9 (loại đơn mang về). Xem BUG-01 |
| 1.1.3 | Tab "Mang về" | PASS | Chỉ 1 đơn mang về |
| 1.1.4 | Tab "Đặt online" | N/A | Trang Lịch sử chỉ có 3 tab: Tất cả / Tại bàn / Mang về — **không có tab "Đặt online"** |
| 1.1.5 | Dropdown "Chọn bàn" | PASS | Chọn "ban 1" → đúng 6 đơn ban1 (phiên này lọc bàn hoạt động) |
| 1.1.6 | Bàn không trùng tên | **FAIL** | "ban 1" và "ban 2" mỗi tên **xuất hiện 2 lần** trong dropdown. Xem BUG-04. (Lưu ý: chọn "ban 1" mục đầu phiên này ra đúng 6 đơn — không tái hiện lỗi "ra rỗng" của 0616) |

### 1.2 Tìm kiếm & bộ lọc
| Mục | Testcase | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.2.1 | Tìm theo mã đơn | PASS | `POS15062068CN2` → đúng 1 đơn |
| 1.2.2 | Tìm theo SĐT | PASS | `0321564987` → đúng 1 đơn (khách tranvana) |
| 1.2.2b | Tìm theo **tên khách hàng** | **FAIL** | `tranvana` → **0 đơn** dù có đơn của khách "tranvana". Search theo tên khách KHÔNG hoạt động (placeholder ghi "Tìm theo mã đơn, tên khách hàng"). Xem BUG-02 |
| 1.2.3 | Tìm không khớp | PASS | `xxxx9999` → danh sách rỗng |
| 1.2.4 | Trạng thái: Đã thanh toán | PASS | → 1 đơn (nhãn là "Đã thanh toán", không phải "...thành công") |
| 1.2.5 | Trạng thái: Chưa thanh toán | PASS | → rỗng (hôm nay không có đơn chưa thanh toán) |
| 1.2.6 | Trạng thái: Đã hủy | PASS | → đúng 9 đơn |
| 1.2.7 | Trạng thái: Đã xử lý trả hàng | N/A | Tùy chọn **có tồn tại**; không có dữ liệu để kiểm tra lọc |
| 1.2.8 | Trạng thái: Công nợ | N/A | Tùy chọn **đã xuất hiện** trong dropdown (khác 0616 báo thiếu); không có dữ liệu |
| 1.2.9 | Lọc theo Tài khoản | N/A | Chỉ có 1 tài khoản tạo đơn (Admin master); không tách bạch được |
| 1.2.10 | Khoảng ngày: Hôm nay | PASS | → 10 đơn (đủ cả đơn hủy) |
| 1.2.11 | Khoảng ngày: Hôm qua | PASS | 18/06 (1 ngày) → rỗng (không có đơn) — lọc 1-ngày hoạt động đúng |
| 1.2.12 | Khoảng ngày: Tuần này | **FAIL** | 15–21/06 (chứa hôm nay 10 đơn) → chỉ **1 đơn**. Xem BUG-03 |
| 1.2.13 | Khoảng ngày: Tháng này | **FAIL** | 01–30/06 → **4 đơn (toàn Đã thanh toán)**; bỏ sót 9 đơn hủy của hôm nay. Xem BUG-03 |
| 1.2.14 | Khoảng ngày: Tùy chọn | N/A | Dùng chung cơ chế khoảng nhiều ngày ⇒ suy ra cùng lỗi BUG-03 |
| 1.2.15 | Kết hợp nhiều bộ lọc | N/A | Đã kiểm riêng từng bộ lọc; chưa chạy tổ hợp đầy đủ |
| 1.2.16 | Ngày bắt đầu > kết thúc | N/A | Calendar tự sắp xếp theo thứ tự chọn, không nhập ngược được |
| 1.2.17 | (Mới) Lọc khoảng nhiều ngày trả đúng đơn | **FAIL** | **BUG NẶNG**: khoảng nhiều ngày chỉ trả về đơn "Đã thanh toán", bỏ sót đơn hủy/chưa TT. Xem BUG-03 |
| 1.2.18 | (Mới) Lọc theo trạng thái thực tế | PASS | Tập trạng thái nay **KHỚP checklist**: Đã thanh toán / Chưa thanh toán / Đã hủy / Đã xử lý trả hàng / Công nợ (khác hẳn 0616) |

### 1.3 Danh sách đơn
| Mục | Testcase | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.3.1 | Thẻ đủ thông tin | PASS* | Có: tên bàn, ngày giờ, mã đơn, số tiền. **Không hiển thị tài khoản nhân viên** trên thẻ — dòng đầu là **tên khách hàng** (tranvana / "Khách lẻ"). |
| 1.3.2 | Trạng thái TT hiển thị đúng | PASS | "Đã thanh toán" / "Đã hủy" đúng (hôm nay không có đơn "Chưa thanh toán" để đối chiếu) |
| 1.3.3 | Trạng thái HĐĐT | PASS | "Chờ ký" (đơn đã TT) / "Không xác định" (đơn hủy) |
| 1.3.4 | Màu thẻ theo trạng thái | PASS* | Đã thanh toán = **xanh lá**; Đã hủy = **đỏ**. (Checklist ghi chưa TT=xám / đã TT=xanh dương — thực tế khác; không có đơn "chưa TT" để xác nhận màu xám) |
| 1.3.5 | Số tiền thẻ khớp chi tiết | PASS | Thẻ 826.486 = **Thực thu** trong chi tiết = 826.486 |

### 1.4 Chi tiết đơn hàng (đơn `POS15062069CN2`)
| Mục | Testcase | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.4.1 | Mở modal chi tiết | PASS | Mở qua menu **"..." → "Chi tiết"** (không mở bằng bấm thân thẻ). Tiêu đề **"Chi tiết hóa đơn"**, đúng mã đơn |
| 1.4.2 | Thông tin đơn | PASS | Bàn: Bàn mang về; Khách hàng: tranvana; SĐT: 0321564987; Người tạo: Admin master; Số khách: 1; Ngày: 19/06/2026 11:56; Hình thức TT: Tiền mặt |
| 1.4.3 | Danh sách món | PASS | tran chau (10.000×1=10.000); comboo 10 (đơn giá 499.500, thành tiền 729.510 gồm topping: +FIFO 117.100, +Nuoc trai cay 1.500, +test0 111.410) |
| 1.4.4 | Tổng tiền hàng | PASS | 739.510 = 10.000 + 729.510 ✓ |
| 1.4.5 | Phụ thu/Giảm/Điểm/VAT | PASS | Phụ thu 50.000; Giảm giá 0; Tích điểm 0; VAT 36.976 (≈5% tổng hàng). Đều hiển thị |
| 1.4.6 | Tổng tiền thanh toán | PASS | Thực thu 826.486 = 739.510 + 50.000 − 0 − 0 + 36.976 ✓ (đúng công thức) |
| 1.4.7 | Phương thức thanh toán | PASS | "Tiền mặt"; dòng Thực thu hiển thị "Tiền mặt 826.486" — khớp |
| 1.4.8 | Đóng modal | PASS* | **Không có nút chữ "Đóng"** — đóng bằng **icon X** góc phải. Bộ lọc giữ nguyên sau khi đóng |

## Tổng hợp
- PASS: 20 (gồm các mục PASS*)
- FAIL: 5 — 1.1.2, 1.1.6, 1.2.2(tên KH), 1.2.12/1.2.13/1.2.17 (khoảng nhiều ngày)
- N/A: 8 — 1.1.4, 1.2.7, 1.2.8, 1.2.9, 1.2.14, 1.2.15, 1.2.16
- Ngoài ra: 2 lỗi UX (dropdown chập chờn; popup lịch không tự đóng)

## Danh sách lỗi (chi tiết & cách tái hiện)

1. **[BUG-01 / 1.1.2] Tab "Tại bàn" không loại đơn mang về**
   - Tái hiện: Vào Lịch sử → bấm tab "Tại bàn".
   - Kỳ vọng: chỉ hiện 9 đơn tại bàn (loại đơn "Bàn mang về").
   - Thực tế: hiện **10 đơn**, gồm cả đơn "Bàn mang về" (`POS15062069CN2`). Tab "Mang về" thì lọc đúng (1 đơn).

2. **[BUG-02 / 1.2.2] Tìm theo tên khách hàng không hoạt động**
   - Tái hiện: ô tìm kiếm nhập `tranvana` (tên khách của đơn `POS15062069CN2`) → Enter.
   - Kỳ vọng: trả về đơn của khách "tranvana".
   - Thực tế: **0 đơn**. Trong khi tìm theo **mã đơn** và **SĐT** đều đúng. Placeholder hứa hẹn tìm theo "tên khách hàng" nhưng không chạy.

3. **[BUG-03 / 1.2.12-1.2.13-1.2.17] Bộ lọc khoảng NHIỀU NGÀY bỏ sót đơn (chỉ trả đơn Đã thanh toán)** — MỨC ĐỘ CAO
   - Tái hiện: Vào Lịch sử (Hôm nay = 10 đơn) → bộ lọc thời gian → chọn "Tuần này" (15–21/06) → Áp dụng.
   - Kỳ vọng: ≥ 10 đơn (khoảng chứa hôm nay có 10 đơn).
   - Thực tế: chỉ **1 đơn** (đúng đơn "Đã thanh toán" duy nhất trong khoảng). "Tháng này" (01–30/06) → **4 đơn, toàn bộ Đã thanh toán** — bỏ sót toàn bộ đơn **Đã hủy**.
   - Đối chứng: mốc **1 ngày** đúng — "Hôm nay" → 10 đơn (gồm cả đơn hủy), "Hôm qua" → rỗng.
   - Kết luận: khoảng nhiều ngày **chỉ trả về đơn đã thanh toán**, lọc rớt đơn hủy/chưa thanh toán ⇒ không thể tra cứu/đối soát đơn hủy theo tuần/tháng. (0616 báo trả về RỖNG; nay trả paid-only — vẫn là lỗi.)

4. **[BUG-04 / 1.1.6] Dropdown "Tất cả bàn" có bàn trùng tên**
   - Tái hiện: tab "Tại bàn" → mở dropdown "Tất cả bàn".
   - Thực tế: danh sách = Tất cả bàn, **ban 1, ban 2, ban 1, ban 2**, ban kiem tra ten dai, ban_qr, ban3…ban10 ⇒ "ban 1"/"ban 2" lặp 2 lần (trùng tên, khác ID). Gây khó phân biệt khi lọc.

5. **[UX] Dropdown bộ lọc (Trạng thái / Chọn bàn) chập chờn**
   - Thường phải bấm **2 lần** mục mới chọn được; sau khi chọn còn để lại **lớp phủ "ma"** che danh sách, phải bấm ra ngoài mới hết.

6. **[UX] Popup lịch (calendar) không tự đóng**
   - Sau khi bấm "Áp dụng"/"Hủy", popup lịch đôi khi không đóng; phải bấm ra ngoài hoặc nhấn Escape.

## Ghi nhận tích cực (so với phiên 0616)
- Tập trạng thái trong dropdown nay **khớp checklist** (đủ: Đã thanh toán / Chưa thanh toán / Đã hủy / Đã xử lý trả hàng / Công nợ; "Công nợ" đã xuất hiện).
- Lọc theo bàn cụ thể ("ban 1") phiên này **trả đúng kết quả** (không tái hiện lỗi "ra rỗng" của 0616).
- Tính toán trong chi tiết hóa đơn (Tổng tiền hàng, VAT, Thực thu) **chính xác**.
