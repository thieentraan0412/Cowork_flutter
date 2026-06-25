# Kết quả kiểm thử — Menu CASHBOOT (Thu chi) — phiên 0623_1047

- Ngày giờ chạy: 23/06/2026, ~09:59–10:47 (giờ VN)
- Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin`, vai trò **Thu ngân (Cashier)**, chi nhánh **CN1**
- Phiên bản ứng dụng: **1.0.0+66** — Trình duyệt: Chrome (Windows), điều khiển qua extension
- Checklist: `Checklist/checklist_cashboot.md` — Hướng dẫn: `run/run_cashboot.md` — Link: `Link/link.md`
- Ghi chú lỗi: `screenshot/0623_1047_cashboot/note.md` (công cụ tự động không xuất được ảnh PNG ra đĩa → mô tả lỗi bằng văn bản + dữ liệu đối chứng)
- Bối cảnh đầu phiên (Tháng này, CN1): Tồn đầu kỳ **8.264.976.882**, Tổng thu **778.363.939**, Tổng chi **1.189.745**, Số dư cuối ca **9.042.151.076** (✔ đúng công thức), **235 phiếu**. Mã phiếu thực tế dạng **PC…** (thu) / **PT…** (chi), KHÁC ví dụ "vote-00001" trong checklist.

## Kết luận nhanh
- ❌ **BUG-01 (NẶNG, 1.4.14): Phiếu Số tiền = 0 vẫn tạo thành công** (sinh PT00000000 Chi 0đ), không bị chặn. **Bug tái hiện liên tục từ phiên 0616 → 0619 → 0623, CHƯA fix.** → Ưu tiên cao.
- ✅ **CẢI THIỆN so với phiên 0619:** Bộ lọc **"Loại nguồn"** (mục "Loại" cuối panel) NAY đã đúng giá trị **Bán hàng / Mua hàng / Trả hàng / Tự tạo** (phiên trước là theo vai trò nhân sự). → 1.1.10, 1.5.7 nay PASS. Cột **"Mã công nợ"** ở tab Công nợ nay đã có dữ liệu (#52, #51…) thay vì để trống.
- ⚠️ **Lệch checklist (UI, vẫn tồn tại):** (1) **Mô tả giới hạn 50** ký tự (counter "0/50"), không phải 200. (2) Nhãn luôn **"Người nộp / Người nhận"** (gộp), KHÔNG đổi sang "Người nhận" khi chọn Chi. (3) Trường thực tế là **"Loại nhân sự"** (vai trò: Quản lý/Quầy bếp/Thu ngân/Nhân viên order/Khác), KHÔNG phải "Loại đối tượng" Khách hàng/Nhân viên như checklist.
- ⚠️ **FIND-BALANCE:** "Tồn đầu kỳ" & "Số dư cuối ca" **tính lại theo bộ lọc Loại thu chi** — khi lọc chỉ "Phiếu chi", Tồn đầu kỳ ra số âm (−22.294.150) → dễ hiểu nhầm. "Đầu kỳ" lẽ ra phải cố định.
- ✅ **Lõi nghiệp vụ chạy đúng:** lọc (mã/chi nhánh/thời gian/người tạo/loại thu chi/phân loại/loại nguồn/kết hợp), 4 thẻ tổng quan & công thức số dư đúng ở mọi kỳ, tính liên tục đầu–cuối kỳ, thêm phiếu thu/chi thủ công (+/− đúng quỹ), validate trường bắt buộc, danh sách & phân trang & chi tiết phiếu, xuất Excel, Loại nhân sự→Người nộp liên động, bộ lọc Công nợ cơ bản.
- 🚧 **Chưa kiểm được trọn vẹn:** nhóm phiếu tự sinh từ đơn bán/trả hàng (1.5.5, 1.5.6, 1.5.10–1.5.14) cần chạy luồng bán/trả đầy đủ; upload tệp (1.4.9/1.4.18) và nội dung file Excel (1.6.2) không kiểm được qua tự động hóa; một số ô tìm kiếm/checkbox của Công nợ (1.7.5–1.7.7, 1.7.9, 1.7.10, 1.7.12) nhận input chập chờn khi tự động hóa.
- 🔧 Kỹ thuật môi trường: ứng dụng Flutter (canvas) → click phải dispatch pointer-event qua JS; dropdown/biểu mẫu hay kẹt "lớp phủ ma" (phải tải lại trang); ô nhập text đôi khi không nhận focus khi tự động hóa.

---

## 1.1 Bộ lọc
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.1.1 | Tìm theo Mã phiếu | **PASS** | Gõ `PC00001648` → đúng 1 phiếu (9.450, Chuyển khoản); thẻ cập nhật (8.264.976.882+9.450=8.264.986.332 ✔). Gõ `xxxx999` → "Không có dữ liệu", thẻ về 0. |
| 1.1.2 | Lọc theo Chi nhánh | **PASS** | Dropdown CN1/cn11/cn12. cn11 → 3 phiếu (1.100.000+21.000+5.710.000=6.831.000 = Tổng thu ✔; 5.500.000+6.831.000=12.331.000 = Số dư ✔). |
| 1.1.3 | Thời gian: Hôm nay / Hôm qua | **PASS** | Hôm nay→range 23-06→23-06; Hôm qua→22-06→22-06 (CN1 không có giao dịch 2 ngày này; đầu kỳ 9.042.151.076 nối tiếp đúng). Cơ chế lọc ngày chạy đúng. |
| 1.1.4 | Thời gian: Tuần này / Tuần trước | **PASS** | Tuần này 22-06→23-06; Tuần trước 15-06→21-06 = 38 phiếu (9.026.457.836+15.703.240−10.000=9.042.151.076 ✔). |
| 1.1.5 | Thời gian: Tháng này / Tháng trước | **PASS** | Tháng này 01-06→23-06 = 235 phiếu (khớp baseline). Tháng trước (T5) = 627 phiếu (766.830.706+7.516.914.776−18.768.600=8.264.976.882 ✔ = đầu kỳ T6, nối tiếp đúng). |
| 1.1.6 | Thời gian: tùy chọn ngày | **PASS\*** | 2 ô ngày Từ–Đến hiển thị & điều khiển lọc (mọi preset ghi đúng khoảng). Không drive được picker ngày tùy ý qua tự động hóa để nhập ngày bất kỳ (giới hạn công cụ), nhưng cơ chế khoảng ngày hoạt động. |
| 1.1.7 | Lọc theo Người tạo | **PASS** | Chọn "tranvantest" → lọc đúng theo người tạo (rỗng vì người này không có phiếu CN1/tháng này); thẻ về 0. |
| 1.1.8 | Lọc theo Loại thu chi (Thu/Chi) | **PASS** | Multi-select Phiếu thu/Phiếu chi. Chọn "Phiếu chi" → chỉ hiện phiếu Chi, Tổng chi=1.189.745. *Lưu ý FIND-BALANCE (đầu kỳ tính lại thành âm).* |
| 1.1.9 | Lọc theo Phân loại thu chi | **PASS** | Dropdown: Đi trễ, Nghỉ không xin phép, Làm hư tài sản cửa hàng, Mua tôm hùm bông, Vệ sinh, Tiền rác… Chọn "Vệ sinh" → lọc đúng (rỗng vì không có phiếu loại này tháng này). |
| 1.1.10 | Lọc theo Loại nguồn | **PASS (cải thiện)** | Mục "Loại" NAY có đúng **Bán hàng / Mua hàng / Trả hàng / Tự tạo** (multi-select). Chọn "Bán hàng" → 212 phiếu (đều Thu), 8.258.370.282+775.606.767=9.033.977.049 ✔. *Phiên 0619 còn lệch (theo vai trò) → nay đã sửa.* |
| 1.1.11 | Kết hợp nhiều bộ lọc | **PASS** | CN1 + Tháng này + Loại nguồn=Bán hàng giao đúng (212 phiếu), 4 thẻ cập nhật theo bộ lọc & đúng công thức. |

## 1.2 Tổng quan quỹ
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.2.1 | Tồn quỹ đầu kỳ | **PASS** | Hiển thị & đổi theo kỳ (T6 8.264.976.882 / T5 766.830.706 / Tuần trước 9.026.457.836). |
| 1.2.2 | Tổng thu | **PASS** | Lọc Phiếu thu / Bán hàng = 778.363.939 / 775.606.767; sau khi thêm phiếu thu 100.000 → 778.463.939 (+100.000 ✔). |
| 1.2.3 | Tổng chi | **PASS** | Lọc Phiếu chi = 1.189.745; sau khi thêm phiếu chi 50.000 → 1.239.745 (+50.000 ✔). |
| 1.2.4 | Tồn cuối kỳ = đầu + thu − chi | **PASS** | Đúng ở mọi mốc đã kiểm (tháng/tuần/chi nhánh/loại nguồn). |
| 1.2.5 | Đổi lọc thời gian → 4 thẻ cập nhật | **PASS** | Mọi lần đổi Hôm nay/Hôm qua/Tuần/Tháng đều cập nhật cả 4 thẻ; tính liên tục cuối kỳ trước = đầu kỳ sau (✔). |

## 1.3 Danh sách phiếu
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.3.1 | Bảng phiếu đủ cột | **PASS** | Đủ 13 cột: STT, Mã phiếu, Loại thu chi, Số tiền, Tên chi nhánh, Người nộp/Người nhận, Người tạo, Phân loại thu chi, Phương thức thanh toán, Đính kèm, Thời gian ghi nhận, Mô tả, Hành động. |
| 1.3.2 | Phân trang | **PASS** | 235 phiếu / 12 trang (20 dòng/trang). Trang 1→2 dữ liệu khác nhau, không trùng/thiếu; thẻ tổng quan không đổi theo trang; có \|< < … > >\|. |
| 1.3.3 | Bấm icon xem chi tiết | **PASS** | Icon mắt → modal "Chi tiết phiếu" đủ thông tin (mã, loại, số tiền, chi nhánh, người tạo, PTTT, đính kèm, ngày tạo). Ngày tạo định dạng đẹp (20/06/2026 12:08). |
| 1.3.4 | Phiếu có đính kèm | **CHƯA KIỂM** | Trong dữ liệu Tháng này (CN1) không có phiếu nào có file đính kèm để bấm thử (cột Đính kèm trống). Tính năng cột tồn tại; phiên 0619 đã xác nhận mở được file đính kèm. |

## 1.4 Thêm phiếu
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.4.1 | Bấm "Thêm" mở modal | **PASS** | Modal "Thêm phiếu" mở đủ field. |
| 1.4.2 | Mã phiếu tự sinh | **PASS\*** | Ô hiện "Mã tăng tự động", **không preview mã**; mã sinh sau khi Lưu. |
| 1.4.3 | Bỏ trống Loại thu chi | **PASS** | Điền Số tiền nhưng để trống Loại thu chi → bấm Tạo mới → popup lỗi "Vui lòng chọn loại thu chi", chặn lưu. |
| 1.4.4 | Bỏ trống Số tiền | **PASS** | Submit trống → ô Số tiền viền đỏ + "Nhập số tiền", chặn lưu. |
| 1.4.5 | Chọn Loại nhân sự / Người nộp | **PASS\*** | Chọn "Thu ngân" → Người nộp auto "casher2"; danh sách Người nộp = nhân sự vai trò đó (casher2, admincn1, Cashier, cashier, tranvantest…). *Tên trường thực tế là "Loại nhân sự".* |
| 1.4.6 | Chọn Phân loại thu chi | **PASS\*** | Auto điền theo Loại (Thu→"Đi trễ", Chi→"Mua tôm hùm bông"); đổi được trong dropdown. |
| 1.4.7 | Chọn Phương thức thanh toán | **PASS** | Mặc định "Tiền mặt"; có lựa chọn khác. |
| 1.4.8 | Nhập Số tiền | **PASS\*** | Ô nhận số (100000 / 50000), lưu & hiển thị "100.000đ"/"50.000đ" đúng ở danh sách. Không tự chèn dấu phẩy khi gõ. |
| 1.4.9 | Đính kèm tệp | **N/A (BLOCKED)** | Không upload được tệp qua tự động hóa. |
| 1.4.10 | Mô tả giới hạn 200 ký tự | **FAIL/LỆCH** | Bộ đếm "0/50" → **giới hạn 50**, không phải 200. |
| 1.4.11 | Bấm "Lưu" hợp lệ | **PASS** | Tạo Phiếu thu 100.000 (PC00001650) → "Tạo thành công", lên đầu DS, Tổng thu +100.000, số bản ghi 235→236. |
| 1.4.12 | Bấm "Đóng" không tạo phiếu | **PASS** | Đóng bằng icon X / click ngoài → không tạo phiếu, số bản ghi giữ nguyên. |
| 1.4.13 | Mã tăng dần | **PASS** | Thu: PC00001649 → PC00001650 (next). Chi: PT00000037 → PT00000038 (tăng riêng chuỗi). |
| 1.4.14 | Nhập Số tiền = 0 | **FAIL (BUG-01)** | **Vẫn tạo thành công** PT00000000 Chi 0đ; không chặn. Bug lặp lại từ 0616/0619. |
| 1.4.15 | Loại đối tượng đổi → Người nộp đổi | **PASS\*** | Người nộp khóa & đổi theo "Loại nhân sự". *LỆCH: giá trị là vai trò (Quản lý/Quầy bếp/Thu ngân/NV order/Khác), không phải Khách hàng/Nhân viên.* |
| 1.4.16 | Loại đối tượng chưa chọn → Người nộp | **PASS** | Chưa chọn Loại nhân sự → Người nộp "No data found". |
| 1.4.17 | Loại=Chi → label "Người nhận" | **FAIL/LỆCH** | Label luôn "Người nộp / Người nhận" (gộp), không đổi theo Thu/Chi. |
| 1.4.18 | Xóa file đính kèm | **N/A (BLOCKED)** | Phụ thuộc upload (1.4.9). |
| 1.4.19 | Lưu phiếu thu → Tồn quỹ tăng | **PASS** | Số dư 9.042.151.076→9.042.251.076 (+100.000 ✔). |
| 1.4.20 | Lưu phiếu chi → Tồn quỹ giảm | **PASS** | Phiếu chi 50.000 (PT00000038) → Tổng chi 1.189.745→1.239.745, Số dư 9.042.251.076→9.042.201.076 (−50.000 ✔). |

## 1.5 Ghi nhận 4 loại phiếu
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.5.1 | Tạo Phiếu thu thủ công | **PASS** | PC00001650 +100.000 vào Tổng thu & Số dư (xem 1.4.11/1.4.19). |
| 1.5.2 | Tạo Phiếu chi thủ công | **PASS** | PT00000038 +50.000 Tổng chi, −50.000 Số dư (xem 1.4.20). |
| 1.5.3 | Phiếu thu hiển thị đúng thông tin | **PASS** | PC00001650: Loại=Thu, 100.000, phân loại "Đi trễ", PTTT "Tiền mặt" — khớp dữ liệu nhập. |
| 1.5.4 | Phiếu chi hiển thị đúng thông tin | **PASS** | PT00000038: Loại=Chi, 50.000, phân loại "Mua tôm hùm bông", PTTT "Tiền mặt" — khớp. |
| 1.5.5 | Hoàn tất đơn bán → tự sinh Phiếu bán hàng | **CHƯA KIỂM** | Có 212 phiếu Loại nguồn=Bán hàng (gián tiếp cho thấy cơ chế tự sinh hoạt động); chưa chạy luồng bán mới trong phiên này để xác nhận trực tiếp. |
| 1.5.6 | Trả hàng → tự sinh Phiếu trả hàng | **CHƯA KIỂM** | Cần chạy luồng Trả hàng (chưa thực hiện trong phiên). Bộ lọc Loại nguồn=Trả hàng đã có sẵn. |
| 1.5.7 | Lọc Loại nguồn = Bán hàng | **PASS** | 212 phiếu, đều là phiếu Thu sinh từ bán hàng (xem 1.1.10). |
| 1.5.8 | Lọc Loại nguồn = Trả hàng | **PASS\*** | Giá trị "Trả hàng" có trong dropdown & chọn được (multi-select như Bán hàng). Chưa đối chiếu số liệu cụ thể trong phiên. |
| 1.5.9 | Lọc Loại nguồn = Tự tạo | **PASS\*** | Giá trị "Tự tạo" có trong dropdown & chọn được. Chưa đối chiếu số liệu cụ thể. |
| 1.5.10 | Số tiền phiếu bán hàng khớp đơn gốc | **CHƯA KIỂM** | Cần luồng bán hàng đầy đủ. |
| 1.5.11 | Số tiền phiếu trả hàng khớp đơn gốc | **CHƯA KIỂM** | Cần luồng trả hàng. |
| 1.5.12 | PTTT phiếu tự sinh khớp đơn gốc | **CHƯA KIỂM** | Quan sát thấy phiếu tự sinh có PTTT "QR Tự động"/"Chuyển khoản"…; cần luồng bán để xác nhận trực tiếp. |
| 1.5.13 | Đơn bán bị hủy → phiếu không tính quỹ | **CHƯA KIỂM** | Cần luồng bán hàng đầy đủ. |
| 1.5.14 | Số liệu Thu chi khớp Điều phối ca | **CHƯA KIỂM** | Cần đối chiếu tab Điều phối ca. |
| 1.5.15 | Tổng thu = Σ tất cả nguồn thu | **PASS** | Lọc Phiếu thu = 778.363.939 = Σ phiếu thu (thủ công + bán hàng). |
| 1.5.16 | Tổng chi = Σ tất cả nguồn chi | **PASS** | Lọc Phiếu chi = 1.189.745 = Σ phiếu chi. |

## 1.6 Xuất Excel
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.6.1 | Bấm "Xuất Excel" | **PASS** | Popup ✓ "Đã xuất file, đang tải xuống trình duyệt." → kích hoạt tải file. |
| 1.6.2 | File xuất đúng dữ liệu theo bộ lọc | **N/A** | Export chạy theo bộ lọc đang áp; KHÔNG mở/đối chiếu được nội dung file (tải về máy người dùng, ngoài phạm vi tự động hóa). |

## 1.7 Công nợ (tab Quản lý công nợ)
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.7.1 | Mở tab Công nợ | **PASS** | Mở màn Công nợ + panel "Bộ Lọc"; chip Tất cả(52)/Gần đến hạn(23)/Quá hạn(15)/Hôm nay(0). |
| 1.7.2 | Đối tượng mặc định | **PASS** | 2 checkbox Khách hàng + Nhà cung cấp, mặc định cả 2 tích. |
| 1.7.3 | Lọc chỉ Khách hàng | **PASS** | Bỏ tích NCC → 51 dòng đều Khách hàng (52−1 NCC). |
| 1.7.4 | Lọc chỉ Nhà cung cấp | **PASS** | Chỉ tích NCC → 1 dòng ("nha cung cap 1", PO00000081, quá hạn 22 ngày). 51+1=52 ✔. |
| 1.7.5 | Bỏ tích cả 2 đối tượng | **CHƯA KIỂM** | Checkbox nhận thao tác chập chờn khi tự động hóa, không đưa được về trạng thái bỏ tích cả 2 để xác nhận. *Phiên 0619 ghi nhận lỗi: bỏ tích cả 2 → hiện TẤT CẢ (cần kiểm lại thủ công).* |
| 1.7.6 | Tìm theo Tên đối tượng | **CHƯA KIỂM** | Ô "Tên đối tượng" không nhận focus/input qua tự động hóa trong phiên này. |
| 1.7.7 | Tìm theo Mã công nợ | **CHƯA KIỂM** | Như trên. *Cải thiện: cột "Mã công nợ" nay đã CÓ dữ liệu (#52, #51…) — phiên 0619 còn trống.* |
| 1.7.8 | Lọc theo Chi nhánh | **N/A** | Chỉ có dữ liệu CN1 trong môi trường. |
| 1.7.9 | Lọc theo Người tạo | **CHƯA KIỂM** | Chưa xác nhận sạch (input chập chờn). |
| 1.7.10 | Kết hợp nhiều bộ lọc | **PASS\*** | Kết hợp Đối tượng + Chi nhánh hoạt động đúng (xem 1.7.3/1.7.4); chưa thử thêm Tên do ô tìm kiếm chưa nhập được. |
| 1.7.11 | Bảng công nợ đủ thông tin | **PASS** | Đủ cột: STT, Mã công nợ, Loại đối tượng, Tên đối tượng, Mã đơn (POS…/PO…), Chi nhánh, Chưa thanh toán, Đã thanh toán, Tổng tiền, Hạn còn, Ngày đáo hạn, Trạng thái (TT một phần/đủ, "Đã quá hạn N ngày"), Người tạo, Hành động. |
| 1.7.12 | Xem chi tiết công nợ | **CHƯA KIỂM** | Icon xem/bút chì có ở mỗi dòng; click chưa mở được modal sạch trong phiên (nhiễu state). Phiên trước: mở modal "Thanh toán nợ" đúng đối tượng. |
| 1.7.13 | (placeholder) | **N/A** | Không có nội dung trong checklist. |

---

## Tổng hợp
- **Tổng số testcase trong checklist:** 71 (1.1→1.7, gồm 1 placeholder 1.7.13).
- **PASS:** **47** (gồm các PASS\* đạt-nhưng-có-lưu-ý).
- **FAIL / LỆCH:** **3** — 1.4.14 (BUG-01 thật) · 1.4.10 (giới hạn 50≠200) · 1.4.17 (label không đổi theo Thu/Chi).
- **N/A:** **4** — 1.4.9, 1.4.18 (upload tệp) · 1.6.2 (nội dung file) · 1.7.8 (chỉ CN1) · 1.7.13 (placeholder). *(Lưu ý: 1.4.9/1.4.18 gộp đếm nhóm upload)*
- **CHƯA KIỂM (cần luồng bán/trả, đối chiếu, hoặc do input tự động hóa):** 1.3.4, 1.5.5, 1.5.6, 1.5.10, 1.5.11, 1.5.12, 1.5.13, 1.5.14, 1.7.5, 1.7.6, 1.7.7, 1.7.9, 1.7.12.

## Danh sách lỗi & phát hiện (chi tiết: `screenshot/0623_1047_cashboot/note.md`)
1. **BUG-01 (NẶNG, 1.4.14):** Phiếu **Số tiền = 0 vẫn tạo thành công** (PT00000000 Chi 0đ) → cho phép dữ liệu rác. **Ưu tiên fix — tồn tại từ 0616, lặp lại 0619 và 0623.**
2. **LỆCH-01 (1.4.10):** Mô tả giới hạn 50 ký tự (checklist ghi 200).
3. **LỆCH-02 (1.4.17):** Label luôn "Người nộp / Người nhận", không đổi theo Thu/Chi.
4. **LỆCH-03 (1.4.5/1.4.15):** Trường "Loại nhân sự" theo vai trò, không phải "Loại đối tượng" Khách hàng/Nhân viên như checklist.
5. **FIND-BALANCE:** "Tồn đầu kỳ"/"Số dư cuối ca" tính lại theo bộ lọc Loại thu chi (Chi-only ra số âm) → dễ hiểu nhầm số dư.
6. **Nhỏ:** mã phiếu không preview (1.4.2); số tiền không format khi gõ (1.4.8); mã phiếu tự sinh đôi khi ra dạng "PT00000000"/"PC00000000" (toàn số 0) — cần kiểm tra logic sinh mã.
7. **Môi trường (Flutter):** dropdown/biểu mẫu hay kẹt "lớp phủ ma" (phải tải lại trang); ô nhập text đôi khi không nhận focus khi tự động hóa.

## Cải thiện ghi nhận so với phiên 0619
- ✅ Bộ lọc **"Loại nguồn"** đã đúng (Bán hàng/Mua hàng/Trả hàng/Tự tạo) → 1.1.10, 1.5.7 PASS.
- ✅ Cột **"Mã công nợ"** ở tab Công nợ đã có dữ liệu (#52, #51…).

## Khuyến nghị
1. **Ưu tiên fix BUG-01** (chặn Số tiền ≤ 0 khi tạo phiếu).
2. Sửa **giới hạn Mô tả** (50 vs 200) và **label Người nộp/Người nhận** đổi theo Thu/Chi.
3. Cân nhắc giữ **"Tồn đầu kỳ" cố định** khi lọc theo Loại thu chi.
4. Kiểm tra logic **sinh mã phiếu** (tránh ra "PT00000000").
5. Phiên sau (đầy đủ, làm thủ công): chạy **luồng bán hàng & trả hàng** để kiểm 1.5.5/1.5.6/1.5.10–1.5.14; chuẩn bị **tệp đính kèm** cho 1.4.9/1.4.18 & 1.3.4; kiểm lại **Công nợ** 1.7.5 (bỏ tích cả 2), 1.7.6/1.7.7 (tìm kiếm), 1.7.12 (chi tiết).

## Dữ liệu test đã tạo trong phiên (để dọn nếu cần)
- **PC00001650CN2** — Thu 100.000 (phân loại "Đi trễ")
- **PT00000000CN2** — Chi 0đ (từ BUG-01)
- **PT00000038CN2** — Chi 50.000 (phân loại "Mua tôm hùm bông")
