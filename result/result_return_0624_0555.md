# Kết quả kiểm thử — RETURN (Trả hàng / Hoàn tiền)

- Menu: return — route `#/pos-shell-route/pos-returns-route`
- Ngày giờ: 24/06 05:55 (UTC)
- Người/agent thực hiện: Claude (Cowork)
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Thu ngân — CN1
- Trình duyệt: Chrome (qua tiện ích điều khiển) — Browser 1
- Thư mục ảnh lỗi: `screenshot/0624_0555_return/`

## Ghi chú chung — PHÁT HIỆN CHÍNH
- Menu **"Trả hàng"** (route `pos-returns-route`) hiển thị placeholder:
  > **"Tính năng \"returns\" đang phát triển"**
- Nghĩa là **chức năng Trả hàng (menu riêng) CHƯA được triển khai** trên môi trường này.
- *Lưu ý:* Thao tác trả hàng vẫn có thể tồn tại ở chỗ khác (menu "..." của đơn ĐÃ THANH TOÁN trong **Lịch sử** có mục "Trả hàng" — xem checklist History 1.4.14; và Điều phối ca có loại "Phiếu trả hàng"). Nhưng **menu "Trả hàng" chuyên biệt theo checklist này thì chưa có chức năng.**

---

## Bảng kết quả

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.1.1 | Tìm đơn cần trả (mã đơn/bàn/thời gian) | N/A | Trang hiện "Tính năng returns đang phát triển" |
| 1.2 | Hiển thị chi tiết đơn được chọn để trả | N/A | Chưa triển khai |
| 2.1 / 2.1.1 | Chọn món / SL trả; không vượt SL đã mua | N/A | Chưa triển khai |
| 2.2 / 2.2.1 | Tính tiền hoàn (thuế/giảm giá) | N/A | Chưa triển khai |
| 2.3 | Hình thức hoàn tiền (TM/CK/thẻ) | N/A | Chưa triển khai |
| 2.4 | Nhập lý do trả hàng | N/A | Chưa triển khai |
| 3.1.1 | Đơn gốc cập nhật trạng thái hoàn | N/A | Chưa triển khai |
| 3.1.2 | Giao dịch hoàn tiền trong History | N/A | Chưa triển khai (menu riêng) |
| 3.2 | Số dư Cashboot giảm đúng nếu hoàn TM | N/A | Chưa triển khai |
| 4.1 / 4.2 | Phân quyền / không trả đơn đã hoàn toàn bộ | N/A | Chưa triển khai |
| 5.1 / 5.2 | Tính toán chính xác / không trùng giao dịch | N/A | Chưa triển khai |

---

## Tổng hợp
- **PASS: 0 · FAIL: 0 · BLOCKED: 0 · N/A: toàn bộ**
- **Lý do:** Menu "Trả hàng" **đang phát triển** (placeholder), chưa có chức năng để kiểm thử.

## Kết luận / khuyến nghị
- Trang điều hướng được, hiển thị thông báo "đang phát triển" rõ ràng (không lỗi).
- **Không có gì để kiểm thử** ở menu Trả hàng chuyên biệt cho đến khi triển khai. Trong thời gian chờ, nếu cần kiểm thử nghiệp vụ trả hàng, dùng đường **Lịch sử → đơn đã thanh toán → "..." → "Trả hàng"** (kiểm thử tay) và đối chiếu phát sinh "Phiếu trả hàng" ở Điều phối ca / Thu chi.
