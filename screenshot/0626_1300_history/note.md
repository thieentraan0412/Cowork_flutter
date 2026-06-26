# Ghi chú lỗi — HISTORY (Lịch sử) — 26/06/2026 13:00

> Lưu ý: phiên chạy bằng trình duyệt Chrome (Claude in Chrome). Ảnh chụp trong trình duyệt không lưu được ra file .png trong phiên này, nên mỗi lỗi được mô tả kèm **bước tái hiện** đầy đủ để chụp lại thủ công.

## Lỗi 1 — [1.1.6 / 1.1.5] Bàn bị trùng tên trong dropdown "Chọn bàn" + lọc ra rỗng
- **Bước tái hiện:**
  1. Lịch sử → mở dropdown "Tất cả bàn".
  2. Quan sát đầu danh sách: **"ban 1" và "ban 2" mỗi bàn xuất hiện 2 lần** (ban 1, ban 2, ban 1, ban 2, ban kiem tra ten dai, ban_qr, ban3…ban10).
  3. Chọn "ban 2" (mục thứ nhất) → danh sách **rỗng** ("Không tìm thấy đơn hàng nào") dù hôm nay có đơn POS15062090CN2 hiển thị tên bàn "ban 2".
  4. Chọn "ban 2" (mục thứ hai) → vẫn **rỗng**.
  5. Để đối chứng: chọn "ban8" → ra đúng 3 đơn. ⇒ Lọc theo bàn hoạt động cho bàn khác, riêng "ban 2"/"ban 1" trùng tên thì lọc sai.
- **Kết luận:** FAIL — bàn trùng tên, và đơn của "ban 2" không lọc được theo bàn.

## Lỗi 2 — [1.2.19] Tìm kiếm theo TÊN khách hàng không trả kết quả
- **Bước tái hiện:**
  1. Đã có đơn công nợ POS15062092CN2 gán thành viên **tranvana** (SĐT 0321564987).
  2. Ô tìm kiếm gõ `tranvana` → Enter → **rỗng** ("Không tìm thấy đơn hàng nào").
  3. Đối chứng: gõ SĐT `0321564987` → Enter → **ra đúng đơn**. Gõ mã `POS15062092CN2` cũng ra đúng.
- **Kết luận:** FAIL — tìm theo tên khách lỗi (tái hiện lại lỗi 0623). Tìm theo SĐT / mã đơn vẫn OK.

## Lỗi 3 — [1.4.14] Menu "..." của đơn ĐÃ THANH TOÁN thiếu mục "Trả hàng"
- **Bước tái hiện:** Bấm "..." trên đơn POS15062091CN2 (Đã thanh toán) → menu chỉ có **4 mục**: Chi tiết / In lại bill / In lại tem / In lại HĐĐT. **Không có "Trả hàng".**
- **Kết luận:** Khác checklist (0624 ghi 5 mục có "Trả hàng"). Cần xác nhận với dev có phải chủ ý bỏ.

## Lỗi 4 — [1.4.16] Menu "..." của đơn ĐÃ HỦY chỉ có "Chi tiết"
- **Bước tái hiện:** Bấm "..." trên đơn POS15062089CN2 (Đã hủy) → menu chỉ có **1 mục: Chi tiết**.
- **Kết luận:** Khác checklist (0624 ghi 5 mục). Logic có thể hợp lý (đơn hủy không in/trả lại) nhưng lệch tài liệu.

## Lỗi 5 — [1.1.4] Thiếu tab "Đặt online" trong bộ lọc loại đơn
- **Bước tái hiện:** Lịch sử → quan sát các tab phía trên: chỉ có **Tất cả / Tại bàn / Mang về**. Không có tab "Đặt online".
- **Kết luận:** Khác checklist gốc (giống phát hiện 0625).

## Phát hiện MỚI — Tạo công nợ BẮT BUỘC chọn thành viên
- **Bước tái hiện:**
  1. Trang chủ → chọn bàn trống (BAN8) → thêm món (tran chau) → Thanh toán → chọn **Tiền mặt** → nhập tiền khách < tổng (5.000 < 10.500) → Thanh toán.
  2. Hệ thống chặn, hiện cảnh báo: **"Vui lòng chọn thành viên để sử dụng tính năng công nợ."**
  3. Chọn thành viên (tranvana) → nhập lại 5.000 → khi đó mới hiện "Số tiền nợ 5.500đ", "Số ngày 30", "Ngày đáo hạn 26-07-2026" → Thanh toán → Xác nhận → tạo công nợ thành công.
- **Kết luận:** Đơn Khách lẻ KHÔNG tạo được công nợ; phải gán thành viên. Đề xuất bổ sung testcase (đã thêm 1.6.23 vào checklist).

## Ghi chú ổn định (không phải lỗi chức năng)
- Màn Trang chủ / Lịch sử thỉnh thoảng **render trắng/giao diện 2 cột rỗng** khi điều hướng; phải tải lại trang (F5) hoặc đổi "số cột" mới hiển thị đúng. Lỗi gián đoạn (intermittent), giống ghi nhận 0625.
