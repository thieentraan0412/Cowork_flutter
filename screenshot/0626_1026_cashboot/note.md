# Ghi chú phát hiện — CASHBOOT (Thu chi) — 26/06/2026 10:26

> Công cụ chụp màn hình không ghi ảnh PNG ra đĩa trong phiên này → mô tả lỗi bằng văn bản + dữ liệu đối chứng.
> Ứng dụng Flutter (canvas) — DOM/accessibility không trích xuất được, thao tác bằng toạ độ.
> Môi trường: https://order-flutter.nasys.vn — store `thientester` — CN1 — tài khoản **Admin master** — phiên bản **1.0.0+80** — route `pos-cashbook-route`.

---

## ĐÃ FIX (so với các phiên trước) ✅

### BUG-01 (1.19.1 / 1.4.14) — Số tiền = 0 → ĐÃ CHẶN
- Bước: Thêm phiếu → Loại = Phiếu chi → Phân loại auto "Mua tôm hùm bông" → Số tiền = 0 → "Lưu".
- Thực tế phiên này: **bị chặn**, ô Số tiền báo đỏ **"Số tiền phải lớn hơn 0"**, KHÔNG tạo phiếu.
- Trước đây (0616→0623): tạo thành công phiếu PT00000000 0đ. → **Nay đã fix.**

### LỆCH-01 (1.19.2 / 1.4.10) — Giới hạn Mô tả → nay = 200
- Ô Mô tả hiển thị bộ đếm **"x/200"** (gõ 54 ký tự → "54/200", nhận đủ).
- Trước đây giới hạn 50. → Nay khớp spec gốc (200).

---

## CÒN LỖI / CÒN LỆCH ❌

### FIND-BALANCE (1.19.5 / 1.14.4 / 1.11.7) — Tồn đầu kỳ đổi theo bộ lọc, ra số ÂM
- Lọc Loại = "Phiếu chi" (Tuần này, CN1): **Tồn quỹ đầu kỳ = −23.483.895đ**, Số dư cuối ca = −23.533.895đ.
- Lọc Phân loại = "Mua tôm hùm bông": Tồn đầu kỳ = −1.110.000đ, Số dư cuối ca = −1.160.000đ.
- "Đầu kỳ" lẽ ra cố định, không nên tính lại theo bộ lọc loại/phân loại → số âm gây hiểu nhầm số dư. Công thức (đầu + thu − chi) vẫn nhất quán nhưng giá trị hiển thị sai nghĩa nghiệp vụ.

### LỆCH-02 (1.19.3 / 1.4.17) — Nhãn Người nộp/Người nhận không đổi theo Thu/Chi
- Chọn Loại = "Phiếu chi" nhưng nhãn vẫn gộp **"Người nộp / Người nhận"**, không đổi thành "Người nhận".

### LỆCH-03 (1.19.4 / 1.4.5) — "Loại nhân sự" thay vì "Loại đối tượng"
- Trường liên động Người nộp/nhận là **"Loại nhân sự"** (theo vai trò), không phải "Loại đối tượng" (Khách hàng/Nhân viên) như checklist.

### NEW BUG — Ô "Số tiền" nhận cả chữ cái (1.4.8 / 1.12.4)
- Gõ "abc1500000" vào ô Số tiền → hiển thị nguyên **"abc1500000"** (không lọc chữ, không tự định dạng dấu phân cách).
- Kỳ vọng: chỉ nhận số, tự format "1.500.000". → Lỗi lọc ký tự đầu vào.

### Sắp xếp cột không hoạt động (1.10.1 / 1.10.2)
- Bấm tiêu đề cột "Số tiền" và "Thời gian ghi nhận" → thứ tự KHÔNG đổi, không có mũi tên sắp xếp.
- Mặc định mới-nhất-lên-đầu (1.10.3) vẫn đúng.

### Modal không đóng bằng Esc / click ngoài (1.18.3)
- Mở "Thêm phiếu" → nhấn Esc: không đóng. Click vùng tối ngoài modal: chỉ đóng dropdown, modal vẫn mở.
- Chỉ đóng được bằng nút **X** (1.4.12 OK) hoặc "Lưu".

### Mã "toàn số 0" còn trong dữ liệu cũ (1.11.4 / 1.19.6)
- Danh sách vẫn còn **PT00000000CN2 (Chi 0đ)** và **PC00000000CN2 (Thu 10.500đ)** — dữ liệu rác sinh từ BUG-01 các phiên trước. Sinh mã mới hiện đã đúng (PT00000038→PT00000039 tuần tự).

---

## ĐỐI CHỨNG TỐT (không lỗi) ✅
- Công thức quỹ đúng mọi kỳ: Số dư cuối ca = Tồn đầu kỳ + Tổng thu − Tổng chi.
  - Tháng này: 8.264.976.882 + 778.529.039 − 1.239.745 = 9.042.266.176 ✓
  - Tuần này: 9.042.151.076 + 165.100 − 50.000 = 9.042.266.176 ✓
  - Hôm nay: 9.042.245.176 + 21.000 − 0 = 9.042.266.176 ✓
- Tạo/Sửa/Xóa phiếu cập nhật quỹ realtime đúng chênh lệch (tạo Chi 12k → −12k; sửa 12k→20k → −8k; xóa → hoàn về cũ).
- Mã phiếu: PC… = Phiếu thu, PT… = Phiếu chi. Tăng tuần tự độc lập.
- Loại nguồn đúng: Bán hàng / Mua hàng / Trả hàng / Tự tạo. Phiếu Bán hàng tự sinh chỉ-xem (không sửa/xóa).
- Công nợ: chip Tất cả(52)/Gần đến hạn(16)/Quá hạn(22)/Hôm nay(2); lọc Quá hạn → đúng 22 dòng "Đã quá hạn N ngày"; Chưa TT + Đã TT = Tổng tiền (521.000=500.000+21.000…); Mã công nợ có dữ liệu (#52, #51…).
- Xuất Excel: kích hoạt tải file ("Đã xuất file, đang tải xuống trình duyệt").
- Phân quyền: dropdown Chi nhánh = CN1/cn11/cn12; phiếu gắn CN1; Người tạo = Admin master.

## Quirk môi trường (Flutter)
- "Tháng này" tải chậm (~14s) nhưng có dữ liệu (phiên 0626_1017 từng treo > 13s — nay tải được).
- Chuyển tab Thu chi ↔ Công nợ đôi khi chồng layout/cuộn ngang lệch; cuộn lại trái hoặc tải lại trang là hết.
- Một số lần chụp màn hình bị treo renderer trong lúc tải dữ liệu (phải chờ + thử lại).

## Dữ liệu test đã tạo & đã dọn
- PT00000039CN2 — Chi 12.000 → sửa thành 20.000 → **đã xóa** (dọn sạch, không để lại rác).
