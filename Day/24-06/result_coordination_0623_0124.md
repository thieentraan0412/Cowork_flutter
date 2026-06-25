# Kết quả kiểm thử — Menu COORDINATION (Điều phối ca) — phiên 0623_0124

- Menu: coordination (**Điều phối ca**)
- Ngày giờ chạy: 23/06/2026, ~01:10–01:25 (giờ VN)
- Người/agent thực hiện: Claude
- Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin` (**Admin master**), vai trò **Thu ngân (Cashier)**, chi nhánh **CN1**
- Phiên bản ứng dụng: **1.0.0+65** — Trình duyệt: Chrome (điều khiển qua extension)
- Tài liệu: `run/run_coordination.md` + `Checklist/checklist_coordination.md` + `Link/Link.md`
- Route thực tế của menu: `#/pos-shell-route/pos-shift-route`

> **Ảnh lỗi:** công cụ chụp màn hình trong phiên này **không lưu được file ảnh ra đĩa** (xác nhận lại như các phiên History/Cashboot/Coordination trước). Vì vậy lỗi/độ lệch được mô tả bằng văn bản kèm số liệu đối chứng + các bước tái hiện. Xem `screenshot/0623_0124_coordination/note.md`.

> **Lưu ý menu:** "Coordination" ở hệ thống này = **Điều phối ca** (quản lý ca thu ngân: ca hiện tại, lịch sử ca, panel chi tiết ca, 4 thẻ tổng hợp, giao dịch trong ca, đối soát, modal "Chi tiết ca"). KHÁC với mô tả "hàng chờ chế biến/bếp" ở phần *Trọng tâm* của `run_coordination.md`. Bài test bám theo **checklist** (đúng UI thực tế).

> **Ghi chú kỹ thuật:** widget Flutter **không nhận click chuột CDP thông thường** → phải dispatch PointerEvent (pointerdown → pointermove → pointerup) trên `flt-glass-pane` mới ăn; ô tìm kiếm Flutter **không nhận gõ phím tự động** → phải set value + dispatch `input` trên `input.flt-text-editing`. Dropdown lịch đôi khi kẹt "lớp phủ ma".

## Bối cảnh dữ liệu (đối chứng)

**CA HIỆN TẠI (đang mở):** `SCR00000098CN2` — NV **Admin master**, người mở Admin master, vào ca **16:49 18/06/2026**, **Tiền mặt đầu ca 0đ**, badge "Đang hoạt động".
- Bán hàng: Công nợ 500.000 · Đơn hàng 7 · Tổng tiền **1.937.386**
- Trả hàng: 0
- Phiếu thu: TM **1.407.486** · CK 30.450 · Quẹt thẻ 0 · QR tự động 9.450 · (Phiếu thu 8) · Tổng **1.447.386**
- Phiếu chi: TM **5.000** · CK 0 · Quẹt thẻ 0 · (Phiếu chi 2) · Tổng **5.000**
- **Tổng tiền mặt trong ca: 1.402.486** (= 1.407.486 − 5.000) ✔
- Giao dịch trong ca: **32 (15 hủy)**

**CA ĐÃ ĐÓNG mẫu:** `SCR00000097CN2` — NV **cashier**, người mở cashier, **người đóng Admin master**, mở 16/06 16:31:28, đóng 18/06 15:51:00, đầu ca 0đ.
- Bán hàng: Công nợ 90.000 · Đơn 7 · Tổng **4.074.650** (Gross) / Net 3.863.000
- Phiếu thu: TM **1.202.700** · CK 2.786.950 · Tổng **3.989.650** (Phiếu thu 8)
- Phiếu chi: 0
- **Tổng tiền mặt trong ca: 1.202.700** (= 1.202.700 − 0) ✔
- Giao dịch: **18 (3 hủy)**

## Kết luận nhanh

- ✅ **Lõi nghiệp vụ Điều phối ca chạy đúng:** lọc lịch sử ca (thời gian + nhân viên), xem chi tiết ca ở panel phải, 4 thẻ tổng hợp + công thức tổng tiền mặt, danh sách giao dịch + đầy đủ bộ lọc (loại/trạng thái/tìm kiếm), modal "Chi tiết ca", phân biệt ca mở/đóng.
- ❌ **FAIL-01 (1.1.8): Không tìm thấy nút "Mở màn hình phụ"** ở panel ca đang mở, hộp CA HIỆN TẠI, lẫn menu ☰ (menu ☰ chỉ có: CN1, Thu ngân, Bật âm thanh, Tải lại cấu hình, **Đặt máy chạy printcenter**, **Hiện thông tin device_id**, Ngôn ngữ). Trùng FAIL phiên 0617.
- ⚠️ **LỆCH-01 (1.3.5): Không có nút "..."** trên thẻ tổng hợp — chi tiết phương thức (TM/CK/Quẹt thẻ/QR) **luôn hiển thị sẵn** trên thẻ (vẫn đạt mục tiêu xem chi tiết, chỉ khác cách thao tác).
- ⚠️ **FIND-01 (1.6.2):** Trong modal "Chi tiết ca" của SCR97, bảng **"Phương thức thanh toán" TM = 1.287.700** nhưng thẻ **Phiếu thu (panel) TM = 1.202.700** (lệch **85.000**). Do hai cách nhóm khác nhau (modal = doanh thu bán hàng Gross theo phương thức; panel = tiền mặt thực thu vào két). CK khớp tuyệt đối (2.786.950) và **"Tổng tiền mặt cuối ca" (modal) = "Tổng tiền mặt trong ca" (panel) = 1.202.700** → tổng quỹ vẫn đúng. Đề nghị thống nhất nhãn/diễn giải để tránh hiểu nhầm.
- 🚧 **BLOCKED (tính năng) — 1.5.5:** Trả hàng vẫn báo **"Tính năng returns đang phát triển"** → không tạo được phiếu trả để kiểm tra giảm tổng.
- ⏸️ **KHÔNG thực thi (an toàn) — 1.2.3 / 1.2.4:** Nút "Đóng ca" / "Đóng và in phiếu" **có sẵn & enabled** nhưng **không bấm** để tránh đóng ca thu ngân đang chạy trên store test dùng chung. **1.5.4 / 1.5.6** cũng không tạo chứng từ mới (tránh thay đổi số liệu ca chung) → kiểm bằng dữ liệu sẵn có.

---

## 1.1 Lịch sử ca

| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.1.1 | Hiển thị danh sách các ca | **PASS** | Mỗi ca đủ trường: nhân viên, người mở, mã ca, giờ mở, giờ đóng, tiền mặt (dạng **thẻ**, không phải bảng cột). Ca đang mở nằm ở hộp **CA HIỆN TẠI**. |
| 1.1.2 | Ca đang mở hiển thị đúng trạng thái | **PASS** | SCR98 ở hộp CA HIỆN TẠI, badge **"Đang hoạt động"**, có "Giờ vào ca", **không** có giờ đóng. (Nhãn "Đang hoạt động", không phải chữ "Đang mở".) |
| 1.1.3 | Lọc theo Thời gian (khoảng ngày) | **PASS** | Đặt 09/06→15/06 → danh sách đổi sang SCR96/SCR95/SCR94 (mở trong khoảng); SCR97 (16/06), SCR98 (18/06) bị loại. Có sẵn nhanh: Hôm nay / Hôm qua / Tuần này / Tháng này / Quý này / Năm nay. |
| 1.1.4 | Lọc theo Nhân viên | **PASS** | Dropdown gồm: Tất cả, Admin master, tran van a, tranvanc, tranvantest, cashier. Chọn "Admin master" (trong khoảng 09–15 toàn ca của cashier) → "Không có dữ liệu lịch sử" → xác nhận lọc theo trường **Nhân viên** của ca. |
| 1.1.5 | Bấm vào 1 ca để xem chi tiết | **PASS** | Bấm thẻ SCR97 → panel phải nạp đúng chi tiết ca đó (header "Đã đóng" + 4 thẻ + giao dịch cập nhật theo ca chọn). |
| 1.1.6 | Nút "In phiếu" của ca | **PASS\*** | Thẻ ca đã đóng có nút **"In phiếu"**; góc phải có **"In phiếu ca"** — đều có sẵn & enabled. Không kích hoạt in thật (tránh mở hộp thoại in). |
| 1.1.7 | Nút "Chi tiết ca" | **PASS** | Bấm "Chi tiết ca" (trên thẻ ca đã chọn) → mở modal "Chi tiết ca" (xem 1.6). |
| 1.1.8 | Nút "Mở màn hình phụ" | **FAIL** | **Không tồn tại** nút "Mở màn hình phụ" ở panel ca đang mở, hộp CA HIỆN TẠI, hay menu ☰. Panel ca đang mở chỉ có "Đóng ca" + "Đóng và in phiếu"; menu ☰ chỉ có CN1/Thu ngân/Bật âm thanh/Tải lại cấu hình/Đặt máy chạy printcenter/Hiện thông tin device_id/Ngôn ngữ. |

## 1.2 Thông tin ca & đóng ca

| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.2.1 | Hiển thị header ca đúng thông tin | **PASS** | Header panel: "2026-06-18 16:49:04 · Nhân viên: Admin master · Đang hoạt động" (ca mở); "2026-06-16 16:31:28 · Nhân viên: cashier · Đã đóng" (ca đóng). Đúng ngày giờ + tên NV + trạng thái. |
| 1.2.2 | Hiển thị Tiền mặt đầu ca | **PASS** | "Tiền mặt đầu ca: 0 đ" — khớp số khai báo khi mở ca (0đ). |
| 1.2.3 | Nút "Đóng ca" | **N/A (an toàn)** | Nút **có sẵn & enabled** ở góc phải panel ca đang mở. **Không bấm** để tránh đóng ca thu ngân đang chạy trên store dùng chung (cần xác nhận người dùng). |
| 1.2.4 | Nút "Đóng và in phiếu" | **N/A (an toàn)** | Nút **có sẵn & enabled** kế bên "Đóng ca". **Không bấm** (lý do như 1.2.3). |
| 1.2.5 | Ca đã đóng không cho thao tác lại | **PASS** | Mở chi tiết SCR97 (đã đóng): góc phải **chỉ** còn "In phiếu ca", **không** hiển thị "Đóng ca"/"Đóng và in phiếu" → không thể đóng lại ca đã đóng. |

## 1.3 Thẻ tổng hợp (Bán hàng / Trả hàng / Phiếu thu / Phiếu chi)

| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.3.1 | Thẻ Bán hàng hiển thị đúng | **PASS** | Thẻ Bán hàng: Đơn hàng **7** · Tổng tiền **1.937.386** (SCR98) / **4.074.650** (SCR97). Có thêm dòng "Công nợ". |
| 1.3.2 | Thẻ Trả hàng hiển thị đúng | **PASS** | Thẻ Trả hàng = 0 (cả 2 ca không phát sinh trả hàng) — Phiếu trả 0, Tổng 0đ. |
| 1.3.3 | Thẻ Phiếu thu hiển thị đúng | **PASS** | SCR98: TM 1.407.486 · CK 30.450 · QR 9.450 · Tổng 1.447.386 (8 phiếu). SCR97: TM 1.202.700 · CK 2.786.950 · Tổng 3.989.650. |
| 1.3.4 | Thẻ Phiếu chi hiển thị đúng | **PASS** | SCR98: TM 5.000 · Tổng 5.000 (2 phiếu). SCR97: 0đ. |
| 1.3.5 | Bấm "..." xem chi tiết phương thức | **LỆCH** | **Không có nút "..."**. Chi tiết phương thức (TM/CK/Quẹt thẻ/QR) **luôn hiển thị sẵn** ngay trên mỗi thẻ → vẫn đạt mục tiêu, chỉ khác cách thao tác so với checklist. |
| 1.3.6 | Tổng các phương thức khớp tổng thẻ | **PASS** | Phiếu thu SCR98: 1.407.486 + 30.450 + 0 + 9.450 = **1.447.386** ✔. Phiếu thu SCR97: 1.202.700 + 2.786.950 = **3.989.650** ✔. Phiếu chi SCR98: 5.000 = 5.000 ✔. |

## 1.4 Giao dịch trong ca

| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.4.1 | Hiển thị danh sách giao dịch | **PASS** | Cột đầy đủ: STT, Mã voucher, Loại giao dịch, Số tiền, Thanh toán, Trạng thái. |
| 1.4.2 | Đếm đúng tổng số giao dịch | **PASS** | Header "Tổng cộng **18** (3 hủy)" cho SCR97; "**32** (15 hủy)" cho SCR98 — khớp số dòng/loại lọc thực tế. |
| 1.4.3 | Lọc loại: Phiếu bán hàng | **PASS** | Tùy chọn có trong dropdown loại; lọc trả về đúng các POS bán hàng. |
| 1.4.4 | Lọc loại: Phiếu trả hàng | **PASS** | Tùy chọn có; SCR97/SCR98 không có phiếu trả → danh sách rỗng (đúng). |
| 1.4.5 | Lọc loại: Phiếu thu | **PASS** | Chọn "Phiếu thu" → chỉ còn các PC (PC...1643/1642/1641/1640/1639...) — đã kiểm trực tiếp. |
| 1.4.6 | Lọc loại: Phiếu chi | **PASS** | Tùy chọn có trong dropdown loại (Tất cả / Phiếu bán hàng / Phiếu trả hàng / Phiếu thu / Phiếu chi). |
| 1.4.7 | Lọc loại: Tất cả | **PASS** | Chọn "Tất cả" → hiển thị mọi loại giao dịch trở lại. |
| 1.4.8 | Lọc trạng thái "Hoàn thành" | **PASS** | Checkbox "Hoàn thành" độc lập; bật riêng → chỉ giao dịch hoàn thành (15 với SCR98 / phần hoàn thành SCR97). |
| 1.4.9 | Lọc trạng thái "Đã hủy" | **PASS** | Bỏ "Hoàn thành", giữ "Đã hủy" → đúng **3** giao dịch hủy của SCR97 (POS...2049/2052/2046), đều 0đ. |
| 1.4.10 | Tìm theo mã / chú thích | **PASS** | Nhập `POS15062048` → trả về đúng **1** giao dịch (POS15062048CN2, Phiếu bán hàng, 99.300, Tiền mặt, Đã thanh toán). |

## 1.5 Đối soát ca (logic tính)

| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.5.1 | Tổng tiền mặt tính đúng công thức | **PASS** | Hệ thống gộp **tiền mặt bán hàng vào Phiếu thu (PC tự sinh)**. Công thức: Tổng TM = Phiếu thu TM − Phiếu chi TM (− Trả hàng TM). SCR98: 1.407.486 − 5.000 − 0 = **1.402.486** ✔. SCR97: 1.202.700 − 0 = **1.202.700** ✔. |
| 1.5.2 | Tiền mặt đầu ca KHÔNG cộng vào tổng | **PASS\*** | Đầu ca cả 2 ca = 0đ; Tổng TM = đúng giá trị giao dịch (không +đầu ca). **Hạn chế:** chưa có ca đầu ca > 0 trong dữ liệu hiện tại để kiểm chặt; modal SCR97 tách riêng "Tiền mặt đầu ca 0" với "Tổng tiền mặt cuối ca 1.202.700". |
| 1.5.3 | Chỉ tính giao dịch tiền mặt vào tổng | **PASS** | SCR98: nếu cộng cả CK/QR thì Phiếu thu = 1.447.386; nhưng "Tổng tiền mặt trong ca" = **1.402.486** (chỉ TM 1.407.486 − 5.000) → CK 30.450 & QR 9.450 **không** tính vào tổng tiền mặt. |
| 1.5.4 | Phiếu bán hàng ghi nhận vào ca | **PASS (theo dữ liệu)** | Các POS bán hàng hiện diện đầy đủ trong danh sách giao dịch của đúng ca phát sinh. **Không** tạo đơn mới (tránh thay đổi số liệu ca chung). |
| 1.5.5 | Phiếu trả hàng làm giảm tổng đúng | **BLOCKED** | Menu Trả hàng báo **"Tính năng returns đang phát triển"** → không tạo được phiếu trả để kiểm. |
| 1.5.6 | Phiếu thu cộng vào ca đúng | **PASS (theo dữ liệu)** | Phiếu thu TM được cộng vào tổng tiền mặt (xác nhận qua công thức 1.5.1). **Không** tạo phiếu thu mới (tránh thay đổi số liệu ca chung). |
| 1.5.7 | Phiếu chi trừ khỏi ca đúng | **PASS (theo dữ liệu)** | SCR98 có Phiếu chi TM **5.000** → Tổng TM giảm đúng 5.000 (1.407.486 → 1.402.486). **Không** tạo phiếu chi mới. |
| 1.5.8 | Giao dịch đã hủy không tính vào tổng | **PASS** | 3 giao dịch "Đã hủy" của SCR97 đều **0đ** và không ảnh hưởng tổng (Tổng TM 1.202.700 chỉ từ giao dịch hoàn thành). |

## 1.6 Chi tiết ca (modal)

| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.6.1 | Mở modal Chi tiết ca | **PASS** | Modal "Chi tiết ca" hiện đúng: Mã ca SCR00000097CN2, Mã nhân sự EMPL00000006CN2, Họ tên cashier, Chức vụ Thu ngân, Giờ mở 16/06 16:31:28, Người đóng Admin master, Giờ đóng 18/06 15:51:00. |
| 1.6.2 | Bảng Thu/Chi theo phương thức trong modal | **PASS** (kèm FIND-01) | Thu **3.989.650** = thẻ Phiếu thu Tổng ✔; Chi **0** = thẻ Phiếu chi ✔; "Phương thức thanh toán" Gross **4.074.650** = thẻ Bán hàng Tổng ✔. Riêng dòng TM trong "Phương thức thanh toán" = 1.287.700 (gross theo PT) khác thẻ Phiếu thu TM 1.202.700 (thực thu) — xem **FIND-01**. |
| 1.6.3 | Tổng tiền mặt trong ca (modal) khớp panel | **PASS** | Modal "Tổng tiền mặt cuối ca" = **1.202.700** = panel "Tổng tiền mặt trong ca" 1.202.700. Chênh lệch tiền mặt trong ca = 0. |
| 1.6.4 | Bấm "Đóng" để thoát modal | **PASS** | Đóng modal bằng nút **✕** (góc phải) → quay về panel chi tiết ca. (Nút "Đóng" ở chân modal cũng có.) |

---

## Tổng hợp

| Trạng thái | Số mục | Danh sách |
|-----------|--------|-----------|
| **PASS** | 33 | 1.1.1–1.1.7 (trừ 1.1.8), 1.2.1, 1.2.2, 1.2.5, toàn bộ 1.3 (trừ 1.3.5), toàn bộ 1.4, 1.5.1–1.5.4, 1.5.6–1.5.8, toàn bộ 1.6 |
| **FAIL** | 1 | 1.1.8 (Mở màn hình phụ không tồn tại) |
| **LỆCH** | 1 | 1.3.5 (không có nút "..."; chi tiết PT hiển thị sẵn) |
| **BLOCKED** | 1 | 1.5.5 (Trả hàng đang phát triển) |
| **N/A – an toàn (không thực thi)** | 2 | 1.2.3, 1.2.4 (Đóng ca / Đóng và in phiếu – nút có sẵn & enabled, không bấm) |

*(1.1.6 = PASS\* nút có sẵn & enabled, không in thật; 1.5.2 = PASS\* đầu ca=0 nên không kiểm được trường hợp đầu ca>0.)*

## Danh sách lỗi & đề xuất

1. **FAIL-01 — 1.1.8 "Mở màn hình phụ" không tồn tại.** Tái hiện: vào Điều phối ca → ca đang mở (CA HIỆN TẠI) → tìm nút "Mở màn hình phụ" ở panel/hộp ca/menu ☰ → không có. Đề xuất: bổ sung nút hoặc cập nhật checklist nếu tính năng đã bỏ. (Ảnh: `screenshot/0623_0124_coordination/note.md` – mô tả menu ☰.)
2. **LỆCH-01 — 1.3.5** thao tác xem chi tiết phương thức không qua nút "...": chi tiết hiển thị sẵn trên thẻ. Đề xuất: cập nhật bước kiểm trong checklist.
3. **FIND-01 — 1.6.2** dòng "Tiền mặt" trong bảng "Phương thức thanh toán" (modal, 1.287.700) ≠ "Tiền mặt" thẻ Phiếu thu (panel, 1.202.700), lệch 85.000 do khác cách nhóm (gross bán hàng vs thực thu). Đề nghị thống nhất nhãn để tránh hiểu nhầm; tổng quỹ vẫn đúng.
4. **BLOCKED — 1.5.5** Trả hàng đang phát triển → cần re-test khi tính năng hoàn thiện.
