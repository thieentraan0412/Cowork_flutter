# Kết quả kiểm thử — Menu CASHBOOT (Thu chi) — phiên 0616_1305

- Ngày giờ chạy: 16/06/2026, ~13:05–14:10 (giờ VN)
- Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin`, vai trò **Thu ngân (Cashier)**, chi nhánh **CN1**
- Phiên bản ứng dụng: **1.0.0+54** — Trình duyệt: Chrome (Windows), điều khiển qua extension
- Checklist: `Checklist/checklist_cashboot.md` — Hướng dẫn: `run/run_cashboot.md` — Link: `Link/Link.md`
- Ghi chú lỗi chi tiết: `screenshot/0616_1305_cashboot/note.md` (công cụ **không xuất được ảnh PNG ra đĩa** → mô tả lỗi bằng văn bản + dữ liệu đối chứng, như các phiên trước)
- Bối cảnh dữ liệu (Tháng này, CN1, đầu phiên): Tồn đầu kỳ **8.264.976.882**, Tổng thu **767.780.909**, Tổng chi **1.179.745**, Số dư cuối ca **9.031.578.046** (✔ đúng công thức), 203 phiếu. Mã phiếu thực tế dạng **PC…** (thu) / **PT…** (chi), KHÁC ví dụ "vote-00001" của checklist.

## Kết luận nhanh
- ❌ **BUG-01 (NẶNG, 1.4.14): Phiếu Số tiền = 0 vẫn tạo thành công** (sinh PT00000034 Chi 0đ), không bị chặn. → Ưu tiên fix.
- ⚠️ **Lệch checklist (UI):** (1) Không có bộ lọc **"Loại nguồn"** (Bán hàng/Mua hàng/Tự tạo/Trả hàng) — bộ lọc "Loại" chỉ theo **vai trò** (Quản lý/Quầy bếp/Thu ngân/NV order/Khác) → kéo theo 1.1.10, 1.5.7–1.5.9. (2) **Mô tả giới hạn 50** ký tự (không phải 200). (3) Label luôn **"Người nộp / Người nhận"** (không đổi theo Thu/Chi). (4) **Bỏ tích cả 2 đối tượng** ở Công nợ → hiện TẤT␣CẢ thay vì rỗng.
- ⚠️ **FIND-BALANCE:** "Tồn đầu kỳ" & "Số dư cuối ca" **tính lại theo bộ lọc Loại thu chi** (Thu-only/Chi-only ra số khác) — "đầu kỳ" lẽ ra cố định.
- 🚧 **BLOCKED:** Tab **Trả hàng "đang phát triển"** → không test được phiếu trả hàng (1.5.6, 1.5.11). Upload tệp & nội dung file Excel không kiểm được qua tự động hóa (1.3.4, 1.4.9, 1.4.18, 1.6.2).
- ✅ Toàn bộ **lõi nghiệp vụ Thu chi chạy đúng**: lọc (mã/chi nhánh/thời gian/người tạo/loại/phân loại/kết hợp), 4 thẻ tổng quan & công thức số dư, tính liên tục đầu–cuối kỳ, thêm phiếu thu/chi thủ công (+/− đúng quỹ), validate trường bắt buộc, **đơn bán tiền mặt tự sinh phiếu thu khớp số tiền & PTTT**, số liệu **khớp Điều phối ca**, đơn hủy không tính quỹ, xuất Excel, và bộ lọc Công nợ.
- 🔧 Kỹ thuật: dropdown bộ lọc hay kẹt "lớp phủ ma" (phải tải lại trang); màn hình thỉnh thoảng đơ khi tự động hóa (môi trường).

---

## 1.1 Bộ lọc
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.1.1 | Tìm theo Mã phiếu | **PASS** | Gõ `PC00001623CN2` (lọc **live**, không Enter) → đúng 1 phiếu, thẻ cập nhật (✔ công thức). Gõ `xxxx999` → "Không có dữ liệu". *Lưu ý: nhấn Enter gây nhảy trang.* |
| 1.1.2 | Lọc theo Chi nhánh | **PASS** | Dropdown CN1/cn11/cn12. cn11 → 3 phiếu (5.500.000+6.831.000=12.331.000 ✔); cn12 → 1 phiếu (0+30.000=30.000 ✔). |
| 1.1.3 | Thời gian: Hôm nay/Hôm qua | **PASS** | Hôm nay 16/06=1 phiếu; Hôm qua 15/06=5 phiếu (Σ 4.020.210 = Tổng thu ✔). Khoảng ngày auto cập nhật. |
| 1.1.4 | Thời gian: Tuần này/Tuần trước | **PASS** | Tuần này (15→16/06)=6 phiếu (Σ 5.120.210 ✔); Tuần trước (08→14/06)=84 phiếu (✔ công thức). **Khoảng nhiều ngày chạy đúng** (khác bug History). |
| 1.1.5 | Thời gian: Tháng này/Tháng trước | **PASS** | Tháng này=203; Tháng trước (T5)=627 phiếu (766.830.706+7.516.914.776−18.768.600=8.264.976.882 ✔). |
| 1.1.6 | Thời gian: tùy chọn ngày | **PASS** | Lịch (chọn ngày + Áp dụng). 10/05→31/05 = 508 phiếu, Tồn tính lại 871.448.982 (✔). |
| 1.1.7 | Lọc theo Người tạo | **PASS** | Chọn "cashier" → 59 phiếu đều do cashier tạo (✔ công thức). |
| 1.1.8 | Lọc theo Loại thu chi (Thu/Chi) | **PASS** | Phiếu chi→6 (Σ 1.179.745=Tổng chi); Phiếu thu→197 (Tổng chi 0). 197+6=203 ✓. *Lưu ý FIND-BALANCE.* |
| 1.1.9 | Lọc theo Phân loại thu chi | **PASS** | Dropdown: tiền bán hàng, thu khách, Tiền mặt bảng, Tiền điện nước, tiền bán hàng(trùng), Đi trễ. "Tiền mặt bảng"+cashier → 3 phiếu (Σ 154.745 ✔). |
| 1.1.10 | Lọc theo Loại nguồn | **FAIL/LỆCH** | Bộ lọc tên "Loại" CÓ và lọc được, nhưng giá trị là **vai trò** (Quản lý/Quầy bếp/Thu ngân/NV order/Khác), KHÔNG phải Bán hàng/Mua hàng/Tự tạo/Trả hàng như checklist. |
| 1.1.11 | Kết hợp nhiều bộ lọc | **PASS** | cashier + "Tiền mặt bảng" + Tháng này → đúng giao 3 phiếu; thẻ tổng quan cập nhật theo lọc. |

## 1.2 Tổng quan quỹ
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.2.1 | Tồn quỹ đầu kỳ | **PASS** | Hiển thị & đổi theo kỳ (T6 8.264.976.882 / tuần trước 8.974.156.053 / T5 766.830.706). |
| 1.2.2 | Tổng thu | **PASS** | Lọc Phiếu thu = 767.780.909; cộng tay Hôm qua 4.020.210 khớp. |
| 1.2.3 | Tổng chi | **PASS** | Lọc Phiếu chi: 6 phiếu Σ = 1.179.745 = thẻ Tổng chi. |
| 1.2.4 | Tồn cuối kỳ = đầu + thu − chi | **PASS** | Đúng ở **mọi** mốc đã kiểm (vd 8.264.976.882+767.780.909−1.179.745=9.031.578.046). |
| 1.2.5 | Đổi lọc thời gian → 4 thẻ cập nhật | **PASS** | Mọi lần đổi Hôm nay/Hôm qua/Tuần/Tháng/Tùy chọn đều cập nhật cả 4 thẻ. Tính liên tục: cuối kỳ trước = đầu kỳ sau (✔). |

## 1.3 Danh sách phiếu
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.3.1 | Bảng phiếu đủ cột | **PASS** | Đủ: Mã phiếu, Loại, Số tiền, Chi nhánh, Người nộp/nhận, Người tạo, Phân loại, PTTT, Đính kèm, Thời gian, Mô tả, Hành động. |
| 1.3.2 | Phân trang | **PASS** | 203 phiếu/11 trang, 20 dòng/trang; trang 1↔2 không trùng/thiếu; có \|< < … > >\|. |
| 1.3.3 | Bấm icon xem chi tiết | **PASS** | Icon mắt → modal "Chi tiết phiếu" đủ thông tin. *Lưu ý: Ngày tạo dạng raw ISO `2026-06-11T08:28:00.000000Z`.* |
| 1.3.4 | Phiếu có đính kèm | **N/A** | Không có phiếu nào có đính kèm trong dữ liệu mẫu; không tạo được (upload bị chặn). |

## 1.4 Thêm phiếu
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.4.1 | Bấm "Thêm" mở modal | **PASS** | Modal "Thêm phiếu" mở đủ field. |
| 1.4.2 | Mã phiếu tự sinh | **PASS\*** | Ô chỉ hiện "Mã tăng tự động", **không preview mã**; mã sinh sau khi Lưu (PC00001624…). |
| 1.4.3 | Bỏ trống Loại thu chi | **PASS** | Submit → popup ✗ "Vui lòng chọn loại thu chi", chặn lưu. |
| 1.4.4 | Bỏ trống Số tiền | **PASS** | Ô Số tiền viền đỏ + "Nhập số tiền", chặn lưu. |
| 1.4.5 | Chọn Loại đối tượng / Người nộp | **PASS\*** | "Loại nhân sự"=Thu ngân → Người nộp auto "casher2". |
| 1.4.6 | Chọn Phân loại thu chi | **PASS** | Auto điền theo Loại; đổi được. |
| 1.4.7 | Chọn PTTT | **PASS** | Mặc định "Tiền mặt"; đổi được Chuyển khoản/Quẹt Thẻ. |
| 1.4.8 | Nhập Số tiền | **PASS\*** | Ô không tự chèn dấu phẩy khi gõ ("10000"); lưu & hiển thị danh sách đúng "10.000đ". |
| 1.4.9 | Đính kèm tệp | **N/A (BLOCKED)** | Không upload được tệp qua tự động hóa. |
| 1.4.10 | Mô tả giới hạn 200 ký tự | **FAIL/LỆCH** | Bộ đếm "23/50" → **giới hạn 50**, không phải 200. |
| 1.4.11 | Bấm "Lưu" hợp lệ | **PASS** | Tạo Phiếu thu 10.000 (PC00001624) → "Tạo thành công", lên đầu DS, Tổng thu +10.000. |
| 1.4.12 | Bấm "Đóng" không tạo phiếu | **PASS** | Đóng bằng **icon X** (không có nút chữ "Đóng") → không tạo phiếu (Tổng giữ 206). |
| 1.4.13 | Mã tăng dần | **PASS** | PC00001624 = 1623+1; chuỗi PT tăng riêng. |
| 1.4.14 | Nhập Số tiền = 0 | **FAIL (BUG-01)** | **Vẫn tạo thành công** PT00000034 Chi 0đ; không chặn, không báo lỗi. |
| 1.4.15 | Loại đối tượng đổi → Người nộp đổi | **PASS\*** | Người nộp khóa theo "Loại nhân sự". *LỆCH: giá trị là vai trò, không phải Khách hàng/Nhân viên.* |
| 1.4.16 | Loại đối tượng chưa chọn → Người nộp | **PASS** | Chưa chọn Loại nhân sự → Người nộp "No data found". |
| 1.4.17 | Loại=Chi → label "Người nhận" | **FAIL/LỆCH** | Label luôn "Người nộp / Người nhận" (gộp), không đổi theo Thu/Chi. |
| 1.4.18 | Xóa file đính kèm | **N/A (BLOCKED)** | Phụ thuộc upload (1.4.9). |
| 1.4.19 | Lưu phiếu thu → Tồn quỹ tăng | **PASS** | Số dư 9.031.578.046→9.031.588.046 (+10.000 ✔). |
| 1.4.20 | Lưu phiếu chi → Tồn quỹ giảm | **PASS** | Phiếu chi 5.000 (PT00000035) → Tổng chi +5.000, Số dư −5.000 (✔). |

## 1.5 Ghi nhận 4 loại phiếu
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.5.1 | Tạo Phiếu thu thủ công | **PASS** | PC00001624 +10.000 vào Tổng thu & Số dư. |
| 1.5.2 | Tạo Phiếu chi thủ công | **PASS** | PT00000035 +5.000 Tổng chi, −5.000 Số dư. |
| 1.5.3 | Phiếu thu hiển thị đúng thông tin | **PASS** | Loại=Thu, 10.000, Người nộp casher2, tiền bán hàng, Tiền mặt, Mô tả khớp. |
| 1.5.4 | Phiếu chi hiển thị đúng thông tin | **PASS** | Loại=Chi, 5.000, tiền mặt bảng, Tiền mặt. |
| 1.5.5 | Hoàn tất đơn bán → tự sinh Phiếu bán hàng | **PASS** | Đơn ban1 (tran chau 10.000+VAT 500=10.500) Tiền mặt → tự sinh **phiếu Thu PC00001625 = 10.500đ**; Tổng thu +10.500. *Không có nhãn "Loại nguồn=Bán hàng" để xác nhận trực tiếp.* |
| 1.5.6 | Trả hàng → tự sinh Phiếu trả hàng | **BLOCKED** | Tab Trả hàng: **"Tính năng 'returns' đang phát triển"**. |
| 1.5.7 | Lọc Loại nguồn = Bán hàng | **FAIL/BLOCKED** | Không có bộ lọc "Loại nguồn" (xem 1.1.10). |
| 1.5.8 | Lọc Loại nguồn = Trả hàng | **FAIL/BLOCKED** | Như trên. |
| 1.5.9 | Lọc Loại nguồn = Tự tạo | **FAIL/BLOCKED** | Như trên. |
| 1.5.10 | Số tiền phiếu bán hàng khớp đơn gốc | **PASS** | 10.500 = tổng thanh toán đơn PO015062036. |
| 1.5.11 | Số tiền phiếu trả hàng khớp đơn gốc | **BLOCKED** | Do 1.5.6 (returns chưa có). |
| 1.5.12 | PTTT phiếu tự sinh khớp đơn gốc | **PASS** | Tiền mặt = PTTT đơn. |
| 1.5.13 | Đơn bán bị hủy → phiếu không tính quỹ | **PASS** | Điều phối ca: PO…031/034/035 "Đã hủy", 0đ, không sinh phiếu thu tính quỹ. |
| 1.5.14 | Số liệu Thu chi khớp Điều phối ca | **PASS** | Khớp 100%: PC00001625 Thu 10.500 Tiền mặt; PT00000035 Chi 5.000; PC00001624 Thu 10.000 — đều trùng 2 màn hình. |
| 1.5.15 | Tổng thu = Σ nguồn thu | **PASS** | Lọc Phiếu thu = 767.790.909 (gồm thủ công + bán hàng). |
| 1.5.16 | Tổng chi = Σ nguồn chi | **PASS** | Lọc Phiếu chi: Σ phiếu = Tổng chi 1.184.745. |

## 1.6 Xuất Excel
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.6.1 | Bấm "Xuất Excel" | **PASS** | Popup ✓ "Đã xuất file, đang tải xuống trình duyệt." → kích hoạt tải file. |
| 1.6.2 | File xuất đúng dữ liệu theo bộ lọc | **N/A-một phần** | Export chạy theo bộ lọc đang áp; KHÔNG mở/đối chiếu được nội dung file (file tải về máy người dùng). |

## 1.7 Công nợ (tab Quản lý công nợ)
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.7.1 | Mở tab Công nợ | **PASS** | Mở màn Công nợ + panel "Bộ Lọc"; chip Tất cả(50)/Gần đến hạn/Quá hạn(14)/Hôm nay. |
| 1.7.2 | Đối tượng mặc định | **PASS** | 2 checkbox Khách hàng + Nhà cung cấp, mặc định cả 2 tích. |
| 1.7.3 | Lọc chỉ Khách hàng | **PASS** | Bỏ tích NCC → 49 dòng đều Khách hàng. |
| 1.7.4 | Lọc chỉ Nhà cung cấp | **PASS** | Bỏ tích KH → 1 dòng NCC (49+1=50 ✓). |
| 1.7.5 | Bỏ tích cả 2 đối tượng | **FAIL/LỆCH** | Hiển thị **TẤT CẢ 50** (coi như không lọc), không rỗng như mong đợi. |
| 1.7.6 | Tìm theo Tên đối tượng | **PASS** | "aaaa" → 8 dòng tên chứa "aaaa" (khớp chuỗi con). |
| 1.7.7 | Tìm theo Mã công nợ | **PASS\*** | Ô lọc hoạt động (không khớp → rỗng); nhưng cột "Mã công nợ" **trống** → không có dữ liệu thử khớp dương. |
| 1.7.8 | Lọc theo Chi nhánh | **PASS** | cn11 → "Không có dữ liệu" (mọi nợ thuộc CN1). |
| 1.7.9 | Lọc theo Người tạo | **PASS** | "Admin master" → 48 (lọc bỏ 1 dòng của user khác). |
| 1.7.10 | Kết hợp nhiều bộ lọc | **PASS** | Khách hàng + Tên "aaaa" → giao 8 dòng. |
| 1.7.11 | Bảng công nợ đủ thông tin | **PASS** | Đủ cột; có Trạng thái (TT một phần/đủ, "Đã quá hạn N ngày"). *Cột "Mã công nợ" để trống.* |
| 1.7.12 | Xem chi tiết công nợ | **PASS** | Icon bút chì (chỉ ở nợ chưa trả đủ) → modal "Thanh toán nợ" đúng đối tượng (tran van a, SĐT, Còn lại 960.000). |
| 1.7.13 | (placeholder) | **N/A** | Không có nội dung trong checklist. |

---

## Tổng hợp
- **Tổng số testcase đã chạy:** 70 (1.1→1.7, gồm 1 placeholder 1.7.13).
- **PASS:** **56** (gồm các PASS\* đạt-nhưng-có-lưu-ý).
- **FAIL / LỆCH:** **8** — 1.4.14 (BUG-01 thật) · 1.1.10, 1.5.7, 1.5.8, 1.5.9 (thiếu bộ lọc "Loại nguồn") · 1.4.10 (giới hạn 50≠200) · 1.4.17 (label không đổi) · 1.7.5 (bỏ tích cả 2 → hiện tất cả).
- **BLOCKED:** **2** — 1.5.6, 1.5.11 (Trả hàng "đang phát triển").
- **N/A:** **5** — 1.3.4, 1.4.9, 1.4.18 (upload tệp) · 1.6.2 (nội dung file) · 1.7.13 (placeholder).

## Danh sách lỗi & phát hiện (chi tiết: `screenshot/0616_1305_cashboot/note.md`)
1. **BUG-01 (NẶNG, 1.4.14):** Phiếu **Số tiền = 0 vẫn tạo thành công** (PT00000034 Chi 0đ) → cho phép dữ liệu rác vào quỹ. **Ưu tiên fix.**
2. **LỆCH-01 (1.1.10/1.5.7–9):** Không có bộ lọc "Loại nguồn" (Bán/Mua/Tự tạo/Trả) — bộ lọc "Loại" chỉ theo vai trò. Cần bổ sung hoặc đồng bộ checklist.
3. **LỆCH-02 (1.4.10):** Mô tả giới hạn 50 ký tự (checklist ghi 200).
4. **LỆCH-03 (1.4.17):** Label luôn "Người nộp / Người nhận", không đổi theo Thu/Chi.
5. **LỆCH-04 (1.7.5):** Công nợ bỏ tích cả 2 đối tượng → hiện tất cả thay vì rỗng.
6. **FIND-BALANCE:** "Tồn đầu kỳ"/"Số dư cuối ca" tính lại theo bộ lọc Thu/Chi → dễ gây hiểu nhầm số dư.
7. **FIND-DROPDOWN (UX):** Dropdown bộ lọc/biểu mẫu hay kẹt "lớp phủ ma", phải tải lại trang.
8. **Nhỏ:** mã phiếu không preview (1.4.2); số tiền không format khi gõ (1.4.8); ngày tạo raw ISO (1.3.3); cột "Mã công nợ" trống (1.7.11); nhấn Enter ở ô Mã phiếu gây nhảy trang (1.1.1).
9. **Môi trường:** màn hình thỉnh thoảng đơ khi tự động hóa (timeout chụp ảnh) — không phải lỗi sản phẩm.

## Khuyến nghị
1. **Ưu tiên fix BUG-01** (chặn Số tiền ≤ 0 khi tạo phiếu).
2. Bổ sung **bộ lọc "Loại nguồn"** (Bán hàng/Mua hàng/Tự tạo/Trả hàng) hoặc đồng bộ lại checklist với UI hiện tại ("Loại" = vai trò).
3. Sửa **giới hạn Mô tả** (50 vs 200) và **label Người nộp/Người nhận** theo Thu/Chi cho khớp checklist; xem lại logic **bỏ tích cả 2 đối tượng** (Công nợ).
4. Cân nhắc giữ **"Tồn đầu kỳ" cố định** khi lọc theo Loại thu chi (tránh hiểu nhầm số dư).
5. Hoàn thiện **tab Trả hàng** để kiểm thử phiếu trả hàng (1.5.6/1.5.11).
6. Cải thiện UX **dropdown** (đóng overlay, chọn 1 lần); format **ngày tạo** & **số tiền khi nhập**; preview **mã phiếu** trong modal.
7. Phiên sau (nếu cần đầy đủ): chuẩn bị **tệp đính kèm** để test 1.3.4/1.4.9/1.4.18 và môi trường cho phép mở file Excel để đối chiếu 1.6.2.

## Dữ liệu test đã tạo trong phiên (để dọn nếu cần)
- PC00001624CN2 — Thu 10.000 (Mô tả "TEST QA cashboot 1.4.11")
- PT00000034CN2 — Chi 0đ (từ BUG-01)
- PT00000035CN2 — Chi 5.000
- Đơn bán PO015062036CN2 (ban1, 10.500 Tiền mặt) → sinh phiếu thu PC00001625CN2 (10.500)
</content>
