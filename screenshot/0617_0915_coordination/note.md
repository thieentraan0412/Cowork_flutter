# Ghi chú lỗi/quan sát — COORDINATION (Điều phối ca) — phiên 0617_0915

> Công cụ tự động hóa **không xuất được ảnh PNG ra đĩa** (giống các phiên trước) → mô tả lỗi bằng văn bản + dữ liệu đối chứng + các bước tái hiện.
> Môi trường: Chrome (extension), https://order-flutter.nasys.vn, store `thientester`, vai trò Thu ngân, chi nhánh CN1, app **1.0.0+55**, 17/06/2026.

---

## FAIL-01 (1.1.8) — Không tìm thấy nút "Mở màn hình phụ"
**Mong đợi:** Ca đang mở có nút "Mở màn hình phụ" → mở màn hình phụ.
**Thực tế:** Không thấy nút này ở 3 nơi đã kiểm:
- Panel chi tiết ca đang mở (chỉ có "Đóng ca" + "Đóng và in phiếu").
- Hộp "CA HIỆN TẠI" (chỉ thông tin ca, không nút).
- Menu ☰ góc phải (chỉ: CN1, Thu ngân, Bật âm thanh, Tải lại cấu hình, Ngôn ngữ).
**Ảnh hưởng:** Không thực hiện được thao tác mở màn hình phụ từ Điều phối ca.

---

## LỆCH-01 (1.3.5) — Không có nút "..." trên thẻ tổng hợp
**Mong đợi:** Bấm "..." trên thẻ → hiện chi tiết phương thức (tiền mặt/CK/quẹt thẻ/QR/khác).
**Thực tế:** Không có nút "...". Mỗi thẻ (Bán hàng/Trả hàng/Phiếu thu/Phiếu chi) **luôn hiển thị sẵn** dòng Tiền mặt / Chuyển khoản / Quẹt thẻ / QR tự động + Tổng tiền.
**Đánh giá:** Vẫn đạt mục tiêu "xem chi tiết phương thức" nhưng khác cách thao tác checklist ⇒ nên đồng bộ checklist với UI.

---

## FIND-01 (1.5.1) — Lệch "Tổng tiền mặt trong ca" ở ca cũ SCR00000085CN2
**Quan sát:**
- Thẻ Bán hàng (tiền mặt) = **958.375**; Trả hàng/Phiếu thu(thủ công)/Phiếu chi = 0.
- Giao dịch hiển thị (Tổng 4, 2 hủy): PC00001514 (Phiếu thu 958.375, TM) + POS00002219 (Phiếu bán hàng 958.375, TM) + POS00002221/POS00002218 (0đ, Đã hủy). PC là phiếu thu **tự sinh** của chính đơn bán → cùng dòng tiền.
- Nhưng **"Tổng tiền mặt trong ca" = 1.468.375** (modal: Thu 1.468.375; cuối ca 1.518.375 = 50.000 đầu ca + 1.468.375).
- **Lệch 1.468.375 − 958.375 = 510.000** không giải thích được bằng 4 giao dịch đang hiển thị.
**Giả thuyết:** Có giao dịch tiền mặt **đã xóa/không hiển thị** từng được cộng vào tổng lưu trữ, hoặc tổng ca không tính lại sau khi xóa giao dịch.
**Đối chứng ngược (ca sạch SCR00000097CN2):** 3 bán hàng (1.169.500) + 3 phiếu thu tự sinh (1.169.500) → Tổng = **1.169.500** (KHÔNG cộng đôi), đầu ca 0 ⇒ **công thức đúng** trên dữ liệu sạch.
**Đề nghị:** Rà soát toàn vẹn dữ liệu ca lịch sử (đặc biệt giao dịch đã xóa).

---

## QUAN SÁT/UX
- **FIND-DROPDOWN:** Dropdown bộ lọc (loại giao dịch, nhân viên, thời gian) thường render trễ/kẹt "lớp phủ ma" — phải chờ 1–2s hoặc re-render. Trùng ghi nhận phiên History/Cashboot.
- **1.4.2 — "Tổng cộng" không theo bộ lọc:** Khi lọc 1 loại (vd Phiếu bán hàng → 3 dòng), header vẫn ghi "Tổng cộng: 6" (tổng mọi giao dịch).
- **1.6.4 — Nút "Đóng" dưới modal:** Lần đầu bấm không đóng (nghi lệch điểm chạm sau khi cuộn nội dung modal); nút **X** góc phải đóng ổn định.
- **1.1.2 — Nhãn trạng thái:** Ca đang mở dùng nhãn **"Đang hoạt động"** (không phải "Đang mở" như checklist).

## BLOCKED
- **1.5.5 — Trả hàng:** tính năng "returns đang phát triển" (theo phiên Cashboot) → không tạo phiếu trả hàng để kiểm giảm tổng.
- **1.5.6 / 1.5.7 — Tạo phiếu thu/chi (môi trường):** Đã thao tác Thu chi → Thêm phiếu → Phiếu thu/Tiền mặt/20.000 → bấm "Tạo mới" thì hiện toast **"Thất bại — Phiên đăng nhập đã hết hạn. Vui lòng đăng nhập lại."** (xảy ra ngay sau một lần rớt kết nối extension). Đăng nhập lại **thất bại**: ô "Mật khẩu" (và mọi ô nhập Flutter) **không nhận text** qua mọi cách (gõ phím CDP, key đơn, JS InputEvent) — form báo "Mật khẩu phải có ít nhất 6 ký tự" dù đã thử nhập. ⇒ Lỗi **môi trường tự động hóa**, không phải lỗi sản phẩm. Trùng FIND-07 phiên History ("phiên đăng nhập hết hạn + kết nối rớt nhiều lần").
- **1.1.6 — In phiếu:** dở dang do cùng lý do môi trường (nút có sẵn, chưa kích hoạt được lệnh in).

## KHÔNG THỰC THI (an toàn — chờ người dùng xác nhận)
- **1.2.3 / 1.2.4 — Đóng ca / Đóng và in phiếu:** Nút có sẵn & enabled ở ca đang mở SCR00000097CN2. KHÔNG bấm để tránh đóng ca thu ngân đang chạy trên store test dùng chung (đóng ca là thao tác làm thay đổi trạng thái toàn cục; cần xác nhận, sau đó nên mở ca mới để khôi phục).

## GHI CHÚ KỸ THUẬT (tự động hóa Flutter web)
- Click: phải **dispatch pointer-event bằng JS** tại tọa độ trang (CDP click thường không kích hoạt GestureDetector của Flutter).
- Nhập text: `computer click + type` hoạt động khi renderer "khỏe" (đã nhập được "20000" vào ô Số tiền); **không** hoạt động sau khi rớt kết nối/hết phiên.
- Màn hình thỉnh thoảng đơ ("renderer frozen") khi chụp ảnh ngay sau thao tác → cần chờ.

## DỮ LIỆU TEST ĐÃ TẠO
- **KHÔNG có** — lần thử tạo "phiếu thu 20.000" bị chặn bởi lỗi hết phiên. Store không bị thay đổi dữ liệu trong phiên này.
