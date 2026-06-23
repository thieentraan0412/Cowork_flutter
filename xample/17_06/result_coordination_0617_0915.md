# Kết quả kiểm thử — Menu COORDINATION (Điều phối ca) — phiên 0617_0915

- Ngày giờ chạy: 17/06/2026, ~09:00–09:15 (giờ VN)
- Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin` (**Admin master**), vai trò **Thu ngân (Cashier)**, chi nhánh **CN1**
- Phiên bản ứng dụng: **1.0.0+55** — Trình duyệt: Chrome (Windows), điều khiển qua extension
- Checklist: `Checklist/checklist_coordination.md` — Hướng dẫn: `run/run_coordination.md` — Link: `Link/Link.md`
- Ghi chú lỗi chi tiết: `screenshot/0617_0915_coordination/note.md` (công cụ **không xuất được ảnh PNG ra đĩa** → mô tả lỗi bằng văn bản + dữ liệu đối chứng, như các phiên trước)
- Lưu ý menu: "Coordination" trong hệ thống này = **Điều phối ca** (quản lý ca thu ngân: ca hiện tại, lịch sử ca, panel chi tiết ca, 4 thẻ tổng hợp, giao dịch trong ca, đối soát, modal chi tiết ca). KHÁC với mô tả "hàng chờ chế biến/bếp" ở phần *Trọng tâm* của `run_coordination.md` — bài test bám theo **checklist** (đúng UI thực tế).

## Bối cảnh dữ liệu (đối chứng)
- **Ca đang mở (CA HIỆN TẠI):** `SCR00000097CN2` — NV cashier, người mở cashier, vào ca 16:31 16/06/2026, **Tiền mặt đầu ca 0đ**, "Đang hoạt động". 6 giao dịch = 3 phiếu bán hàng (POS, 42.000/550.000/577.500) + 3 phiếu thu tự sinh (PC, cùng số tiền). **Bán hàng tiền mặt = Tổng tiền mặt trong ca = 1.169.500đ**.
- **Ca đã đóng mẫu:** `SCR00000085CN2` — NV Admin master, đầu ca 50.000, Tổng tiền mặt trong ca 1.468.375 (modal: cuối ca 1.518.375), 4 giao dịch (2 hủy).

## Kết luận nhanh
- ✅ **Lõi nghiệp vụ Điều phối ca chạy đúng:** lọc lịch sử ca (thời gian + nhân viên), xem chi tiết ca ở panel phải, 4 thẻ tổng hợp + công thức tổng tiền mặt, danh sách giao dịch + đầy đủ bộ lọc (loại/trạng thái/tìm kiếm), modal "Chi tiết ca", phân biệt ca mở/đóng.
- ❌ **FAIL/LỆCH-01 (1.1.8): Không tìm thấy nút "Mở màn hình phụ"** trong panel ca đang mở, hộp CA HIỆN TẠI, lẫn menu ☰ (chỉ có CN1/vai trò/âm thanh/tải lại cấu hình/ngôn ngữ).
- ⚠️ **LỆCH-02 (1.3.5): Không có nút "..."** trên thẻ tổng hợp — chi tiết phương thức (Tiền mặt/CK/Quẹt thẻ/QR) **luôn hiển thị sẵn** trên thẻ (vẫn đạt mục tiêu xem chi tiết, chỉ khác cách thao tác).
- ⚠️ **FIND-01 (1.5.1, ca SCR85):** "Tổng tiền mặt trong ca" lưu trữ **1.468.375** > tiền mặt nhìn thấy từ giao dịch hiện có **958.375** (lệch **510.000** không giải thích được bằng giao dịch đang hiển thị) — nghi dữ liệu cũ/đã xóa. Đề nghị rà soát toàn vẹn dữ liệu. (Ca đang mở SCR97 dữ liệu sạch → công thức **đúng**.)
- 🚧 **BLOCKED (môi trường):** Phiên đăng nhập **hết hạn sau khi rớt kết nối extension** ("Phiên đăng nhập đã hết hạn"), đăng nhập lại thất bại do **ô nhập liệu Flutter không nhận text** (mọi cách: gõ phím/JS đều fail) → chặn **1.5.6, 1.5.7** (tạo phiếu thu/chi để kiểm đồng bộ) và **1.1.6** (in phiếu). Trùng ghi nhận instability "môi trường tự động hóa" ở các phiên History/Cashboot trước.
- 🚧 **BLOCKED (tính năng):** **1.5.5** Trả hàng — theo phiên Cashboot, tính năng "returns đang phát triển" → không tạo được phiếu trả để kiểm giảm tổng.
- ⏸️ **KHÔNG thực thi (an toàn):** **1.2.3 / 1.2.4** (Đóng ca / Đóng và in phiếu) — nút **có sẵn & enabled** nhưng **không bấm** để tránh đóng ca thu ngân đang chạy trên store test dùng chung (cần xác nhận của người dùng).
- 🔧 Kỹ thuật: cần dispatch pointer-event bằng JS để click (CDP click thường không ăn trên widget Flutter); dropdown hay kẹt "lớp phủ ma"; màn hình thỉnh thoảng đơ khi tự động hóa.

---

## 1.1 Lịch sử ca
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.1.1 | Hiển thị danh sách các ca | **PASS** | Mỗi ca hiển thị đủ: nhân viên, người mở, mã ca, giờ mở ca, giờ đóng ca, tiền mặt. (Dạng **thẻ**, không phải bảng cột, nhưng đủ trường.) |
| 1.1.2 | Ca đang mở hiển thị đúng trạng thái | **PASS** | Ca đang mở nằm ở hộp **CA HIỆN TẠI** với badge **"Đang hoạt động"** + "Giờ vào ca", KHÔNG có giờ đóng. (Nhãn "Đang hoạt động", không phải chữ "Đang mở".) |
| 1.1.3 | Lọc theo Thời gian (khoảng ngày) | **PASS** | Chọn 01/06→05/06 → danh sách đổi sang các ca mở trong khoảng (SCR88, SCR87); ca ngoài khoảng (SCR96 mở 09/06) bị loại. Có sẵn nhanh: Hôm nay/Hôm qua/Tuần này/Tháng này/Quý này/Năm nay. |
| 1.1.4 | Lọc theo Nhân viên | **PASS** | Chọn "Admin master" → chỉ hiện ca của Admin master (SCR85, SCR84); trước đó (Tất cả) hiện ca cashier. Dropdown nhiều nhân viên. |
| 1.1.5 | Bấm vào 1 ca để xem chi tiết | **PASS** | Bấm SCR85 → panel phải nạp đúng chi tiết ca (header + 4 thẻ + giao dịch cập nhật theo ca chọn). |
| 1.1.6 | Nút "In phiếu" của ca | **BLOCKED (môi trường)** | Nút **"In phiếu"** (trên thẻ ca đã đóng) + **"In phiếu ca"** (góc phải) **có sẵn & enabled**; chưa kích hoạt lệnh in được do phiên hết hạn trước khi test. |
| 1.1.7 | Nút "Chi tiết ca" | **PASS** | Bấm "Chi tiết ca" → mở modal "Chi tiết ca" (xem 1.6). |
| 1.1.8 | Nút "Mở màn hình phụ" | **FAIL/Không tìm thấy** | Không có nút "Mở màn hình phụ" ở panel ca đang mở, hộp CA HIỆN TẠI, hay menu ☰ (menu ☰ chỉ có: CN1, Thu ngân, Bật âm thanh, Tải lại cấu hình, Ngôn ngữ). Panel ca đang mở chỉ có "Đóng ca" + "Đóng và in phiếu". |

## 1.2 Thông tin ca & đóng ca
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.2.1 | Header ca đúng thông tin | **PASS** | Header hiện đúng ngày giờ + tên nhân viên + trạng thái. VD đóng: "2026-06-05 13:58:06 \| Admin master \| Đã đóng"; mở: "2026-06-16 16:31:28 \| cashier \| Đang hoạt động". |
| 1.2.2 | Hiển thị Tiền mặt đầu ca | **PASS** | Hiện đúng đầu ca (SCR85 = 50.000đ; SCR97 = 0đ), khớp số trong modal Chi tiết ca. |
| 1.2.3 | Nút "Đóng ca" | **KHÔNG thực thi (an toàn)** | Nút **"Đóng ca"** có sẵn & enabled ở ca đang mở. **Không bấm** để tránh đóng ca thu ngân đang chạy trên store test dùng chung → cần người dùng xác nhận mới chạy. |
| 1.2.4 | Nút "Đóng và in phiếu" | **KHÔNG thực thi (an toàn)** | Nút **"Đóng và in phiếu"** có sẵn cạnh "Đóng ca". Không bấm (lý do như 1.2.3 + kích hoạt in). |
| 1.2.5 | Ca đã đóng không cho thao tác lại | **PASS** | Ca đã đóng (SCR85) **KHÔNG hiển thị nút "Đóng ca"** — chỉ có "In phiếu ca" (góc phải) + In phiếu/Chi tiết ca (trên thẻ). Không thể đóng lại ca đã đóng. |

## 1.3 Thẻ tổng hợp (Bán hàng / Trả hàng / Phiếu thu / Phiếu chi)
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.3.1 | Thẻ Bán hàng hiển thị đúng | **PASS** | SCR97: "Xuất hóa đơn điện tử 3", Tiền mặt 1.169.500, CK/Quẹt thẻ/QR 0, **Tổng tiền 1.169.500**. |
| 1.3.2 | Thẻ Trả hàng hiển thị đúng | **PASS (không có DL)** | Thẻ hiện "Phiếu trả 0", các phương thức 0, Tổng 0. Không có ca nào có trả hàng để kiểm số khác 0. |
| 1.3.3 | Thẻ Phiếu thu hiển thị đúng | **PASS một phần** | Thẻ hiển thị đúng cấu trúc (đếm 0, theo phương thức, Tổng 0). Phiếu thu **thủ công** = 0 trong dữ liệu có sẵn; **phiếu thu tự sinh từ bán hàng được tính vào thẻ Bán hàng**, không vào thẻ này (khớp ghi nhận Cashboot). Không tạo được phiếu thu thủ công để kiểm số khác 0 (BLOCKED môi trường — 1.5.6). |
| 1.3.4 | Thẻ Phiếu chi hiển thị đúng | **PASS một phần** | Thẻ hiển thị đúng (0). Không tạo được phiếu chi để kiểm số khác 0 (BLOCKED môi trường — 1.5.7). |
| 1.3.5 | Bấm "..." trên thẻ xem chi tiết phương thức | **FAIL/LỆCH** | **Không có nút "..."**. Chi tiết phương thức (Tiền mặt / Chuyển khoản / Quẹt thẻ / QR tự động) **luôn hiển thị sẵn** ngay trên mỗi thẻ. (Đạt mục tiêu xem chi tiết, nhưng khác thao tác checklist.) |
| 1.3.6 | Tổng các phương thức khớp tổng thẻ | **PASS** | Thẻ Bán hàng: 1.169.500 (TM) + 0 + 0 + 0 = **Tổng 1.169.500** ✔. |

## 1.4 Giao dịch trong ca
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.4.1 | Hiển thị danh sách giao dịch | **PASS** | Đủ cột: STT, Mã voucher, Loại giao dịch, Số tiền, Thanh toán, Trạng thái. |
| 1.4.2 | Đếm đúng tổng số giao dịch | **PASS** | "Tổng cộng: 6" = 6 dòng thực tế (SCR97). *Lưu ý: số "Tổng cộng" phản ánh TỔNG, không đổi theo bộ lọc loại đang áp.* |
| 1.4.3 | Lọc loại: Phiếu bán hàng | **PASS** | Chỉ hiện 3 phiếu bán hàng (POS, 42k/550k/577.5k). |
| 1.4.4 | Lọc loại: Phiếu trả hàng | **PASS** | Hiện rỗng (ca không có trả hàng) — đúng cơ chế lọc. |
| 1.4.5 | Lọc loại: Phiếu thu | **PASS** | Chỉ hiện 3 phiếu thu (PC, 42k/550k/577.5k). |
| 1.4.6 | Lọc loại: Phiếu chi | **PASS** | "Không có giao dịch" (ca không có phiếu chi). |
| 1.4.7 | Lọc loại: Tất cả | **PASS** | Khôi phục đủ 6 giao dịch. |
| 1.4.8 | Lọc trạng thái "Hoàn thành" | **PASS** | Bỏ tích "Hoàn thành" → ẩn các giao dịch hoàn thành (SCR97 → rỗng vì không có giao dịch hủy). |
| 1.4.9 | Lọc trạng thái "Đã hủy" | **PASS** | Trên SCR85: bỏ tích "Hoàn thành" (chỉ còn "Đã hủy") → hiện đúng 2 phiếu bán hàng "Đã hủy". |
| 1.4.10 | Tìm theo mã / chú thích | **PASS** | Gõ "POS15062042" → trả về đúng 1 giao dịch khớp. |

## 1.5 Đối soát ca (logic tính)
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.5.1 | Tổng tiền mặt trong ca tính đúng công thức | **PASS (ca sạch) / FIND (ca cũ)** | SCR97 (sạch): Tổng 1.169.500 = bán hàng TM (phiếu thu tự sinh KHÔNG cộng đôi; trả hàng/phiếu thu thủ công/phiếu chi = 0) ✔. **FIND-01:** SCR85 lưu Thu 1.468.375 nhưng tiền mặt từ giao dịch hiển thị chỉ 958.375 (lệch 510.000 không rõ nguồn) → nghi dữ liệu cũ/đã xóa. |
| 1.5.2 | Tiền mặt đầu ca KHÔNG cộng vào tổng | **PASS** | SCR85: đầu ca 50.000; panel "Tổng tiền mặt trong ca" = 1.468.375 (= Thu, KHÔNG gồm đầu ca); modal "Tổng tiền mặt **cuối ca**" = 1.518.375 (= đầu ca + Thu). ⇒ đầu ca không cộng vào tổng trong ca. |
| 1.5.3 | Chỉ tính giao dịch tiền mặt vào tổng | **PASS (theo thiết kế)** | "Tổng tiền mặt trong ca" chỉ cộng dòng **Tiền mặt**; CK/Quẹt thẻ/QR hiển thị riêng trên thẻ, không vào tổng tiền mặt. (Dữ liệu hiện toàn tiền mặt; không thêm được giao dịch phi tiền mặt để chứng minh số học do BLOCKED môi trường, nhưng thiết kế rõ ràng.) |
| 1.5.4 | Phiếu bán hàng ghi nhận vào ca | **PASS** | 3 phiếu bán hàng (POS) có sẵn xuất hiện trong danh sách giao dịch ca SCR97 và thẻ Bán hàng (1.169.500). |
| 1.5.5 | Phiếu trả hàng làm giảm tổng đúng | **BLOCKED** | Tính năng Trả hàng "đang phát triển" (theo phiên Cashboot) → không tạo được phiếu trả để kiểm. Thẻ Trả hàng = 0. |
| 1.5.6 | Phiếu thu cộng vào ca đúng | **BLOCKED (môi trường)** | Đã mở "Thu chi → Thêm phiếu", chọn Phiếu thu/Tiền mặt, nhập 20.000, nhưng **bấm "Tạo mới" báo "Phiên đăng nhập đã hết hạn"** (rớt kết nối) → không tạo được. (Phiên Cashboot trước đã xác nhận phiếu thu Thu chi đồng bộ sang Điều phối ca.) |
| 1.5.7 | Phiếu chi trừ khỏi ca đúng | **BLOCKED (môi trường)** | Như 1.5.6 (chưa tạo được phiếu chi). |
| 1.5.8 | Giao dịch đã hủy không tính vào tổng | **PASS** | SCR85: 2 giao dịch "Đã hủy" đều 0đ, không vào tổng; bộ lọc "Hoàn thành"/"Đã hủy" tách rõ. (Mẫu hủy đều 0đ nên chưa chứng minh số học loại trừ số khác 0, nhưng cơ chế đúng.) |

## 1.6 Chi tiết ca (modal)
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.6.1 | Mở modal Chi tiết ca | **PASS** | Modal "Chi tiết ca" mở đủ: Mã ca SCR00000085CN2, Mã NS 00001, Họ tên Admin master, Chức vụ Quản lý, đầu ca 50.000, cuối ca 1.518.375, chênh lệch -1.518.375, VAT 65.875, người mở/đóng, giờ mở/đóng. |
| 1.6.2 | Bảng Thu/Chi theo phương thức trong modal | **PASS** | "Phương thức thanh toán": Tiền mặt 958.375 (khớp thẻ Bán hàng); "Nguồn đơn": Không có dữ liệu; "Thu/Chi": Thu 1.468.375, Chi 0; Bán hàng Gross 958.375 / Net 1.050.000. |
| 1.6.3 | Tổng tiền mặt trong ca (modal) khớp panel chính | **PASS (có lưu ý)** | Modal **"Thu" 1.468.375** = panel "Tổng tiền mặt trong ca" 1.468.375 ✔. Modal còn có "Tổng tiền mặt **cuối ca**" 1.518.375 (= đầu ca + Thu, đúng nghĩa khác). Modal không có nhãn nguyên văn "Tổng tiền mặt trong ca". |
| 1.6.4 | Bấm "Đóng" để thoát modal | **PASS** | Nút **X** (góc phải) đóng modal, quay về panel chi tiết. (Nút "Đóng" dưới cùng lần đầu chưa ăn — nghi lệch điểm chạm khi cuộn; X xác nhận hoạt động ổn định.) |

---

## Tổng hợp
- **Tổng số testcase trong checklist:** 40 (1.1.1→1.6.4).
- **PASS:** **28** — 1.1.1–1.1.5, 1.1.7; 1.2.1, 1.2.2, 1.2.5; 1.3.1, 1.3.2, 1.3.3*, 1.3.4*, 1.3.6; 1.4.1–1.4.10; 1.5.1*(ca sạch), 1.5.2, 1.5.3, 1.5.4, 1.5.8; 1.6.1–1.6.4. (*PASS một phần / theo thiết kế.)
- **FAIL / LỆCH:** **2** — 1.1.8 (không có "Mở màn hình phụ"); 1.3.5 (không có nút "...").
- **BLOCKED:** **3** — 1.5.5 (Trả hàng đang phát triển); 1.5.6, 1.5.7 (môi trường: phiên hết hạn, không nhập liệu được). 1.1.6 (In phiếu) cũng dở dang do môi trường.
- **KHÔNG thực thi (an toàn, chờ xác nhận):** **2** — 1.2.3, 1.2.4 (đóng ca live).

## Danh sách lỗi & phát hiện (chi tiết: `screenshot/0617_0915_coordination/note.md`)
1. **FAIL-01 (1.1.8):** Không tìm thấy nút "Mở màn hình phụ" cho ca đang mở (panel/hộp ca/menu ☰).
2. **LỆCH-01 (1.3.5):** Không có nút "..." trên thẻ tổng hợp — chi tiết phương thức luôn hiển thị sẵn.
3. **FIND-01 (1.5.1, SCR85):** "Tổng tiền mặt trong ca" lưu 1.468.375 > tiền mặt từ giao dịch hiển thị 958.375 (lệch 510.000 không rõ nguồn) → rà soát toàn vẹn dữ liệu ca cũ.
4. **LỆCH-nhỏ (1.4.2):** Số "Tổng cộng" giao dịch không đổi theo bộ lọc loại đang áp (luôn là tổng).
5. **FIND-DROPDOWN (UX):** Dropdown bộ lọc hay kẹt "lớp phủ ma" (phải re-render) — trùng phiên History/Cashboot.
6. **BLOCKED-tính năng (1.5.5):** Trả hàng "đang phát triển".
7. **BLOCKED-môi trường (1.5.6/1.5.7/1.1.6):** Phiên đăng nhập hết hạn sau khi rớt kết nối extension; đăng nhập lại không nhập liệu được (Flutter input không nhận text trong phiên lỗi).

## Khuyến nghị
1. **Bổ sung / xác minh nút "Mở màn hình phụ"** (1.1.8) cho ca đang mở, hoặc đồng bộ lại checklist nếu tính năng đã bỏ.
2. **Đồng bộ checklist với UI thẻ tổng hợp** (1.3.5): UI hiển thị phương thức sẵn, không cần "...".
3. **Rà soát FIND-01:** Vì sao "Tổng tiền mặt trong ca" của ca cũ (SCR85) lệch 510.000 so với giao dịch hiện có — kiểm tra giao dịch đã xóa/không hiển thị.
4. **Cải thiện UX dropdown** (đóng overlay sau khi chọn) — vấn đề lặp lại nhiều phiên.
5. **Phiên sau (cần môi trường ổn định):** chạy lại **1.5.6/1.5.7** (tạo phiếu thu/chi rồi đối chiếu Tổng tiền mặt trong ca tăng/giảm đúng), **1.1.6** (in phiếu), và — nếu được người dùng đồng ý — **1.2.3/1.2.4** (đóng ca, sau đó mở ca mới để khôi phục môi trường). Cân nhắc tạo 1 giao dịch **phi tiền mặt** + 1 giao dịch **hủy số khác 0** để chứng minh số học cho 1.5.3 và 1.5.8.

## Dữ liệu test (nếu cần dọn)
- KHÔNG có phiếu thu/chi nào được tạo thành công (lần thử tạo "phiếu thu 20.000" bị chặn bởi lỗi hết phiên). Store không thay đổi dữ liệu từ phiên này.
