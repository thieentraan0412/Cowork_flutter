# Kết quả kiểm thử — Menu HISTORY (Lịch sử đơn hàng) — phiên 0616_0928

- Ngày giờ chạy: 16/06/2026, ~09:28–10:05 (giờ VN)
- Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin`, vai trò **Thu ngân (Cashier)**, chi nhánh **CN1**
- Phiên bản ứng dụng: **1.0.0+54**
- Trình duyệt: Chrome (Windows), điều khiển qua extension
- Checklist tham chiếu: `Checklist/checklist_history.md` — Hướng dẫn: `run/run_history.md` — Link: `Link/Link.md`
- Ghi chú lỗi/quan sát chi tiết: `screenshot/0616_0928_history/note.md` (công cụ **không xuất được ảnh PNG ra đĩa** → mô tả lỗi bằng văn bản kèm dữ liệu đối chứng, như các phiên trước)
- Bối cảnh dữ liệu: **Hôm nay (16/06): 3 đơn** (2 Đã hủy: `PO015062035CN2` ban2 560.000, `PO015062034CN2` ban2 1.000.000; 1 Đã thanh toán: `PO015062033CN2` ban1 1.100.000). **Hôm qua (15/06): 20 đơn** (đa dạng).

## Kết luận nhanh
- ❌ **BUG-01 (NẶNG): Bộ lọc khoảng ngày nhiều ngày trả về RỖNG.** "Tuần này" (15–21/06) và "Tháng này" (01–30/06) đều ra **0 đơn**, dù khoảng chứa 15/06 (20 đơn) và 16/06 (3 đơn). Chỉ mốc **một ngày** (Hôm nay, Hôm qua) chạy đúng.
- ⚠️ **Lệch checklist:** dropdown **Trạng thái** thực tế là `Đang xử lý / Hoàn thành / Đã hủy / Đã trả hàng / Chờ thanh toán` (không có "Công nợ"); **không có tab "Đặt online"** (chỉ 3 tab Tất cả/Tại bàn/Mang về).
- ⚠️ **FIND: bàn trùng tên** trong dropdown "Tất cả bàn" ("ban 1"×2, "ban 2"×2) → chọn "ban 1" (mục đầu) ra rỗng dù có đơn ban1.
- ✅ Tìm kiếm theo mã đơn, lọc theo bàn (ban2), lọc theo trạng thái (Hoàn thành/Đã hủy), lọc theo tài khoản, lọc 1 ngày, kết hợp nhiều bộ lọc, và **chi tiết hóa đơn** (thông tin/món/tổng tiền/VAT/PTTT) đều **đúng**.
- 🔧 Lưu ý kỹ thuật: các dropdown bộ lọc chập chờn (phải bấm 2 lần, tự sắp xếp lại, lớp phủ "ma"); phiên đăng nhập hết hạn & kết nối rớt nhiều lần (môi trường tự động hóa).

---

## 1.1 Bộ lọc loại đơn
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.1.1 | Lọc tab "Tất cả" | **PASS** | Tab mặc định; **3 đơn** đủ loại trạng thái (2 Đã hủy + 1 Đã thanh toán), không phân biệt loại |
| 1.1.2 | Lọc tab "Tại bàn" | **PASS** | **3 đơn**, đều là đơn tại bàn (đúng — hôm nay toàn đơn tại bàn). Tab này còn hiện thêm dropdown "Tất cả bàn" + "Tài khoản" |
| 1.1.3 | Lọc tab "Mang về" | **PASS** | Rỗng — "Không tìm thấy đơn hàng nào" (đúng, hôm nay không có đơn mang về) |
| 1.1.4 | Lọc tab "Đặt online" | **FAIL / N-A** | **Không có tab "Đặt online"**. Thanh tab chỉ có 3: Tất cả / Tại bàn / Mang về (xem FIND-03) |
| 1.1.5 | Dropdown "Chọn bàn" | **PASS\*** | Dropdown tên **"Tất cả bàn"**, có lọc (chọn **ban 2** → đúng **2 đơn**). **\*Bất thường:** mục bàn **trùng** ("ban 1"×2, "ban 2"×2); chọn **"ban 1"** (mục đầu) → **rỗng** dù có đơn ban1 (xem FIND-04) |

## 1.2 Tìm kiếm & bộ lọc
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.2.1 | Tìm theo mã đơn | **PASS** | Nhập `PO015062033CN2` + Enter → đúng **1 đơn** tương ứng |
| 1.2.2 | Tìm theo số điện thoại | **N/A** | Toàn bộ khách là "Khách lẻ", **không có dữ liệu SĐT** (ô SĐT trong chi tiết để trống) → không có dữ liệu để xác nhận |
| 1.2.3 | Tìm không khớp | **PASS** | Nhập `xxxx9999` → danh sách rỗng "Không tìm thấy đơn hàng nào" |
| 1.2.4 | Trạng thái: Đã thanh toán thành công | **PASS\*** | Không có nhãn này; dùng **"Hoàn thành"** → đúng **1 đơn** đã thanh toán (`PO015062033CN2`). Lệch nhãn (xem FIND-02) |
| 1.2.5 | Trạng thái: Chưa thanh toán | **PASS\* / no-data** | Không có nhãn này; gần nhất **"Chờ thanh toán"** → rỗng (hôm nay không có đơn loại này). Lệch nhãn |
| 1.2.6 | Trạng thái: Đã hủy | **PASS** | Chọn **"Đã hủy"** → đúng **2 đơn** Đã hủy |
| 1.2.7 | Trạng thái: Đã xử lý trả hàng | **PASS\* / no-data** | Không có nhãn này; gần nhất **"Đã trả hàng"** → rỗng hôm nay. Lệch nhãn |
| 1.2.8 | Trạng thái: Công nợ | **FAIL / N-A** | **Không có tùy chọn "Công nợ"** trong dropdown trạng thái (xem FIND-02) |
| 1.2.9 | Lọc theo Tài khoản (nhân viên) | **PASS** | Dropdown "Tài khoản": Admin master / tran van a / tranvanb / tranvanc. Chọn **Admin master** → **3 đơn** (đúng, hôm nay đều do admin tạo) |
| 1.2.10 | Khoảng ngày: Hôm nay | **PASS** | 16/06 → **3 đơn** |
| 1.2.11 | Khoảng ngày: Hôm qua | **PASS** | 15/06 → **20 đơn** |
| 1.2.12 | Khoảng ngày: Tuần này | **FAIL (BUG-01)** | 15/06–21/06 → **0 đơn** dù chứa 15/06 (20 đơn) + 16/06 (3 đơn) |
| 1.2.13 | Khoảng ngày: Tháng này | **FAIL (BUG-01)** | 01/06–30/06 → **0 đơn** dù chứa toàn bộ đơn tháng 6 |
| 1.2.14 | Khoảng ngày: Tùy chọn | **FAIL\* (BUG-01)** | Chọn ngày qua lịch được; nhưng **khoảng nhiều ngày → rỗng** (cùng lỗi BUG-01). Mốc 1 ngày thì chạy. Lịch còn có thêm "Quý này"/"Năm nay" |
| 1.2.15 | Kết hợp nhiều bộ lọc | **PASS** | **Tại bàn + "Hoàn thành" + Hôm nay** → đúng **1 đơn** (ban1 `PO015062033CN2`, đã thanh toán) — giao của các điều kiện đúng |
| 1.2.16 | Ngày bắt đầu > ngày kết thúc | **PASS** | Lịch **chặn** trạng thái không hợp lệ: bấm ngày kết thúc (10) sau ngày bắt đầu (20) → tự đặt lại bắt đầu = 10; không thể tạo khoảng bắt đầu > kết thúc |

## 1.3 Danh sách đơn
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.3.1 | Thẻ đơn hiển thị đủ thông tin | **PASS\*** | Thẻ hiện: tên bàn, khách hàng (Khách lẻ), ngày giờ, mã đơn, số tiền, Trạng thái, HĐĐT. **Lưu ý:** thẻ **không hiển thị tài khoản nhân viên** (chỉ có trong chi tiết: "Người tạo") |
| 1.3.2 | Trạng thái thanh toán hiển thị đúng | **PASS** | Đơn đã thanh toán hiện "Đã thanh toán" (xanh); đơn hủy hiện "Đã hủy" (đỏ). (Hôm nay không có đơn "Chưa thanh toán" để hiện nhãn đó) |
| 1.3.3 | Trạng thái HĐĐT hiển thị đúng | **PASS** | Hiện đúng "Không xác định" (đơn hủy) và "Chờ ký" (đơn đã thanh toán) |
| 1.3.4 | Màu thẻ theo trạng thái | **PASS\*** | **Đã thanh toán = xanh lá** ✓; **Đã hủy = đỏ**. Checklist nhắc "chưa thanh toán = xám" — không có đơn loại này hôm nay để xác nhận màu xám |
| 1.3.5 | Số tiền trên thẻ khớp chi tiết | **PASS** | Thẻ ban1 = **1.100.000** = "Thực thu" trong modal chi tiết (Tổng hàng 1.000.000 + VAT 100.000). Số tiền thẻ = tổng thanh toán đã gồm VAT |

## 1.4 Chi tiết đơn hàng  (kiểm trên đơn ban1 `PO015062033CN2`, đã thanh toán)
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.4.1 | Bấm vào đơn mở modal chi tiết | **PASS\*** | Mở qua **menu "..." → "Chi tiết"** (không mở bằng cách bấm thân thẻ). Modal **"Chi tiết hóa đơn"**, hiển thị đúng mã đơn `PO015062033CN2` + ngày + nhãn "Đã thanh toán" |
| 1.4.2 | Thông tin đơn hiển thị đúng | **PASS** | Bàn **ban 1**, Khách hàng **Khách lẻ**, Người tạo **Admin master**, Ngày tạo **16/06/2026 08:35**, Số khách **1** — khớp dữ liệu thẻ |
| 1.4.3 | Danh sách món hiển thị đúng | **PASS** | Dòng món: **test hang hoa** — Đơn giá **500.000** — SL **2** — Thành tiền **1.000.000** |
| 1.4.4 | Tổng tiền hàng tính đúng | **PASS** | 500.000 × 2 = **1.000.000** = "Tổng tiền hàng" ✓ |
| 1.4.5 | Phụ thu/Giảm giá/Tiền điểm/VAT | **PASS** | Phụ thu 0, Giảm giá 0, Tích điểm 0, **VAT 100.000** (=10%) — hiển thị đúng. (Đơn này không áp phụ thu/giảm giá nên chưa thử giá trị ≠ 0) |
| 1.4.6 | Tổng tiền thanh toán đúng công thức | **PASS** | "Thực thu" **1.100.000** = 1.000.000 + 0 − 0 − 0 + 100.000 ✓ (nhãn là "Thực thu") |
| 1.4.7 | Phương thức thanh toán hiển thị đúng | **PASS** | "Hình thức TT: **Tiền mặt**"; phần thu: "Tiền mặt 1.100.000" — khớp |
| 1.4.8 | Bấm "Đóng" thoát modal | **PASS\*** | Đóng bằng **icon X** (không có nút chữ "Đóng"); về danh sách, bộ lọc giữ nguyên |

---

## Tổng hợp
- **PASS:** 23 (gồm các PASS\* đạt-nhưng-có-lưu-ý)
- **FAIL:** 4 — **1.2.12, 1.2.13, 1.2.14** (BUG-01 lọc khoảng ngày) + **1.2.8 / 1.1.4** (UI thiếu tùy chọn so với checklist — tính là FAIL/N-A)
- **N/A:** 1 — **1.2.2** (không có dữ liệu SĐT khách)

*(1.1.4 và 1.2.8 là FAIL do UI không có mục tương ứng — xem cột Kết quả ở bảng trên.)*

## Danh sách lỗi & phát hiện (chi tiết: `screenshot/0616_0928_history/note.md`)
1. **BUG-01 (NẶNG, 1.2.12/1.2.13/1.2.14):** Bộ lọc **khoảng ngày nhiều ngày** ("Tuần này", "Tháng này", khoảng tùy chọn) trả về **rỗng** dù khoảng chứa ngày có đơn. Chỉ mốc **một ngày** chạy đúng. → **Ưu tiên fix.**
2. **FIND-02 (1.2.4–1.2.8):** Dropdown trạng thái thực tế: `Đang xử lý / Hoàn thành / Đã hủy / Đã trả hàng / Chờ thanh toán` — **không có "Công nợ"**, nhãn khác checklist (Đã thanh toán→Hoàn thành, Chưa thanh toán→Chờ thanh toán, Đã xử lý trả hàng→Đã trả hàng). Cần đồng bộ checklist/UI.
3. **FIND-03 (1.1.4):** Trang Lịch sử **không có tab "Đặt online"** (chỉ 3 tab).
4. **FIND-04 (1.1.5):** Dropdown "Tất cả bàn" có **bàn trùng tên** ("ban 1"×2, "ban 2"×2); chọn "ban 1" (mục đầu) → rỗng dù có đơn ban1. Cần rà soát dữ liệu bàn.
5. **FIND-05 (UX):** Dropdown bộ lọc (Trạng thái/Bàn/Tài khoản) chập chờn — phải bấm 2 lần, tự sắp xếp lại, để lại lớp phủ "ma".
6. **FIND-06 (UX):** Popup lịch để lại lớp phủ "ma" sau khi Áp dụng.
7. **FIND-07 (Môi trường):** Phiên đăng nhập hết hạn + kết nối trình duyệt rớt nhiều lần khi tự động hóa.

## Khuyến nghị
1. **Ưu tiên fix BUG-01** (lọc khoảng ngày) — đây là lỗi chặn nghiệp vụ tra cứu/đối soát lịch sử.
2. Đồng bộ **nhãn & tập trạng thái** trong bộ lọc với checklist/sản phẩm; làm rõ "Công nợ", "Đặt online" có nằm trong phạm vi trang Lịch sử không.
3. Rà soát **dữ liệu bàn trùng tên** (ban 1, ban 2) gây lọc sai.
4. Cải thiện UX các **dropdown/popup lịch** (đóng overlay, chọn 1 lần, không tự sắp xếp lại).
5. Phiên sau nên có sẵn đơn **"Chưa thanh toán"/"Đã trả hàng"** trong ngày để xác nhận đủ các trạng thái và màu thẻ (xám).
