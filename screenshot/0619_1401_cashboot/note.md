# Ghi chú lỗi & phát hiện — Menu CASHBOOT (Thu chi) — phiên 0619_1401

> Công cụ tự động hóa **không xuất được ảnh PNG ra đĩa** → mô tả lỗi bằng văn bản kèm dữ liệu đối chứng (như các phiên trước).
> Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin`, vai trò **Thu ngân (Cashier)**, chi nhánh **CN1**, phiên bản **1.0.0+58**, Chrome (Windows) qua extension.
> Bối cảnh đầu phiên (Tháng này, CN1): Tồn đầu kỳ **8.264.976.882**, Tổng thu **778.293.039**, Tổng chi **1.184.745**, Số dư cuối ca **9.042.085.176** (✔ đúng công thức), **227 phiếu**.

---

## BUG-01 (NẶNG) — 1.4.14: Phiếu Số tiền = 0 vẫn tạo thành công
- **Các bước tái hiện:** Thu chi → Thêm → Loại thu chi = "Phiếu chi" → Phân loại "Tiền mặt bảng" → Số tiền nhập `0` → bấm "Tạo mới".
- **Kết quả:** Hệ thống báo **"Tạo thành công"**, sinh phiếu **PT00000036CN2 (Chi 0đ)**, số bản ghi tăng 227 → 228.
- **Mong đợi:** Chặn lưu, yêu cầu số tiền > 0.
- **Ghi chú:** Ô Số tiền có hiển thị viền đỏ "Nhập số tiền" (inline) nhưng KHÔNG chặn được submit. Tổng quỹ không đổi (vì cộng 0) nhưng tạo dữ liệu rác.

## LỆCH-01 — 1.1.10 / 1.5.7–1.5.9: Không có bộ lọc "Loại nguồn"
- Bộ lọc tên **"Loại"** có tồn tại nhưng giá trị là **vai trò nhân sự**: Tất cả / Quản lý / Quầy bếp / Thu ngân / Nhân viên order / Khác.
- KHÔNG phải Bán hàng / Mua hàng / Tự tạo / Trả hàng như checklist mong đợi → không lọc được theo "Loại nguồn".

## LỆCH-02 — 1.4.10: Mô tả giới hạn 50 ký tự (không phải 200)
- Modal Thêm phiếu → ô Mô tả: nhập 62 ký tự → bộ đếm dừng ở **"50/50"**, văn bản bị cắt còn 50 ký tự. Checklist ghi 200.

## LỆCH-03 — 1.4.17: Nhãn luôn "Người nộp / Người nhận"
- Chọn Loại thu chi = "Phiếu chi" → nhãn vẫn là **"Người nộp / Người nhận"** (gộp), không đổi thành riêng "Người nhận".

## LỆCH-04 — 1.7.5: Công nợ bỏ tích cả 2 đối tượng → hiện TẤT CẢ
- Tab Công nợ → bỏ tích cả "Khách hàng" và "Nhà cung cấp" → danh sách hiển thị **TẤT CẢ 51** dòng (coi như không lọc), thay vì rỗng như mong đợi.

## FIND-BALANCE — 1.2 / 1.1.8: "Tồn đầu kỳ" & "Số dư cuối ca" tính lại theo bộ lọc Loại thu chi
- Lọc "Phiếu thu" → Tồn đầu kỳ = 8.287.271.032; lọc "Phiếu chi" → Tồn đầu kỳ = −22.294.150 (khác nhau, và khác mốc Tất cả 8.264.976.882).
- Công thức vẫn đúng trong từng trường hợp, nhưng "tồn đầu kỳ" lẽ ra phải cố định theo kỳ → dễ gây hiểu nhầm số dư.

## Phát hiện nhỏ / UX
- **1.4.2:** Ô Mã phiếu chỉ hiện "Mã tăng tự động", không preview mã thực; mã sinh sau khi Lưu (PC…/PT…).
- **1.4.8:** Ô Số tiền không tự chèn dấu phẩy khi gõ ("10000"); hiển thị đúng "10.000đ" ở danh sách sau khi lưu.
- **1.7.11:** Cột "Mã công nợ" để trống ở mọi dòng (không có dữ liệu để test khớp dương 1.7.7).
- **FIND-DROPDOWN (UX):** Các dropdown bộ lọc/biểu mẫu (Chi nhánh, Loại thu chi, Phân loại, Loại) thường **kẹt "lớp phủ ma"** — phải tải lại trang mới thao tác tiếp được. Ô nhập text (Tên đối tượng, Số tiền) đôi khi nhận input trễ/khó focus khi tự động hóa.
- **Môi trường:** màn hình thỉnh thoảng đơ/loading lâu khi tự động hóa (không phải lỗi sản phẩm).

## Khác biệt so với checklist (đặt tên trường)
- "Loại đối tượng" (checklist) thực tế là **"Loại nhân sự"** (giá trị theo vai trò), không phải Khách hàng/Nhân viên.

## Dữ liệu test đã tạo trong phiên (cần dọn nếu muốn)
- **PT00000036CN2** — Chi **0đ** (sinh ra từ BUG-01)
- **PC00001646CN2** — Thu **10.000** (Mô tả "ABCDEFGHIJ…" 50 ký tự)
- **PT00000037CN2** — Chi **5.000**
- (Đã mở xem đính kèm PC00001541CN2 — file ảnh PNG, không tạo/sửa dữ liệu)
