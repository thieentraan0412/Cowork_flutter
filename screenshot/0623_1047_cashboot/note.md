# Ghi chú lỗi — CASHBOOT phiên 0623_1047

> Công cụ tự động không xuất được ảnh PNG ra đĩa nên mô tả lỗi bằng văn bản + dữ liệu đối chứng.
> Ứng dụng Flutter (canvas) — không trích được DOM/ảnh từng phần.

## BUG-01 (NẶNG) — 1.4.14: Phiếu Số tiền = 0 vẫn tạo thành công
- Bước tái hiện:
  1. Thu chi → bấm "Thêm".
  2. Loại thu chi = "Phiếu chi" (Phân loại auto "Mua tôm hùm bông").
  3. Số tiền = 0.
  4. Bấm "Tạo mới".
- Kết quả thực tế: hiện popup ✓ "Tạo thành công" → sinh phiếu **PT00000000CN2** Chi **0đ**, lên đầu danh sách. KHÔNG bị chặn.
- Kết quả mong đợi: chặn lưu + báo lỗi "số tiền phải lớn hơn 0".
- Mức độ: NẶNG (dữ liệu rác). Đã tồn tại từ phiên 0616, lặp lại 0619 & 0623 → CHƯA fix.

## LỆCH-01 — 1.4.10: Mô tả giới hạn 50 ký tự (checklist ghi 200)
- Modal "Thêm phiếu" → ô "Mô tả" hiển thị bộ đếm "0/50". Giới hạn thực = 50.

## LỆCH-02 — 1.4.17: Nhãn Người nộp/Người nhận không đổi theo Thu/Chi
- Chọn Loại = "Phiếu chi" nhưng nhãn vẫn là "Người nộp / Người nhận" (gộp), không đổi thành "Người nhận".

## LỆCH-03 — 1.4.5/1.4.15: "Loại nhân sự" thay vì "Loại đối tượng"
- Trường thực tế là "Loại nhân sự" với giá trị theo VAI TRÒ: Quản lý / Quầy bếp / Thu ngân / Nhân viên order / Khác.
- Checklist mong đợi "Loại đối tượng": Khách hàng / Nhân viên.
- Chọn "Thu ngân" → Người nộp auto "casher2", danh sách = nhân sự vai trò đó (đúng cơ chế liên động, chỉ lệch tên/scope).

## FIND-BALANCE — Tồn đầu kỳ tính lại theo bộ lọc Loại thu chi
- Lọc chỉ "Phiếu chi" (Tháng này, CN1): Tồn đầu kỳ hiển thị **−22.294.150đ**, Số dư cuối **−23.483.895đ**.
- "Đầu kỳ" lẽ ra cố định, không nên đổi theo bộ lọc Thu/Chi → dễ gây hiểu nhầm số dư.

## Lỗi nhỏ
- Mã phiếu tự sinh đôi khi ra dạng "PT00000000" / "PC00000000" (toàn số 0) — kiểm tra logic sinh mã.
- Mã phiếu không preview trong modal (chỉ "Mã tăng tự động").
- Ô Số tiền không tự định dạng dấu phẩy khi gõ.

## Cải thiện so với 0619
- Bộ lọc "Loại nguồn" đã đúng: Bán hàng / Mua hàng / Trả hàng / Tự tạo (1.1.10, 1.5.7 PASS).
- Cột "Mã công nợ" (tab Công nợ) đã có dữ liệu (#52, #51…).

## Dữ liệu test đã tạo (để dọn nếu cần)
- PC00001650CN2 — Thu 100.000
- PT00000000CN2 — Chi 0đ (BUG-01)
- PT00000038CN2 — Chi 50.000
