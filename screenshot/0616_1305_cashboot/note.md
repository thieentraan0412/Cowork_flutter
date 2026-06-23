# Ghi chú lỗi/quan sát — CASHBOOT (Thu chi) — phiên 0616_1305

> Công cụ tự động hóa **không xuất được ảnh PNG ra đĩa** (giống các phiên trước) → mô tả lỗi bằng văn bản + dữ liệu đối chứng + các bước tái hiện.
> Môi trường: Chrome (extension), https://order-flutter.nasys.vn, store `thientester`, vai trò Thu ngân, chi nhánh CN1, app 1.0.0+54, 16/06/2026.

---

## BUG-01 (NẶNG) — Phiếu Số tiền = 0 vẫn tạo thành công (testcase 1.4.14)
**Mong đợi:** Nhập Số tiền = 0 → hệ thống chặn, báo "số tiền phải lớn hơn 0".
**Thực tế:** Tạo phiếu Chi với Số tiền = 0 → **TẠO THÀNH CÔNG**, sinh phiếu `PT00000034CN2` (Chi, 0đ), Tổng bản ghi 204→205.
**Tái hiện:**
1. Thu chi → "Thêm".
2. Loại thu chi = "Phiếu chi"; Số tiền = 0; (Phân loại tự điền "Tiền mặt bảng").
3. Bấm "Tạo mới".
4. → Popup "Tạo thành công", phiếu 0đ xuất hiện đầu danh sách.
**Ảnh hưởng:** cho phép dữ liệu rác (phiếu 0đ) vào sổ quỹ.

---

## LỆCH CHECKLIST/UI (không hẳn bug nhưng khác mô tả)
- **1.1.10 / 1.5.7–1.5.9 — Không có bộ lọc "Loại nguồn":** Checklist cần lọc theo Bán hàng/Mua hàng/Tự tạo/Trả hàng. Thực tế bộ lọc tên "Loại" chỉ có giá trị **vai trò**: Quản lý / Quầy bếp / Thu ngân / Nhân viên order / Khác. ⇒ Không lọc được theo nguồn phát sinh.
- **1.4.10 — Mô tả giới hạn 50 ký tự (không phải 200):** Bộ đếm hiển thị "23/50". Checklist ghi 200.
- **1.4.17 — Label không đổi theo Thu/Chi:** Luôn hiển thị "Người nộp / Người nhận" (gộp) cho cả Phiếu thu lẫn Phiếu chi. Checklist mong đổi "Người nộp" ↔ "Người nhận".
- **1.7.5 — Bỏ tích cả 2 đối tượng → hiện TẤT CẢ (50):** Checklist mong danh sách rỗng. Thực tế coi "không chọn = chọn tất cả".

## QUAN SÁT/UX
- **FIND-BALANCE:** "Tồn quỹ đầu kỳ" và "Số dư cuối ca" **tính lại theo bộ lọc Loại thu chi**. Khi lọc chỉ "Phiếu thu": đầu kỳ 8.287.271.032, cuối kỳ 9.055.051.941 (bỏ qua chi); chỉ "Phiếu chi": đầu kỳ -22.294.150. "Đầu kỳ" lẽ ra là điểm cố định ⇒ dễ gây hiểu nhầm số dư khi đang lọc.
- **FIND-DROPDOWN:** Các dropdown bộ lọc/biểu mẫu hay kẹt "lớp phủ ma" — click option không ăn (dropdown giữ mở), keyboard/double-click/type-ahead đều vô hiệu; **tải lại trang hoặc mở tab mới** thì hết kẹt, click 1 lần ăn bình thường. (Khớp ghi nhận phiên History.)
- **1.4.2 — Mã phiếu không preview:** Ô Mã phiếu chỉ hiện chữ "Mã tăng tự động", không hiện mã thực; mã chỉ sinh sau khi Lưu (vd PC00001624, PT00000035 — tăng dần đúng theo 2 chuỗi PC/PT).
- **1.4.8 — Số tiền không tự định dạng khi gõ:** Ô hiển thị "10000" (không có dấu phẩy lúc nhập); lưu & danh sách hiển thị đúng "10.000đ".
- **1.3.3 — Ngày tạo dạng raw:** Modal chi tiết phiếu hiển thị "2026-06-11T08:28:00.000000Z" (chưa format).
- **1.1.1 — Ô Mã phiếu lọc live:** không cần Enter; nhấn Enter gây nhảy trang.
- **1.7.11 — Cột "Mã công nợ" để trống** ở mọi dòng (chỉ có "Mã đơn").

## BLOCKED (không kiểm được)
- **1.5.6 / 1.5.11 — Trả hàng:** Tab "Trả hàng" hiển thị **"Tính năng 'returns' đang phát triển"** → không thực hiện được phiếu trả hàng.
- **1.3.4 / 1.4.9 / 1.4.18 — Đính kèm tệp:** không upload được tệp qua tự động hóa (không có tệp trên máy người dùng để chọn).
- **1.6.2 — Nội dung file Excel:** không mở/đối chiếu được file tải về (file ở máy người dùng).

## DỮ LIỆU TEST ĐÃ TẠO (để dọn nếu cần)
- PC00001624CN2 — Thu 10.000 (Mô tả "TEST QA cashboot 1.4.11")
- PT00000034CN2 — Chi 0đ (từ BUG-01)
- PT00000035CN2 — Chi 5.000 (test 1.4.20)
- Đơn bán PO015062036CN2 (ban1, tran chau, 10.500 Tiền mặt) → sinh phiếu thu PC00001625CN2 10.500
</content>
</invoke>
