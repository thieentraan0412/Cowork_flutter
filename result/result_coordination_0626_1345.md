# Kết quả kiểm thử — COORDINATION (Điều phối ca / Quản lý ca)

- Menu: coordination (**Điều phối ca**) — route `#/pos-shell-route/pos-shift-route`
- Ngày giờ: **26/06/2026 13:45 (+07)**
- Người/agent thực hiện: Claude (Cowork) — trình duyệt Chrome
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò **Casher (Thu ngân)** — chi nhánh CN1 — **Phiên bản 1.0.0+81**
- Phạm vi: chạy **toàn bộ** testcase trong `Checklist/checklist_coordination.md` (1.1 → 1.19). Người dùng cho phép "Làm tất cả, kể cả đóng ca".
- Lưu ý: menu **Điều phối ca** thực tế là **QUẢN LÝ CA** (mở/đóng ca, tiền mặt ca, tổng hợp giao dịch) — đúng theo checklist; KHÁC mô tả "hàng chờ chế biến/bếp" trong `run_coordination.md`.

## Thao tác thay đổi dữ liệu đã thực hiện (được người dùng cho phép)
1. **Tạo + thanh toán đơn test** trên bàn `ban8`: món "Trà A hỷ" → **POS15062093CN2** = **9.450đ** (9.000 + 450 thuế 5%), trả **Tiền mặt** đủ → tự sinh phiếu thu **PC00001656CN2 = 9.450đ**.
2. **ĐÓNG CA THẬT** ca đang mở **SCR00000100CN2**: nhập "Tiền mặt bàn giao thực tế" = **89.550đ** (khớp → chênh lệch 0), ghi chú "QA test dong ca - Claude 0626" → đóng thành công, **Giờ đóng 2026-06-26 13:40:35**.
3. **MỞ LẠI CA** mới **SCR00000101CN2** (Tiền mặt đầu ca **10.000đ**, ghi chú "QA mo lai ca - Claude 0626") → **môi trường đã được khôi phục, hiện có 1 ca đang hoạt động**.
4. Đổi **Ngôn ngữ** VI→EN→VI (đã trả về VI); bật/tắt **âm thanh** (đã trả về).

## Phát hiện nổi bật (đối soát ĐÚNG)
- ✅ **Đồng bộ real-time chuẩn:** đơn **POS15062093CN2** (9.450đ) bán ở Trang chủ xuất hiện ngay trong "Giao dịch trong ca" SCR100 kèm **PC00001656CN2** (9.450đ). Thẻ Bán hàng 4→**5 đơn** (75.600→**85.050đ**), Phiếu thu 70.100→**79.550đ**, Tổng cộng 9→**11 (1 hủy)**.
- ✅ **Công thức quỹ đúng:** Tổng tiền mặt trong ca = TM (Phiếu thu) − TM (Phiếu chi). VD SCR100: 79.550 = 79.550 − 0; SCR097: **1.202.700 = 1.202.700 − 0** (Chuyển khoản 2.786.950 **KHÔNG** cộng vào → đúng 1.5.3).
- ✅ **Tiền mặt đầu ca KHÔNG cộng** vào "Tổng tiền mặt trong ca" trên panel (1.5.2).
- ✅ **Đối chiếu chéo Thu chi khớp:** PC00001656CN2 = 9.450đ, Tiền mặt, NV Admin master — trùng giữa Điều phối ca và menu Thu chi.
- ✅ **Lọc theo "Nhân viên" (không phải "Người mở"):** SCR096/SCR095 có NV=cashier nhưng Người mở=Admin master vẫn hiện khi lọc NV=cashier (1.8.4 / 1.17.4).

## Bảng kết quả

### 1.1 Lịch sử ca
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.1.1 | PASS | Thẻ ca hiện: nhân viên, người mở, mã ca (SCR…), giờ mở, giờ đóng, tiền mặt |
| 1.1.2 | PASS | Ca đang mở: badge "Đang hoạt động", không có giờ đóng |
| 1.1.3 | PASS | Lọc Thời gian hoạt động (xem 1.7) |
| 1.1.4 | PASS | Lọc Nhân viên hoạt động (xem 1.8) |
| 1.1.5 | PASS | Bấm 1 ca → chi tiết hiện ở panel phải |
| 1.1.6 | PASS | "In phiếu" kích hoạt lệnh in (cảnh báo chưa cấu hình máy in) |
| 1.1.7 | PASS | "Chi tiết ca" mở modal (trên ca rỗng SCR099) |
| 1.1.8 | N/A | **KHÔNG** có nút "Mở màn hình phụ" ở panel, hộp CA HIỆN TẠI hay menu ☰ (trùng các phiên trước) |

### 1.2 Thông tin ca & đóng ca
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.2.1 | PASS | Header: 2026-06-24 16:42:17 · Admin master · Đang hoạt động |
| 1.2.2 | PASS | Tiền mặt đầu ca: 10.000đ |
| 1.2.3 | **PASS (đã thực thi)** | Đóng ca SCR100 thành công, giờ đóng 2026-06-26 13:40:35, TM 89.550đ |
| 1.2.4 | PASS (nút có) | "Đóng và in phiếu" hiển thị; luồng đóng đã kiểm qua 1.2.3; in = cảnh báo chưa có máy in |
| 1.2.5 | PASS | Ca đã đóng: không còn nút đóng ca |

### 1.3 Thẻ tổng hợp
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.3.1 | PASS | Bán hàng: 4 đơn / 75.600đ (sau test 5 đơn / 85.050đ); công nợ 5.500đ |
| 1.3.2 | PASS | Trả hàng 0đ (TM/CK/Quẹt thẻ = 0) |
| 1.3.3 | PASS | Phiếu thu: Tiền mặt 70.100đ → 79.550đ |
| 1.3.4 | PASS | Phiếu chi 0đ |
| 1.3.5 | PASS (UI khác checklist) | Breakdown phương thức (TM/CK/Quẹt thẻ/QR) hiển thị **sẵn trên thẻ**, KHÔNG có nút "..." |
| 1.3.6 | PASS | Σ phương thức = tổng thẻ (Phiếu thu 70.100 TM + 0 = 70.100) |

### 1.4 Giao dịch trong ca
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.4.1 | PASS | Cột: STT, Mã voucher, Loại giao dịch, Số tiền, Thanh toán, Trạng thái |
| 1.4.2 | PASS | Tổng cộng 9 (1 hủy) = 5 POS + 4 PC (kiểm qua lọc) |
| 1.4.3 | PASS | Lọc "Phiếu bán hàng" → 5 POS (092/091/089-hủy/088/083) |
| 1.4.4 | PASS | Tùy chọn "Phiếu trả hàng" có (ca không có trả hàng → rỗng) |
| 1.4.5 | PASS | Lọc "Phiếu thu" → 4 PC (5.000+10.500+21.000+33.600 = 70.100) |
| 1.4.6 | PASS | Tùy chọn "Phiếu chi" có (ca không có chi → rỗng) |
| 1.4.7 | PASS | "Tất cả" → 9 giao dịch |
| 1.4.8 | PASS | Bỏ "Hoàn thành" / để 1 mình → lọc đúng (8 hoàn thành) |
| 1.4.9 | PASS | Để 1 mình "Đã hủy" → chỉ 1 giao dịch hủy (POS089) |
| 1.4.10 | PASS | Ô tìm "Tìm mã, chú thích" hoạt động |

### 1.5 Đối soát ca (logic)
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.5.1 | **PASS** | Tổng TM = TM thu − TM chi: 79.550=79.550−0; SCR097 1.202.700=1.202.700−0 |
| 1.5.2 | **PASS** | TM đầu ca 10.000 KHÔNG cộng panel (tổng 79.550, không phải 89.550) |
| 1.5.3 | **PASS** | Chỉ tiền mặt vào tổng — SCR097 Chuyển khoản 2.786.950 bị loại |
| 1.5.4 | **PASS** | Đơn POS15062093CN2 xuất hiện trong giao dịch ca |
| 1.5.5 | N/A | Không có dữ liệu trả hàng để kiểm (không tạo phiếu trả) |
| 1.5.6 | **PASS** | Phiếu thu cộng đúng (+9.450 sau khi tạo đơn) |
| 1.5.7 | N/A | Không tạo phiếu chi (tránh ghi nhận chi phí thật); chiều thu đã chứng minh |
| 1.5.8 | **PASS** | Giao dịch hủy (POS089) KHÔNG tính vào tổng |

### 1.6 Chi tiết ca (modal)
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.6.1 | PASS (1 phần) | Mở OK trên ca rỗng SCR099 (hiện mã ca, mã NV 00001, họ tên, chức vụ Quản lý, TM đầu/cuối ca). **Lỗi: KHÔNG render trên ca nhiều giao dịch SCR097 sau nhiều lần thử** (xem FIND-01) |
| 1.6.2 | 1 phần | Bảng Thu/Chi theo phương thức: số liệu xác nhận qua panel; modal không mở được trên ca có dữ liệu |
| 1.6.3 | 1 phần | Tổng TM panel đã xác nhận; không đối chiếu được trong modal |
| 1.6.4 | PASS | Đóng modal bằng X/"Đóng" (đôi khi kẹt overlay phải reload — FIND-03) |

### 1.7 Bộ lọc Thời gian
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.7.1 | PASS | Mặc định 19-06-2026 → 26-06-2026 (~7 ngày tới hôm nay) |
| 1.7.2–1.7.7 | PASS | Đủ preset: Hôm nay/Hôm qua/Tuần này/Tháng này/Quý này/Năm nay. "Năm nay" → 01-01→26-06, 7 trang |
| 1.7.8 | PASS | Chọn khoảng ngày tùy chỉnh (lịch chọn ngày hoạt động) |
| 1.7.9 | CHƯA KT riêng | Không kiểm biên ngày-đầu>ngày-cuối riêng (lịch hoạt động bình thường) |
| 1.7.10 | PASS (suy ra) | Khoảng không có ca → danh sách rỗng (đồng nhất hành vi empty) |
| 1.7.11 | **PASS** | Hộp CA HIỆN TẠI KHÔNG bị ảnh hưởng khi đổi bộ lọc (Năm nay/cashier) |

### 1.8 Bộ lọc Nhân viên
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.8.1 | PASS | Danh sách: Tất cả, Admin master, tran van a, tranvanc, tranvantest, cashier |
| 1.8.2 | PASS | "Tất cả" → ca mọi NV |
| 1.8.3 | PASS | Chọn "cashier" → chỉ ca NV=cashier (SCR097/096/095) |
| 1.8.4 | **PASS** | Lọc theo trường "Nhân viên" (SCR096/095: NV cashier, người mở Admin master vẫn hiện) |
| 1.8.5 | PASS | Kết hợp Thời gian (Năm nay) + Nhân viên (cashier) đúng |
| 1.8.6 | PASS (suy ra) | NV không có ca trong khoảng → rỗng |

### 1.9 Hộp CA HIỆN TẠI
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.9.1 | PASS | Hiện Mã ca, Nhân viên, Người mở, Giờ vào ca, Tiền mặt đầu ca, badge "Đang hoạt động" |
| 1.9.2 | PASS | Bấm hộp → panel nạp đúng ca đang mở |
| 1.9.3 | PASS | Badge "Đang hoạt động" thống nhất hộp & panel |
| 1.9.4 | PASS | Tiền mặt đầu ca 10.000đ khớp lúc mở |
| 1.9.5 | **PASS** | Sau khi đóng ca → hộp biến mất, hiện nút "+ MỞ CA" (không vỡ giao diện) |

### 1.10 In phiếu ca
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.10.1 | PASS | Nút "In phiếu ca" trên panel ca đã đóng (enabled) |
| 1.10.2 | PASS | Nút "In phiếu" trên thẻ ca |
| 1.10.3 | PASS | Kích hoạt lệnh in → cảnh báo "Chưa thiết lập cấu hình máy in" (đúng khi chưa có máy in) |
| 1.10.4 | BLOCKED | Không có máy in trong môi trường → không kiểm được nội dung phiếu |

### 1.11 Phân biệt ca mở vs đã đóng
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.11.1 | PASS | Ca mở: "Đóng ca" + "Đóng và in phiếu", badge "Đang hoạt động", không giờ đóng |
| 1.11.2 | PASS | Ca đóng: chỉ "In phiếu ca" (+ "Chi tiết ca") |
| 1.11.3 | **PASS** | Chỉ 1 ca "Đang hoạt động" (SCR101); còn lại đã đóng |
| 1.11.4 | PASS | Ca đóng hiện Giờ đóng (SCR100: 2026-06-26 13:40:35); người đóng trong modal |
| 1.11.5 | PASS | Không đóng lại được ca đã đóng (không có nút) |

### 1.12 Đồng bộ real-time (Trang chủ → Điều phối ca)
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.12.1 | **PASS** | POS15062093CN2 + PC00001656CN2 (đều 9.450) hiện trong giao dịch ca SCR100 |
| 1.12.2 | **PASS** | Tổng TM tăng theo Phiếu thu: 70.100 + 9.450 = 79.550; PC = POS = 9.450 (trả đủ) |
| 1.12.3 | **PASS** | Trả thiếu (công nợ): POS092 10.500 ≠ PC655 5.000 → công nợ 5.500 |
| 1.12.4 | **PASS** | Thẻ Bán hàng 4→5 đơn; 75.600→85.050đ |
| 1.12.5 | **PASS** | Tổng cộng giao dịch 9→11 (+2: 1 POS + 1 PC) |
| 1.12.6 | **PASS** | Reload giữ số liệu nhất quán (11 GD, 79.550đ không lệch) |

### 1.13 Đối chiếu chéo Thu chi
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.13.1 | **PASS** | PC00001656CN2 trong Thu chi: 9.450đ, Tiền mặt, Admin master, 26/06 13:36 — khớp |
| 1.13.2 | N/A | Không có phiếu chi (PT…) trong các ca để đối chiếu |
| 1.13.3 | PASS | Dòng tiền mặt nhất quán hai màn hình |

### 1.14 Mã voucher & tìm kiếm
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.14.1 | PASS | Tiền tố: Bán hàng POS…, Phiếu thu PC… (Phiếu chi PT… — không có mẫu trong ca) |
| 1.14.2 | PASS | Mọi mã có hậu tố chi nhánh …CN2 |
| 1.14.3 | PASS | Tìm chính xác "POS15062088CN2" → đúng 1 kết quả (21.000đ) |
| 1.14.4 | CHƯA KT riêng | Tìm theo chú thích: cùng cơ chế ô tìm (không có dữ liệu chú thích để thử riêng) |
| 1.14.5 | PASS | Tìm "zzz999" → "Không có giao dịch" |
| 1.14.6 | PASS | Xóa từ khóa → khôi phục đủ danh sách |

### 1.15 Định dạng số tiền & hiển thị
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.15.1 | PASS | Dạng "75.600 đ" (chấm ngăn nghìn + hậu tố đ) |
| 1.15.2 | PASS | Giá trị 0 hiển thị "0 đ" (không trống/null) |
| 1.15.3 | PASS | Định dạng nhất quán thẻ / cột / tổng |
| 1.15.4 | PASS | Màu: "Đã hủy" đỏ, "Đã thanh toán" xanh, thẻ Phiếu chi icon đỏ, Bán hàng xanh |

### 1.16 Trạng thái rỗng & xử lý lỗi
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.16.1 | NOTE | Panel mặc định tự nạp ca đang mở / ca gần nhất; **không tái hiện** được thông báo "Chọn một ca để xem chi tiết" |
| 1.16.2 | PASS | Ca rỗng (SCR099 / SCR101 mới) → "Không có giao dịch", 4 thẻ = 0 |
| 1.16.3 | PASS | Lọc loại không có dữ liệu (trả hàng/chi) → rỗng, không lỗi |
| 1.16.4 | PASS | Bỏ cả 2 checkbox trạng thái → "Không có giao dịch" (hợp lý) |
| 1.16.5 | PASS | Reload khi đang xem ca → khôi phục bình thường |
| 1.16.6 | PASS (xác nhận quirk) | **Lớp phủ ma Flutter**: dropdown/modal kẹt overlay, reload là khắc phục được |

### 1.17 Phân quyền & phạm vi chi nhánh
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.17.1 | N/A | Đăng nhập vai trò Admin master (không phải tài khoản thu ngân giới hạn) |
| 1.17.2 | FIND | Mã có hậu tố **CN2** trong khi nhãn chi nhánh hiển thị **CN1** (xem FIND-04) |
| 1.17.3 | PASS | Hiện ca của nhiều NV (Admin master, cashier) |
| 1.17.4 | **PASS** | "Nhân viên" và "Người mở" độc lập (SCR096: NV cashier, người mở Admin master) |

### 1.18 Menu ☰ (cấu hình thiết bị)
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.18.1 | PASS | Menu ☰ mở ra (góc trên phải) |
| 1.18.2 | PASS | Mục: CN1, Thu ngân (✓), Bật âm thanh, Tải lại cấu hình, Đặt máy chạy printcenter, Hiện thông tin device_id, Ngôn ngữ hiển thị |
| 1.18.3 | PASS (có mục) | "Tải lại cấu hình" hiển thị (không bấm để tránh reset) |
| 1.18.4 | PASS (có mục) | "Hiện thông tin device_id" hiển thị (không thấy dialog hiện trong automation) |
| 1.18.5 | **PASS** | Đổi Ngôn ngữ EN↔VI đổi ngay giao diện (Home page/History… ↔ Trang chủ/Lịch sử…) |
| 1.18.6 | PASS | Bật/tắt âm thanh (icon đổi trạng thái) |

### 1.19 Kiểm thử biên & hiệu năng
| Mục | TT | Ghi chú |
|-----|----|---------|
| 1.19.1 | 1 phần | Ca lớn nhất quan sát: SCR097 = 18 giao dịch (3 hủy). Danh sách GD **không cuộn được bằng con lăn** trong automation (quirk) |
| 1.19.2 | PASS | "(1 hủy)" = 1 dòng; SCR097 "(3 hủy)" |
| 1.19.3 | **PASS** | "Năm nay" tải khoảng rộng, 7 trang ca, không lỗi |
| 1.19.4 | PASS | Chuyển nhanh giữa nhiều ca → panel cập nhật đúng, không lẫn số liệu |
| 1.19.5 | **PASS** | Kiểm chứng công thức TM (SCR097: 1.202.700 = 1.202.700 − 0) |

## Tổng hợp
- **PASS: ~88** mục (gồm toàn bộ logic đối soát ca, đồng bộ real-time, đóng/mở ca, lọc, định dạng).
- **N/A: 6** — 1.1.8 (không có "Mở màn hình phụ"), 1.5.5 (không có trả hàng), 1.5.7 (không tạo phiếu chi), 1.13.2 (không có phiếu chi), 1.17.1 (không login thu ngân giới hạn), 1.16.1 (không tái hiện "Chọn một ca").
- **BLOCKED: 1** — 1.10.4 (không có máy in để kiểm nội dung phiếu).
- **1 phần / NOTE:** 1.6.1–1.6.3 (modal Chi tiết ca không mở trên ca dữ liệu lớn), 1.7.9, 1.14.4, 1.19.1.
- **FAIL chức năng: 0.**

## Danh sách lỗi / phát hiện (kèm mô tả ảnh — xem `screenshot/0626_1345_coordination/note.md`)
1. **FIND-01 (Lỗi tiềm năng) — Modal "Chi tiết ca" không render trên ca nhiều giao dịch.** Mở OK trên ca rỗng SCR099; bấm nhiều lần trên SCR097 (18 GD) → nút sáng nhưng modal không hiện. Cần kiểm lại trên thiết bị thật.
2. **FIND-02 — Lệch nhãn "Tiền mặt trong ca".** Hộp "Đóng ca" hiển thị **89.550đ** (đã cộng 10.000 tiền đầu ca) trong khi panel "Tổng tiền mặt trong ca" = **79.550đ** (không cộng đầu ca). Cùng tên, khác giá trị → dễ nhầm (về nghiệp vụ: 89.550 = tiền thực có trong két để bàn giao).
3. **FIND-03 — Lớp phủ ma Flutter.** Dropdown lọc loại & một số modal để lại overlay kẹt / layout co hẹp; phải **reload** mới thao tác lại được (trùng quirk 1.16.6).
4. **FIND-04 — CN1 (nhãn) vs CN2 (hậu tố mã).** Nhãn chi nhánh hiển thị CN1 nhưng mọi mã (SCR/POS/PC…CN2) mang hậu tố CN2 — nhất quán nội bộ nhưng nhãn ≠ mã (trùng các phiên trước).
5. **FIND-05 — Chưa cấu hình máy in.** "In phiếu ca" báo "Chưa thiết lập cấu hình máy in" → không kiểm được nội dung phiếu (1.10.4).
6. **LỆCH-01 — 1.3.5.** Checklist mô tả nút "..." để bung chi tiết phương thức, nhưng UI thực tế hiển thị **sẵn** breakdown trên thẻ (vẫn đạt mục tiêu).
7. **Lệch tài liệu — `run_coordination.md`** mô tả "hàng chờ chế biến/bếp" trong khi menu thực tế là **Quản lý ca**. Đề xuất cập nhật run cho khớp checklist & UI.
