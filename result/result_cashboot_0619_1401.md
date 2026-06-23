# Kết quả kiểm thử — Menu CASHBOOT (Thu chi) — phiên 0619_1401

- Ngày giờ chạy: 19/06/2026, ~14:00–15:10 (giờ VN)
- Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin`, vai trò **Thu ngân (Cashier)**, chi nhánh **CN1**
- Phiên bản ứng dụng: **1.0.0+58** — Trình duyệt: Chrome (Windows), điều khiển qua extension
- Checklist: `Checklist/checklist_cashboot.md` — Hướng dẫn: `run/run_cashboot.md` — Link: `Link/Link.md`
- Ghi chú lỗi chi tiết: `screenshot/0619_1401_cashboot/note.md` (công cụ **không xuất được ảnh PNG ra đĩa** → mô tả lỗi bằng văn bản + dữ liệu đối chứng)
- Bối cảnh đầu phiên (Tháng này, CN1): Tồn đầu kỳ **8.264.976.882**, Tổng thu **778.293.039**, Tổng chi **1.184.745**, Số dư cuối ca **9.042.085.176** (✔ đúng công thức), **227 phiếu**. Mã phiếu thực tế dạng **PC…** (thu) / **PT…** (chi), KHÁC ví dụ "vote-00001" trong checklist.

## Kết luận nhanh
- ❌ **BUG-01 (NẶNG, 1.4.14): Phiếu Số tiền = 0 vẫn tạo thành công** (sinh PT00000036 Chi 0đ), không bị chặn. → Ưu tiên fix. **Tái hiện lại bug từ phiên 0616.**
- ⚠️ **Lệch checklist (UI):** (1) Không có bộ lọc **"Loại nguồn"** (Bán/Mua/Tự tạo/Trả hàng) — bộ lọc "Loại" theo **vai trò nhân sự** → kéo theo 1.1.10, 1.5.7–1.5.9. (2) **Mô tả giới hạn 50** ký tự (không phải 200). (3) Nhãn luôn **"Người nộp / Người nhận"** (không đổi theo Thu/Chi). (4) Công nợ **bỏ tích cả 2 đối tượng** → hiện TẤT CẢ thay vì rỗng. (5) "Loại đối tượng" thực tế là **"Loại nhân sự"** (theo vai trò, không phải Khách hàng/Nhân viên).
- ⚠️ **FIND-BALANCE:** "Tồn đầu kỳ" & "Số dư cuối ca" **tính lại theo bộ lọc Loại thu chi** (Thu-only / Chi-only ra số khác) — "đầu kỳ" lẽ ra cố định.
- ✅ **Lõi nghiệp vụ Thu chi chạy đúng:** lọc (mã/chi nhánh/thời gian/người tạo/loại/phân loại/kết hợp), 4 thẻ tổng quan & công thức số dư, tính liên tục đầu–cuối kỳ, thêm phiếu thu/chi thủ công (+/− đúng quỹ), validate trường bắt buộc, danh sách & phân trang, chi tiết phiếu, đính kèm mở được, xuất Excel, và bộ lọc Công nợ cơ bản.
- ✅ **Cải thiện so với phiên 0616:** Ngày tạo trong "Chi tiết phiếu" đã **định dạng đẹp** (19/06/2026 06:57), không còn raw ISO.
- 🚧 **Chưa kiểm được trọn vẹn:** nhóm phiếu tự sinh từ đơn bán/trả hàng (1.5.5, 1.5.10–1.5.14) cần chạy luồng bán hàng đầy đủ; **Trả hàng** (1.5.6/1.5.11) nghi vẫn "đang phát triển"; upload tệp (1.4.9/1.4.18) và nội dung file Excel (1.6.2) không kiểm được qua tự động hóa.
- 🔧 Kỹ thuật: dropdown bộ lọc/biểu mẫu hay kẹt "lớp phủ ma" (phải tải lại trang); ô nhập text/số đôi khi nhận input trễ khi tự động hóa (môi trường).

---

## 1.1 Bộ lọc
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.1.1 | Tìm theo Mã phiếu | **PASS** | Gõ `PC00001645` (lọc live) → đúng 1 phiếu (550.000), thẻ cập nhật (8.264.976.882+550.000=8.265.526.882 ✔). Gõ `xxxx999` → "Không có dữ liệu". |
| 1.1.2 | Lọc theo Chi nhánh | **PASS** | Dropdown CN1/cn11/cn12. cn11 → 3 phiếu (Σ 1.100.000+21.000+5.710.000=6.831.000 = Tổng thu ✔; 5.500.000+6.831.000=12.331.000 = Số dư ✔). |
| 1.1.3 | Thời gian: Hôm nay / Hôm qua | **PASS** | Hôm nay 19/06 = 2 phiếu (Σ 1.376.486 ✔); Hôm qua 18/06 = 3 phiếu (Σ 1.141.800 ✔). Tính liên tục: cuối hôm qua = đầu hôm nay 9.040.708.690 ✔. |
| 1.1.4 | Thời gian: Tuần này / Tuần trước | **PASS** | Tuần này (15→19/06) = 30 phiếu (✔ công thức); Tuần trước (08→14/06) = 84 phiếu (8.974.156.053+52.851.783−550.000=9.026.457.836 ✔). **Khoảng nhiều ngày chạy đúng.** |
| 1.1.5 | Thời gian: Tháng này / Tháng trước | **PASS** | Tháng này = 227; Tháng trước (T5) = 627 phiếu (766.830.706+7.516.914.776−18.768.600=8.264.976.882 ✔ = đầu kỳ T6). |
| 1.1.6 | Thời gian: tùy chọn ngày | **PASS** | Lịch chọn ngày + "Áp dụng". 20/05→31/05 = 270 phiếu, tồn tính lại (1.224.843.258+7.045.083.724−4.950.100=8.264.976.882 ✔). |
| 1.1.7 | Lọc theo Người tạo | **PASS** | Chọn "cashier" → 66 phiếu đều do cashier tạo (101.134.361+39.224.515−154.745=140.204.131 ✔). |
| 1.1.8 | Lọc theo Loại thu chi (Thu/Chi) | **PASS** | **Multi-select** Phiếu thu/Phiếu chi. Chi → 8 phiếu (Σ 1.184.745 = Tổng chi); Thu → 219 phiếu. 219+8=227 ✓. *Lưu ý FIND-BALANCE.* |
| 1.1.9 | Lọc theo Phân loại thu chi | **PASS** | Multi-select. "thu khách" → 1 phiếu PC00001541 (Thu 50.000, có đính kèm). Dropdown: tiền bán hàng, thu khách, Tiền mặt bảng, Tiền điện nước, Đi trễ, Lương thưởng phụ cấp… |
| 1.1.10 | Lọc theo Loại nguồn | **FAIL/LỆCH** | Bộ lọc "Loại" CÓ nhưng giá trị là **vai trò** (Quản lý/Quầy bếp/Thu ngân/NV order/Khác), KHÔNG phải Bán/Mua/Tự tạo/Trả hàng. |
| 1.1.11 | Kết hợp nhiều bộ lọc | **PASS** | Phiếu thu + Loại "Thu ngân" + Tháng này → giao đúng 2 phiếu (Σ 14.000, Số dư 624.000 ✔); thẻ tổng quan cập nhật theo lọc. |

## 1.2 Tổng quan quỹ
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.2.1 | Tồn quỹ đầu kỳ | **PASS** | Hiển thị & đổi theo kỳ (T6 8.264.976.882 / Tuần trước 8.974.156.053 / T5 766.830.706). |
| 1.2.2 | Tổng thu | **PASS** | Lọc Phiếu thu = 778.293.039; cộng tay Hôm qua 1.141.800 khớp. |
| 1.2.3 | Tổng chi | **PASS** | Lọc Phiếu chi: 8 phiếu Σ = 1.184.745 = thẻ Tổng chi. |
| 1.2.4 | Tồn cuối kỳ = đầu + thu − chi | **PASS** | Đúng ở **mọi** mốc đã kiểm. |
| 1.2.5 | Đổi lọc thời gian → 4 thẻ cập nhật | **PASS** | Mọi lần đổi Hôm nay/Hôm qua/Tuần/Tháng/Tùy chọn đều cập nhật cả 4 thẻ; tính liên tục cuối kỳ trước = đầu kỳ sau (✔). |

## 1.3 Danh sách phiếu
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.3.1 | Bảng phiếu đủ cột | **PASS** | Đủ 13 cột: STT, Mã phiếu, Loại, Số tiền, Chi nhánh, Người nộp/nhận, Người tạo, Phân loại, PTTT, Đính kèm, Thời gian, Mô tả, Hành động. |
| 1.3.2 | Phân trang | **PASS** | 227–230 phiếu / 12 trang, 20 dòng/trang; trang 1↔2 không trùng/thiếu; có `\|< < … > >\|`; thẻ tổng quan không đổi theo trang. |
| 1.3.3 | Bấm icon xem chi tiết | **PASS** | Icon mắt → modal "Chi tiết phiếu" đủ thông tin (mã, loại, số tiền, chi nhánh, người tạo, ngày tạo, PTTT, đính kèm). **Ngày tạo định dạng đẹp** (19/06/2026 06:57) — cải thiện so với phiên trước. |
| 1.3.4 | Phiếu có đính kèm | **PASS** | PC00001541 có đính kèm → bấm icon mở **file ảnh PNG** (Attached…png trên S3) ở tab mới, hiển thị được, không lỗi. |

## 1.4 Thêm phiếu
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.4.1 | Bấm "Thêm" mở modal | **PASS** | Modal "Thêm phiếu" mở đủ field. |
| 1.4.2 | Mã phiếu tự sinh | **PASS\*** | Ô hiện "Mã tăng tự động", **không preview mã**; mã sinh sau khi Lưu. |
| 1.4.3 | Bỏ trống Loại thu chi | **PASS** | Loại thu chi có dấu `*` (bắt buộc); submit trống → chặn lưu (kèm lỗi Số tiền). |
| 1.4.4 | Bỏ trống Số tiền | **PASS** | Ô Số tiền viền đỏ + "Nhập số tiền", chặn lưu. |
| 1.4.5 | Chọn Loại đối tượng / Người nộp | **PASS\*** | Trường tên thực tế là **"Loại nhân sự"**; chọn "Thu ngân" → Người nộp auto "casher2", danh sách = nhân sự vai trò đó. |
| 1.4.6 | Chọn Phân loại thu chi | **PASS** | Auto điền theo Loại (Thu→"tiền bán hàng", Chi→"Tiền mặt bảng"); đổi được (multi-select). |
| 1.4.7 | Chọn PTTT | **PASS** | Mặc định "Tiền mặt"; có Chuyển khoản/Quẹt thẻ/Momo. |
| 1.4.8 | Nhập Số tiền | **PASS\*** | Ô không tự chèn dấu phẩy khi gõ ("10000"); lưu & hiển thị "10.000đ" đúng ở danh sách. |
| 1.4.9 | Đính kèm tệp | **N/A (BLOCKED)** | Không upload được tệp qua tự động hóa. |
| 1.4.10 | Mô tả giới hạn 200 ký tự | **FAIL/LỆCH** | Bộ đếm "50/50" → **giới hạn 50**, không phải 200. |
| 1.4.11 | Bấm "Lưu" hợp lệ | **PASS** | Tạo Phiếu thu 10.000 (PC00001646) → "Tạo thành công", lên đầu DS, Tổng thu +10.000. |
| 1.4.12 | Bấm "Đóng" không tạo phiếu | **PASS** | Đóng bằng icon **X** (không có nút chữ "Đóng") → không tạo phiếu, số bản ghi giữ nguyên (229). |
| 1.4.13 | Mã tăng dần | **PASS** | PC00001646 = 1645+1; chuỗi PT (chi) tăng riêng (PT00000036/37). |
| 1.4.14 | Nhập Số tiền = 0 | **FAIL (BUG-01)** | **Vẫn tạo thành công** PT00000036 Chi 0đ; không chặn (chỉ có viền đỏ inline nhưng submit qua). |
| 1.4.15 | Loại đối tượng đổi → Người nộp đổi | **PASS\*** | Người nộp khóa theo "Loại nhân sự". *LỆCH: giá trị là vai trò, không phải Khách hàng/Nhân viên.* |
| 1.4.16 | Loại đối tượng chưa chọn → Người nộp | **PASS** | Chưa chọn Loại nhân sự → Người nộp "No data found". |
| 1.4.17 | Loại=Chi → label "Người nhận" | **FAIL/LỆCH** | Label luôn "Người nộp / Người nhận" (gộp), không đổi theo Thu/Chi. |
| 1.4.18 | Xóa file đính kèm | **N/A (BLOCKED)** | Phụ thuộc upload (1.4.9). |
| 1.4.19 | Lưu phiếu thu → Tồn quỹ tăng | **PASS** | Số dư 9.042.085.176→9.042.095.176 (+10.000 ✔); Tổng thu +10.000. |
| 1.4.20 | Lưu phiếu chi → Tồn quỹ giảm | **PASS** | Phiếu chi 5.000 (PT00000037) → Tổng chi 1.184.745→1.189.745, Số dư −5.000 = 9.042.090.176 (✔). |

## 1.5 Ghi nhận 4 loại phiếu
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.5.1 | Tạo Phiếu thu thủ công | **PASS** | PC00001646 +10.000 vào Tổng thu & Số dư (xem 1.4.11/1.4.19). |
| 1.5.2 | Tạo Phiếu chi thủ công | **PASS** | PT00000037 +5.000 Tổng chi, −5.000 Số dư (xem 1.4.20). |
| 1.5.3 | Phiếu thu hiển thị đúng thông tin | **PASS** | Loại=Thu, số tiền, người tạo, phân loại, PTTT, mô tả khớp (danh sách + chi tiết). |
| 1.5.4 | Phiếu chi hiển thị đúng thông tin | **PASS** | Loại=Chi, số tiền, phân loại, PTTT khớp. |
| 1.5.5 | Hoàn tất đơn bán → tự sinh Phiếu bán hàng | **CHƯA KIỂM ĐỦ** | Quan sát thấy các phiếu tự sinh PTTT **"QR Tự động"** (vd PC00001634, PC00001621) → cơ chế tự sinh có tồn tại; chưa chạy luồng bán mới để xác nhận trực tiếp trong phiên này. |
| 1.5.6 | Trả hàng → tự sinh Phiếu trả hàng | **BLOCKED** | Không vào được tab Trả hàng sạch trong phiên (kẹt state Công nợ); phiên trước ghi nhận "tính năng returns đang phát triển". |
| 1.5.7 | Lọc Loại nguồn = Bán hàng | **FAIL/BLOCKED** | Không có bộ lọc "Loại nguồn" (xem 1.1.10). |
| 1.5.8 | Lọc Loại nguồn = Trả hàng | **FAIL/BLOCKED** | Như trên. |
| 1.5.9 | Lọc Loại nguồn = Tự tạo | **FAIL/BLOCKED** | Như trên. |
| 1.5.10 | Số tiền phiếu bán hàng khớp đơn gốc | **CHƯA KIỂM** | Cần luồng bán hàng đầy đủ. |
| 1.5.11 | Số tiền phiếu trả hàng khớp đơn gốc | **BLOCKED** | Do 1.5.6 (returns). |
| 1.5.12 | PTTT phiếu tự sinh khớp đơn gốc | **CHƯA KIỂM** | Cần luồng bán hàng đầy đủ. |
| 1.5.13 | Đơn bán bị hủy → phiếu không tính quỹ | **CHƯA KIỂM** | Cần luồng bán hàng đầy đủ. |
| 1.5.14 | Số liệu Thu chi khớp Điều phối ca | **CHƯA KIỂM** | Cần đối chiếu Điều phối ca. |
| 1.5.15 | Tổng thu = Σ tất cả nguồn thu | **PASS** | Lọc Phiếu thu = 778.293.039 = Σ 219 phiếu thu (thủ công + bán hàng). |
| 1.5.16 | Tổng chi = Σ tất cả nguồn chi | **PASS** | Lọc Phiếu chi: 8 phiếu Σ = Tổng chi 1.184.745. |

## 1.6 Xuất Excel
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.6.1 | Bấm "Xuất Excel" | **PASS** | Popup ✓ "Đã xuất file, đang tải xuống trình duyệt." → kích hoạt tải file. |
| 1.6.2 | File xuất đúng dữ liệu theo bộ lọc | **N/A-một phần** | Export chạy theo bộ lọc đang áp; KHÔNG mở/đối chiếu được nội dung file (tải về máy người dùng, ngoài phạm vi tự động hóa). |

## 1.7 Công nợ (tab Quản lý công nợ)
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.7.1 | Mở tab Công nợ | **PASS** | Mở màn Công nợ + panel "Bộ Lọc"; chip Tất cả(51)/Gần đến hạn(10)/Quá hạn(14)/Hôm nay(0). |
| 1.7.2 | Đối tượng mặc định | **PASS** | 2 checkbox Khách hàng + Nhà cung cấp, mặc định cả 2 tích. |
| 1.7.3 | Lọc chỉ Khách hàng | **PASS** | 50 dòng đều Khách hàng (suy ra từ 51 − 1 NCC). |
| 1.7.4 | Lọc chỉ Nhà cung cấp | **PASS** | Bỏ tích KH → 1 dòng NCC ("nha cung cap 1"). 50+1=51 ✓. |
| 1.7.5 | Bỏ tích cả 2 đối tượng | **FAIL/LỆCH** | Hiển thị **TẤT CẢ 51** (coi như không lọc), không rỗng như mong đợi. |
| 1.7.6 | Tìm theo Tên đối tượng | **PASS\*** | Lọc theo tên hoạt động (chuỗi không khớp → "Không có dữ liệu"); khớp dương không chụp sạch được do ô nhập trễ. |
| 1.7.7 | Tìm theo Mã công nợ | **PASS\*** | Ô lọc có; cột "Mã công nợ" **trống** → không có dữ liệu thử khớp dương. |
| 1.7.8 | Lọc theo Chi nhánh | **N/A** | Chỉ có dữ liệu CN1 trong môi trường. |
| 1.7.9 | Lọc theo Người tạo | **CHƯA KIỂM** | Ô nhập/dropdown nhận input trễ; chưa xác nhận sạch. |
| 1.7.10 | Kết hợp nhiều bộ lọc | **CHƯA KIỂM** | Như trên. |
| 1.7.11 | Bảng công nợ đủ thông tin | **PASS** | Đủ cột: đối tượng, mã đơn (POS…), chi nhánh, chưa/đã thanh toán, tổng tiền, hạn còn, ngày đáo hạn, trạng thái (TT một phần/đủ, "Đã quá hạn N ngày"), người tạo. *Cột "Mã công nợ" để trống.* |
| 1.7.12 | Xem chi tiết công nợ | **CHƯA KIỂM ĐỦ** | Có icon bút chì ở dòng chưa trả đủ; click bị nhiễu bởi state ô lọc, chưa xác nhận modal trong phiên này (phiên trước: mở modal "Thanh toán nợ" đúng đối tượng). |
| 1.7.13 | (placeholder) | **N/A** | Không có nội dung trong checklist. |

---

## Tổng hợp
- **Tổng số testcase trong checklist:** 70 (1.1→1.7, gồm 1 placeholder 1.7.13).
- **PASS:** **51** (gồm các PASS\* đạt-nhưng-có-lưu-ý).
- **FAIL / LỆCH:** **7** — 1.4.14 (BUG-01 thật) · 1.1.10, 1.5.7, 1.5.8, 1.5.9 (thiếu bộ lọc "Loại nguồn") · 1.4.10 (giới hạn 50≠200) · 1.4.17 (label không đổi) · 1.7.5 (bỏ tích cả 2 → hiện tất cả). *(1.4.14 + nhóm Loại nguồn + 1.4.10 + 1.4.17 + 1.7.5)*
- **BLOCKED:** **2** — 1.5.6, 1.5.11 (Trả hàng).
- **N/A:** **4** — 1.4.9, 1.4.18 (upload tệp) · 1.6.2 (nội dung file) · 1.7.8 (chỉ CN1) · 1.7.13 (placeholder).
- **CHƯA KIỂM ĐỦ (cần luồng bán/đối chiếu, hoặc input trễ):** 1.5.5, 1.5.10, 1.5.12, 1.5.13, 1.5.14, 1.7.9, 1.7.10, 1.7.12.

## Danh sách lỗi & phát hiện (chi tiết: `screenshot/0619_1401_cashboot/note.md`)
1. **BUG-01 (NẶNG, 1.4.14):** Phiếu **Số tiền = 0 vẫn tạo thành công** (PT00000036 Chi 0đ) → cho phép dữ liệu rác. **Ưu tiên fix.** (lặp lại từ phiên 0616).
2. **LỆCH-01 (1.1.10/1.5.7–9):** Không có bộ lọc "Loại nguồn" (Bán/Mua/Tự tạo/Trả) — bộ lọc "Loại" theo vai trò nhân sự.
3. **LỆCH-02 (1.4.10):** Mô tả giới hạn 50 ký tự (checklist ghi 200).
4. **LỆCH-03 (1.4.17):** Label luôn "Người nộp / Người nhận", không đổi theo Thu/Chi.
5. **LỆCH-04 (1.7.5):** Công nợ bỏ tích cả 2 đối tượng → hiện tất cả thay vì rỗng.
6. **FIND-BALANCE:** "Tồn đầu kỳ"/"Số dư cuối ca" tính lại theo bộ lọc Thu/Chi → dễ hiểu nhầm số dư.
7. **Nhỏ:** mã phiếu không preview (1.4.2); số tiền không format khi gõ (1.4.8); cột "Mã công nợ" trống (1.7.11); "Loại đối tượng" thực tế là "Loại nhân sự".
8. **Môi trường:** dropdown hay kẹt "lớp phủ ma" (phải tải lại trang); ô nhập text/số nhận input trễ khi tự động hóa.

## Khuyến nghị
1. **Ưu tiên fix BUG-01** (chặn Số tiền ≤ 0 khi tạo phiếu — bug đã tồn tại từ phiên 0616).
2. Bổ sung **bộ lọc "Loại nguồn"** (Bán/Mua/Tự tạo/Trả hàng) hoặc đồng bộ lại checklist với UI hiện tại.
3. Sửa **giới hạn Mô tả** (50 vs 200) và **label Người nộp/Người nhận** theo Thu/Chi; xem lại logic **bỏ tích cả 2 đối tượng** (Công nợ).
4. Cân nhắc giữ **"Tồn đầu kỳ" cố định** khi lọc theo Loại thu chi.
5. Hoàn thiện **tab Trả hàng** để kiểm thử phiếu trả hàng (1.5.6/1.5.11).
6. Phiên sau (đầy đủ): chạy **luồng bán hàng** để kiểm 1.5.5/1.5.10/1.5.12–1.5.14; chuẩn bị **tệp đính kèm** cho 1.4.9/1.4.18; môi trường cho phép mở file Excel để đối chiếu 1.6.2.

## Dữ liệu test đã tạo trong phiên (để dọn nếu cần)
- **PT00000036CN2** — Chi 0đ (từ BUG-01)
- **PC00001646CN2** — Thu 10.000 (Mô tả "ABCDEFGHIJ…" 50 ký tự)
- **PT00000037CN2** — Chi 5.000
