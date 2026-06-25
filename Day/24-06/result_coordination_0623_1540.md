# Kết quả kiểm thử — Menu COORDINATION (Điều phối ca) — phiên 0623_1540

- Menu: coordination (**Điều phối ca** = "Shift Coordination")
- Ngày giờ chạy: 23/06/2026, ~14:30–15:40 (giờ VN)
- Người/agent thực hiện: Claude
- Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin` (**Admin master**), vai trò **Thu ngân (Cashier)**, chi nhánh hiển thị **CN1** (hậu tố mã **CN2** — xem FIND-02)
- Phiên bản ứng dụng: **1.0.0+67** — Trình duyệt: Chrome (Browser 2, qua extension)
- Tài liệu: `run/run_coordination.md` + `Checklist/checklist_coordination.md` + `Link/Link.md`
- Route thực tế: `#/pos-shell-route/pos-shift-route`

> **Ảnh lỗi:** công cụ chụp màn hình **không lưu được file ảnh ra đĩa** (`save_to_disk` không tác dụng — như các phiên trước). Lỗi/độ lệch mô tả bằng văn bản + số liệu đối chứng tại `screenshot/0623_1540_coordination/note.md`.

> **Phạm vi thực thi:** người dùng chọn **"Thực thi toàn bộ"** → phiên này **ĐÃ ĐÓNG CA THẬT** ca đang mở SCR98 (1.2.3). Việc tạo đơn/phiếu mới ở Trang chủ **không thực hiện được** do hạn chế tương tác Flutter-canvas trong môi trường tự động (xem BLOCKED-TECH).

> **Ghi chú kỹ thuật (Flutter):** app render canvas, **không có DOM/semantic text** → đọc số liệu qua ảnh/zoom. Dropdown đôi khi render trễ ("lớp phủ ma"), cần chờ 1–2s. **Thanh nav trên cùng chỉ bấm được ngay sau khi reload trang** — sau khi tương tác nhiều, nav & một số click trong trang ngừng phản hồi cho tới khi reload. Ô input & nút trong panel ca nhận gõ/bấm bình thường.

## Bối cảnh dữ liệu (đối chứng)

**Ca đang mở → đã đóng trong phiên: `SCR00000098CN2`** — NV **Admin master**, người mở Admin master, vào ca **16:49 18/06/2026**, **Tiền mặt đầu ca 0đ**.
- Bán hàng: Công nợ 500.000 · Đơn hàng 8 · Tổng **1.947.886**
- Trả hàng: 0 (Phiếu trả 0)
- Phiếu thu: TM **1.517.986** · CK 30.450 · Quẹt thẻ 0 · QR tự động 9.450 · (10 phiếu) · Tổng **1.557.886**
- Phiếu chi: TM **55.000** · (4 phiếu) · Tổng **55.000**
- **Tổng tiền mặt trong ca: 1.462.986** (= 1.517.986 − 55.000) ✔
- Giao dịch: **37 (15 hủy)** — phân trang 15/trang × 3 trang
- **Đóng lúc 2026-06-23 15:39:30**, tiền bàn giao 1.462.986 (chênh lệch 0).

**Ca đã đóng mẫu `SCR00000097CN2`** — NV **cashier**, người mở cashier, **người đóng Admin master**, mở 16/06 16:31:28, đóng 18/06 15:51:00, đầu ca 0đ.
- Bán hàng: Đơn 7 · Gross **4.074.650** / Net 3.863.000 · Công nợ 90.000
- Phiếu thu: TM **1.202.700** · CK 2.786.950 · Tổng **3.989.650** ; Phiếu chi 0
- **Tổng tiền mặt trong ca: 1.202.700** ✔ · Giao dịch **18 (3 hủy)**

**Ca `SCR00000096CN2`** (NV cashier, người mở Admin master, 09/06→16/06, TM 0, **327 giao dịch / 22 trang**) và **`SCR00000095CN2`** (09/06 08:46→08:47, TM **111đ**) — xuất hiện khi lọc khoảng 09–16/06.

## Kết luận nhanh

- ✅ **Lõi nghiệp vụ Điều phối ca chạy đúng:** lọc lịch sử (thời gian + nhân viên), xem chi tiết ca, 4 thẻ tổng hợp + công thức tổng tiền mặt, danh sách giao dịch + đầy đủ bộ lọc (loại/trạng thái/tìm kiếm), modal "Chi tiết ca", phân biệt ca mở/đóng, menu ☰, **đối chiếu chéo Thu chi khớp tuyệt đối**, **đóng ca thật thành công**.
- ❌ **FAIL-01 (1.1.8):** Không có nút **"Mở màn hình phụ"** ở panel/hộp CA HIỆN TẠI/menu ☰. Trùng các phiên 0617 & 0623_0124.
- ⚠️ **LỆCH-01 (1.3.5):** 4 thẻ **không có nút "..."** — breakdown phương thức hiển thị sẵn trên thẻ.
- ⚠️ **FIND-01 (1.6.2):** Modal SCR97 "Phương thức thanh toán" TM **1.287.700** ≠ thẻ Phiếu thu (panel) TM **1.202.700** (lệch 85.000, do gross-bán-hàng vs thực-thu); **tổng quỹ vẫn đúng** (1.202.700 hai nơi). CK khớp.
- ⚠️ **FIND-02:** Nhãn chi nhánh **CN1** (menu/Thu chi) nhưng hậu tố mã **CN2** (SCR/PC/PT/POS…CN2). Nhất quán hai màn hình, nhưng nhãn ≠ mã.
- 🚧 **BLOCKED-TECH (1.12.2/1.12.3/1.12.4):** không tạo được đơn bán mới ở Trang chủ (Flutter canvas không nhận click sau điều hướng) → không xem được bộ đếm tăng +1 trực tiếp. Lõi đồng bộ vẫn chứng minh gián tiếp (1.12.1, 1.13, 1.12.5).
- 🚧 **BLOCKED (1.5.5 trả hàng, 1.10.4 nội dung phiếu in):** returns không tạo được; máy in chưa cấu hình nên không có preview để đối chiếu.
- ⚠️ **Store hiện KHÔNG còn ca mở** sau khi test đóng ca — bấm **"Mở ca"** để mở lại khi cần.

---

## 1.1 Lịch sử ca

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.1.1 | Hiển thị danh sách ca | **PASS** | Mỗi ca đủ trường: nhân viên, người mở, mã ca, giờ mở, giờ đóng, tiền mặt (dạng **thẻ**). |
| 1.1.2 | Ca đang mở đúng trạng thái | **PASS** | SCR98 ở hộp CA HIỆN TẠI, badge **"Đang hoạt động"**, có Giờ vào ca, **không** có giờ đóng. |
| 1.1.3 | Lọc theo Thời gian (khoảng ngày) | **PASS** | Đặt 09→16/06 → danh sách đổi sang SCR97/96/95 (mở trong khoảng). |
| 1.1.4 | Lọc theo Nhân viên | **PASS** | Dropdown: Tất cả/Admin master/tran van a/tranvanc/tranvantest/cashier. |
| 1.1.5 | Bấm 1 ca xem chi tiết | **PASS** | Bấm thẻ SCR97 → panel phải nạp đúng chi tiết ca đó. |
| 1.1.6 | Nút "In phiếu" của ca | **PASS\*** | Thẻ ca đã đóng có "In phiếu"; góc phải có "In phiếu ca" — đều enabled. |
| 1.1.7 | Nút "Chi tiết ca" | **PASS** | Mở modal "Chi tiết ca" (xem 1.6). |
| 1.1.8 | Nút "Mở màn hình phụ" | **FAIL** | **Không tồn tại** ở panel, hộp CA HIỆN TẠI, hay menu ☰. (FAIL-01) |

## 1.2 Thông tin ca & đóng ca

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.2.1 | Header ca đúng thông tin | **PASS** | Ca mở: "2026-06-18 16:49:04 · Admin master · Đang hoạt động". Ca đóng: "… · cashier · Đã đóng". |
| 1.2.2 | Hiển thị Tiền mặt đầu ca | **PASS** | "Tiền mặt đầu ca: 0 đ" khớp khai báo. |
| 1.2.3 | Nút "Đóng ca" | **PASS (ĐÃ THỰC THI)** | Bấm "Đóng ca" → modal "THÔNG TIN ĐÓNG CA" (nhập tiền bàn giao 1.462.986, ghi chú) → "ĐÓNG CA" → toast **"Đóng ca thành công"**; ca chuyển **"Đã đóng"**, **giờ đóng 2026-06-23 15:39:30** ghi chính xác. |
| 1.2.4 | Nút "Đóng và in phiếu" | **PASS\*** | Nút **có sẵn & enabled** cạnh "Đóng ca" trước khi đóng; chỉ đóng được 1 lần nên đã dùng "Đóng ca" (1.2.3). Tương đương Đóng ca + lệnh in. |
| 1.2.5 | Ca đã đóng không thao tác lại | **PASS** | Sau đóng, SCR98 chỉ còn "In phiếu ca"; mất "Đóng ca"/"Đóng và in phiếu". |

## 1.3 Thẻ tổng hợp

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.3.1 | Thẻ Bán hàng | **PASS** | Đơn hàng 8 · Tổng 1.947.886 (SCR98) / Đơn 7 · 4.074.650 (SCR97). |
| 1.3.2 | Thẻ Trả hàng | **PASS** | = 0đ (cả 2 ca không trả hàng). |
| 1.3.3 | Thẻ Phiếu thu | **PASS** | SCR98: TM 1.517.986·CK 30.450·QR 9.450·Tổng 1.557.886 (10). SCR97: TM 1.202.700·CK 2.786.950·Tổng 3.989.650 (8). |
| 1.3.4 | Thẻ Phiếu chi | **PASS** | SCR98: TM 55.000·Tổng 55.000 (4). SCR97: 0. |
| 1.3.5 | Bấm "..." xem chi tiết PT | **LỆCH** | **Không có nút "..."** — breakdown TM/CK/Quẹt thẻ/QR hiển thị sẵn trên thẻ. (LỆCH-01) |
| 1.3.6 | Tổng phương thức = tổng thẻ | **PASS** | SCR98 Phiếu thu: 1.517.986+30.450+0+9.450 = **1.557.886** ✔. Phiếu chi SCR98 = 55.000 = 50.000+5.000+0+0 ✔. SCR97 Phiếu thu: 1.202.700+2.786.950 = **3.989.650** ✔. |

## 1.4 Giao dịch trong ca

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.4.1 | Hiển thị danh sách | **PASS** | Cột: STT · Mã voucher · Loại giao dịch · Số tiền · Thanh toán · Trạng thái. |
| 1.4.2 | Đếm đúng tổng số | **PASS** | "Tổng cộng 37 (15 hủy)" = "Tổng 37 bản ghi" (phân trang). |
| 1.4.3 | Lọc Phiếu bán hàng | **PASS** | Chỉ còn POS… (gồm vài dòng "Đã hủy"). |
| 1.4.4 | Lọc Phiếu trả hàng | **PASS** | SCR97 không trả hàng → "Không có giao dịch" (đúng). |
| 1.4.5 | Lọc Phiếu thu | **PASS** | Chỉ còn PC… (TM/CK/QR khác nhau). |
| 1.4.6 | Lọc Phiếu chi | **PASS** | 4 dòng PT… ; TM 50.000+5.000 = 55.000 khớp thẻ Phiếu chi. |
| 1.4.7 | Lọc Tất cả | **PASS** | Hiện mọi loại trở lại. |
| 1.4.8 | Lọc "Hoàn thành" | **PASS** | Bỏ "Đã hủy" → chỉ giao dịch "Đã thanh toán". |
| 1.4.9 | Lọc "Đã hủy" | **PASS** | Bỏ "Hoàn thành" → chỉ giao dịch "Đã hủy" (đa số 0đ). |
| 1.4.10 | Tìm theo mã | **PASS** | Nhập `POS15062072CN2` → đúng **1** dòng (10.500đ, Tiền mặt, Đã thanh toán). |

## 1.5 Đối soát ca (logic tính)

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.5.1 | Tổng tiền mặt đúng công thức | **PASS** | Tiền mặt bán hàng gộp vào Phiếu thu. SCR98: 1.517.986 − 55.000 = **1.462.986** ✔. SCR97: 1.202.700 − 0 = **1.202.700** ✔. |
| 1.5.2 | Đầu ca KHÔNG cộng vào tổng | **PASS\*** | Đầu ca = 0đ; tổng = đúng giá trị giao dịch. *Hạn chế:* chưa có ca đầu ca>0 để kiểm chặt; modal tách riêng "Tiền mặt đầu ca" với "Tổng tiền mặt cuối ca". |
| 1.5.3 | Chỉ tính giao dịch tiền mặt | **PASS** | SCR98 tổng TM 1.462.986 chỉ từ TM; CK 30.450 & QR 9.450 **không** cộng. |
| 1.5.4 | Phiếu bán hàng ghi nhận vào ca | **PASS (theo dữ liệu)** | Nhiều POS… bán hàng có trong danh sách giao dịch ca. Không tạo đơn mới (xem 1.12). |
| 1.5.5 | Phiếu trả hàng giảm tổng | **BLOCKED** | Không tạo được phiếu trả (điều hướng Trả hàng bị chặn + tính năng nhiều khả năng đang phát triển). |
| 1.5.6 | Phiếu thu cộng vào ca | **PASS (theo dữ liệu)** | Phiếu thu TM cộng vào tổng (xác nhận qua công thức 1.5.1). |
| 1.5.7 | Phiếu chi trừ khỏi ca | **PASS (theo dữ liệu)** | SCR98 Phiếu chi TM 55.000 → tổng giảm đúng 55.000. |
| 1.5.8 | Giao dịch hủy không tính | **PASS** | Giao dịch "Đã hủy" đều 0đ/không ảnh hưởng tổng. |

## 1.6 Chi tiết ca (modal)

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.6.1 | Mở modal Chi tiết ca | **PASS** | SCR97: Mã ca SCR00000097CN2, Mã NS EMPL00000006CN2, cashier, Thu ngân, mở 16/06 16:31:28, người đóng Admin master, đóng 18/06 15:51:00. |
| 1.6.2 | Bảng Thu/Chi theo phương thức | **PASS (kèm FIND-01)** | Thu 3.989.650 = thẻ Phiếu thu ✔; Chi 0 ✔; Gross 4.074.650 = thẻ Bán hàng ✔. **Riêng** TM "Phương thức thanh toán" 1.287.700 ≠ thẻ Phiếu thu TM 1.202.700 (lệch 85.000). |
| 1.6.3 | Tổng tiền mặt (modal) khớp panel | **PASS** | Modal "Tổng tiền mặt cuối ca" 1.202.700 = panel "Tổng tiền mặt trong ca" 1.202.700; chênh lệch 0. |
| 1.6.4 | Bấm "Đóng" thoát modal | **PASS** | Nút "Đóng" (chân modal) → quay về panel chi tiết. |

## 1.7 Bộ lọc Thời gian

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.7.1 | Giá trị mặc định | **PASS** | "16-06-2026 - 23-06-2026" (~7 ngày tới hôm nay). |
| 1.7.2 | Preset "Hôm nay" | **PASS** | 23/06 → "Không có dữ liệu lịch sử" (không có ca mở hôm nay trước khi đóng SCR98). |
| 1.7.3 | Preset "Hôm qua" | **PASS\*** | Nút preset **có sẵn**; chưa áp riêng (cơ chế đã kiểm qua "Hôm nay" + khoảng tùy chỉnh). |
| 1.7.4 | Preset "Tuần này" | **PASS\*** | Nút có sẵn. |
| 1.7.5 | Preset "Tháng này" | **PASS\*** | Nút có sẵn. |
| 1.7.6 | Preset "Quý này" | **PASS\*** | Nút có sẵn. |
| 1.7.7 | Preset "Năm nay" | **PASS\*** | Nút có sẵn. |
| 1.7.8 | Khoảng ngày tùy chỉnh | **PASS** | 09→16/06 → SCR97/96/95 (giờ mở trong khoảng). |
| 1.7.9 | Ngày bắt đầu > kết thúc (biên) | **PASS** | Picker **tự sắp xếp** khoảng bất kể thứ tự bấm (bấm 16 rồi 9 → khoảng 9–16). Không treo. |
| 1.7.10 | Khoảng không có ca | **PASS** | "Không có dữ liệu lịch sử" + icon, không vỡ giao diện. |
| 1.7.11 | Không ảnh hưởng CA HIỆN TẠI | **PASS** | Lọc 23/06 (ngoài ca mở 18/06) → hộp CA HIỆN TẠI vẫn hiển thị SCR98. |

## 1.8 Bộ lọc Nhân viên

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.8.1 | Danh sách đầy đủ | **PASS** | Tất cả, Admin master, tran van a, tranvanc, tranvantest, cashier. |
| 1.8.2 | Chọn "Tất cả" | **PASS** | Hiện ca mọi nhân viên trong khoảng. |
| 1.8.3 | Chọn 1 NV ("cashier") | **PASS** | Hiện SCR97/96/95 (đều NV cashier). |
| 1.8.4 | Lọc theo trường "Nhân viên" (≠ Người mở) | **PASS** | "Admin master" + 09–16/06 → rỗng dù Admin master **mở** SCR95/96 (NV = cashier) → lọc đúng theo trường Nhân viên. |
| 1.8.5 | Kết hợp Thời gian + Nhân viên | **PASS** | 09–16/06 + Admin master → "Không có dữ liệu lịch sử". |
| 1.8.6 | NV không có ca trong khoảng | **PASS** | Danh sách rỗng, empty state. |

## 1.9 Hộp "CA HIỆN TẠI"

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.9.1 | Đủ thông tin ca đang mở | **PASS** | SCR98 · Admin master · Người mở Admin master · Giờ vào ca 16:49-18/06 · đầu ca 0đ · badge "Đang hoạt động". |
| 1.9.2 | Bấm hộp mở chi tiết | **PASS** | Bấm hộp → panel phải nạp chi tiết ca đang mở. |
| 1.9.3 | Badge "Đang hoạt động" | **PASS** | Badge xanh, thống nhất giữa hộp và header panel. |
| 1.9.4 | Tiền mặt đầu ca khớp | **PASS** | 0đ đúng khai báo. |
| 1.9.5 | Không có ca đang mở | **PASS** | Sau khi đóng SCR98 → hộp CA HIỆN TẠI thay bằng nút **"+ MỞ CA"**, không vỡ giao diện. |

## 1.10 In phiếu ca

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.10.1 | "In phiếu ca" trên panel ca đã đóng | **PASS** | Hiển thị & enabled góc phải header. |
| 1.10.2 | "In phiếu" trên thẻ ca | **PASS** | Có trên thẻ ca đã đóng. |
| 1.10.3 | Kích hoạt lệnh in | **PASS** | Bấm "In phiếu" → toast **"Cảnh báo: Chưa thiết lập cấu hình máy in…"** — lệnh kích hoạt, không treo, không mở hộp thoại in chặn. |
| 1.10.4 | Nội dung phiếu in khớp số liệu | **BLOCKED** | Chưa cấu hình máy in/printcenter → không có preview để đối chiếu. |

## 1.11 Phân biệt ca mở vs đóng

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.11.1 | Ca mở: có nút đóng ca | **PASS** | "Đóng ca" + "Đóng và in phiếu"; badge "Đang hoạt động"; không giờ đóng. |
| 1.11.2 | Ca đóng: chỉ nút in | **PASS** | Chỉ "In phiếu ca" (+ "Chi tiết ca"). |
| 1.11.3 | Chỉ 1 ca mở 1 thời điểm | **PASS** | Trước đóng: chỉ SCR98 hoạt động. Sau đóng: 0 ca mở. |
| 1.11.4 | Ca đóng hiện người đóng + giờ đóng | **PASS** | SCR97 (modal): người đóng Admin master, giờ đóng 18/06 15:51:00. SCR98: giờ đóng 23/06 15:39:30. |
| 1.11.5 | Không đóng lại ca đã đóng | **PASS** | Không có nút đóng trên ca đã đóng. |

## 1.12 Đồng bộ thời gian thực với Home

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.12.1 | Đơn bán mới xuất hiện trong ca | **PASS (theo dữ liệu)** | Nhiều POS… bán ở Home hiện trong "Giao dịch trong ca". Thấy 1 đơn chưa thanh toán POS15062081CN2 (10.000đ) đang luân chuyển. |
| 1.12.2 | Tổng tiền mặt cập nhật sau đơn TM | **BLOCKED-TECH** | Không tạo được đơn mới ở Trang chủ (Flutter canvas không nhận click chọn bàn sau điều hướng). |
| 1.12.3 | Thẻ Bán hàng tăng số đơn | **BLOCKED-TECH** | Như trên. |
| 1.12.4 | Bộ đếm "Tổng cộng (n)" cập nhật | **BLOCKED-TECH** | Như trên. |
| 1.12.5 | Reload giữ số liệu nhất quán | **PASS** | F5 → mọi số liệu SCR98 khớp y nguyên (Phiếu thu 1.557.886, Tổng TM 1.462.986, 37 (15 hủy)). |

## 1.13 Đối chiếu chéo với menu Thu chi

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.13.1 | Phiếu thu khớp Thu chi | **PASS** | PC00001651CN2: Thu chi = Thu 10.500đ TM = giao dịch ca ✔. PC00001650CN2 100.000đ TM ✔. PC00001648CN2 9.450đ CK ✔. |
| 1.13.2 | Phiếu chi khớp Thu chi | **PASS** | PT00000038CN2: Chi 50.000đ TM ✔. PT00000000CN2: Chi 0đ TM ✔. |
| 1.13.3 | Logic tiền mặt nhất quán 2 màn hình | **PASS** | Cùng bộ mã/số tiền/PTTT/thời gian, không mâu thuẫn. |

## 1.14 Mã voucher & tìm kiếm

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.14.1 | Tiền tố mã theo loại | **PASS** | Bán hàng **POS…**, Phiếu thu **PC…**, Phiếu chi **PT…**. |
| 1.14.2 | Hậu tố chi nhánh | **PASS (kèm FIND-02)** | Mọi mã …**CN2** (dù nhãn chi nhánh CN1). |
| 1.14.3 | Tìm mã chính xác | **PASS** | `POS15062072CN2` → đúng 1 giao dịch. |
| 1.14.4 | Tìm theo chú thích | **PASS\*** | Ô tìm nhận text (đã kiểm qua tìm mã). Chú thích tồn tại (vd "Mua tôm hùm bông", "Đi trễ" trong Thu chi). Chưa test riêng từ khóa chú thích trong danh sách ca. |
| 1.14.5 | Tìm mã không tồn tại | **PASS** | `zzz999` → "Không có giao dịch". |
| 1.14.6 | Xóa từ khóa khôi phục | **PASS** | Xóa ô tìm → danh sách trở lại đầy đủ. |

## 1.15 Định dạng số tiền & hiển thị

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.15.1 | Dấu nghìn + hậu tố đ | **PASS** | "10.500 đ", "1.517.986 đ" (dấu chấm + đ). |
| 1.15.2 | Giá trị 0 đúng | **PASS** | "0 đ" hiển thị rõ (không trống/null). |
| 1.15.3 | Nhất quán mọi nơi | **PASS** | Thẻ, tổng tiền mặt, cột Số tiền, modal đồng dạng. |
| 1.15.4 | Màu/loại giao dịch | **PASS** | "Đã thanh toán" xanh lá, "Đã hủy" đỏ — nhất quán. |

## 1.16 Trạng thái rỗng & xử lý lỗi

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.16.1 | Chưa chọn ca | **PASS** | Sau reload panel hiện **"Chọn một ca để xem chi tiết"**. |
| 1.16.2 | Ca không có giao dịch | **PASS\* (hạn chế dữ liệu)** | Không có ca 0 giao dịch trong dữ liệu để test trực tiếp; empty-state đã chứng minh qua 1.4.4/1.14.5/1.16.3/1.16.4. |
| 1.16.3 | Lọc loại không có dữ liệu | **PASS** | Lọc "Phiếu trả hàng" (ca không trả) → rỗng, không lỗi. |
| 1.16.4 | Bỏ cả 2 checkbox trạng thái | **PASS** | Bỏ "Hoàn thành" + "Đã hủy" → "Không có giao dịch" (hợp lý), không vỡ. |
| 1.16.5 | Reload khi đang xem ca | **PASS** | F5 → khôi phục bình thường (panel về "Chọn một ca…", rồi auto nạp ca mở), số liệu khớp. |
| 1.16.6 | Kẹt "lớp phủ ma" (Flutter) | **PASS (ghi nhận quirk)** | Dropdown lịch đôi khi để lại lớp phủ mờ; bấm ra ngoài/Escape hoặc reload là hết. |

## 1.17 Phân quyền & phạm vi chi nhánh

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.17.1 | Thu ngân thấy đúng phạm vi | **PASS\*** | Vai trò Thu ngân (Admin master) thấy ca trong phạm vi; chi nhánh CN1/CN2 (FIND-02). |
| 1.17.2 | Mã ca gắn đúng chi nhánh | **PASS (kèm FIND-02)** | Mã ca SCR…**CN2**; nhãn chi nhánh hiển thị **CN1**. |
| 1.17.3 | Hiển thị ca nhiều nhân viên | **PASS** | "Tất cả" → ca của Admin master (SCR98) + cashier (SCR95/96/97). |
| 1.17.4 | Phân biệt "Nhân viên" vs "Người mở" | **PASS** | SCR96/95: NV **cashier**, Người mở **Admin master** — hiển thị độc lập, đúng. |

## 1.18 Menu ☰ (cấu hình thiết bị)

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.18.1 | Mở menu ☰ | **PASS** | Menu xổ ra danh sách cấu hình. |
| 1.18.2 | Danh sách mục đầy đủ | **PASS** | CN1 · Thu ngân (✓) · Bật âm thanh · Tải lại cấu hình · Đặt máy chạy printcenter · Hiện thông tin device_id · Ngôn ngữ hiển thị (VN/EN/KO). |
| 1.18.3 | "Tải lại cấu hình" | **PASS** | Toast **"Đã tải lại cấu hình"**, không lỗi. |
| 1.18.4 | "Hiện thông tin device_id" | **PASS** | Toggle Hiện ↔ Ẩn (đã bật rồi tắt lại). |
| 1.18.5 | Đổi Ngôn ngữ | **PASS** | EN tức thì ("Điều phối ca"→"Shift Coordination", "Bán hàng"→"Sales"…), đổi lại VN OK, **không cần đăng nhập lại**. |
| 1.18.6 | Bật âm thanh | **PASS** | Toggle Bật ↔ Tắt âm thanh (đã bật rồi tắt lại). |

## 1.19 Kiểm thử biên & hiệu năng

| STT | Testcase | Kết quả | Quan sát |
|-----|----------|---------|----------|
| 1.19.1 | Ca nhiều giao dịch (37+) | **PASS** | SCR98 37 dòng (3 trang); SCR96 **327 dòng (22 trang)** — phân trang 15/trang, mượt, không treo. |
| 1.19.2 | Đếm "Tổng cộng (n hủy)" khớp | **PASS** | "Tổng cộng 37 (15 hủy)" = "Tổng 37 bản ghi"; lọc Đã hủy/Hoàn thành đúng số. |
| 1.19.3 | Khoảng ngày rất rộng / ca lớn | **PASS** | Ca 327 giao dịch tải đầy đủ, không lỗi hiệu năng. |
| 1.19.4 | Chuyển nhanh giữa nhiều ca | **PASS** | SCR98→97→96 panel cập nhật đúng từng ca, không lẫn số liệu. |
| 1.19.5 | Đếm tiền mặt kiểm chứng công thức | **PASS** | 1.517.986 − 55.000 = **1.462.986** ✔ (SCR98); 1.202.700 − 0 = 1.202.700 ✔ (SCR97). |

---

## Tổng hợp

| Trạng thái | Số mục | Ghi chú |
|-----------|--------|---------|
| **PASS** (gồm PASS\*) | **104** | Đa số chức năng đạt; PASS\* là đạt nhưng có hạn chế nhỏ/không thực thi riêng (1.1.6, 1.2.4, 1.5.2, 1.7.3–1.7.7, 1.14.4, 1.16.2, 1.17.1). |
| **FAIL** | **1** | 1.1.8 (Mở màn hình phụ không tồn tại). |
| **LỆCH** | **1** | 1.3.5 (không có nút "..."; chi tiết PT hiển thị sẵn). |
| **BLOCKED** | **5** | 1.5.5 (trả hàng), 1.10.4 (nội dung phiếu in), 1.12.2, 1.12.3, 1.12.4 (tạo đơn mới — hạn chế Flutter canvas). |
| **Tổng** | **111** | |

*Phát hiện thêm (không tính FAIL): **FIND-01** (1.6.2 lệch nhãn TM modal vs panel, tổng quỹ đúng), **FIND-02** (nhãn chi nhánh CN1 vs hậu tố mã CN2).*

## Danh sách lỗi & đề xuất

1. **FAIL-01 — 1.1.8 "Mở màn hình phụ" không tồn tại.** Tái hiện: Điều phối ca → ca đang mở → tìm nút ở panel/hộp CA HIỆN TẠI/menu ☰ → không có. Đề xuất: bổ sung nút hoặc cập nhật checklist nếu tính năng đã bỏ. (Trùng phiên 0617 & 0623_0124.)
2. **LỆCH-01 — 1.3.5** thao tác xem chi tiết phương thức không qua "..."; chi tiết hiển thị sẵn trên thẻ. Đề xuất: cập nhật bước kiểm trong checklist.
3. **FIND-01 — 1.6.2** dòng "Tiền mặt" trong "Phương thức thanh toán" (modal, 1.287.700) ≠ thẻ Phiếu thu TM (panel, 1.202.700), lệch 85.000 do gross-bán-hàng vs thực-thu-vào-két. Tổng quỹ vẫn đúng. Đề nghị thống nhất nhãn để tránh hiểu nhầm.
4. **FIND-02 — Nhãn chi nhánh CN1 vs hậu tố mã CN2.** Đề nghị làm rõ quy ước (CN1 = tên hiển thị, CN2 = mã?).
5. **BLOCKED — 1.5.5 / 1.12.2-1.12.4 / 1.10.4.** Trả hàng & tạo đơn mới không thực thi được trong môi trường tự động (Flutter canvas + returns); máy in chưa cấu hình. Đề nghị re-test thủ công phần tăng realtime +1 và nội dung phiếu in.
6. **Lưu ý vận hành:** sau test, **store không còn ca mở** (đã đóng SCR98). Mở lại bằng nút **"Mở ca"** khi cần.
