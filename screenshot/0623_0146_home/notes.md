# Ghi chú ảnh lỗi — HOME 0623_0146

Công cụ chụp màn hình của phiên KHÔNG lưu được ảnh ra đĩa, nên mô tả bằng chữ:

## 1) 1.1.14 — Số liệu tab chưa khớp tổng (CẦN XEM LẠI)
- Trang chủ: "Tất cả (15)" — "Bàn trống (7)" — "Đang sử dụng (7)" — "Chờ xác nhận (0)" — "Chờ thanh toán (0)".
- 7 + 7 + 0 + 0 = 14 ≠ 15. Chênh +1 (nhiều khả năng là thẻ "Bàn mang về").

## 2) Hiểu nhầm dễ gặp về filter "Bàn trống" (KHÔNG phải lỗi)
- Bộ lọc trạng thái là toggle CỘNG DỒN. Nếu để cả "Đang sử dụng" + "Bàn trống" cùng bật, màn hình hiện cả bàn cam (đang dùng) lẫn bàn teal (trống) → dễ tưởng lọc sai.
- Khi chỉ bật riêng "Bàn trống" → chỉ hiện bàn trống. ĐÚNG.

## 3) Modal "Chọn món kèm theo" không tự đóng sau "Thêm vào giỏ hàng" (UX)
- Sau khi bấm "Thêm vào giỏ hàng - 40.000đ", món được thêm vào hóa đơn nhưng modal vẫn mở; phải bấm nút X mới đóng.

## 4) Hiệu năng / async
- Tổng tiền panel hóa đơn cập nhật trễ ~1–4s sau thao tác.
- Cuối phiên trình duyệt đơ/giật nặng (ảnh chụp time-out liên tục).

## Dữ liệu mẫu đã dùng (bàn ban 1 / hóa đơn POS15062077CN2)
- Test điều chuyển: SL1, 500.000, thuế 0%
- Cơm (M, Đường 20%, ghi chú "ít muối @#1"): SL3, 20.000 → 60.000, thuế 5% = 3.000
- Tổng tiền hàng 560.000 + Thuế 3.000 = Tổng thanh toán 563.000 (đúng)
