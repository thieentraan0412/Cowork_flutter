# Kết quả kiểm thử — ONLINE (Đơn online)

- Menu: online
- Ngày giờ: 24/06 05:55 (UTC)
- Người/agent thực hiện: Claude (Cowork)
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Thu ngân — CN1
- Trình duyệt: Chrome (qua tiện ích điều khiển) — Browser 1
- Thư mục ảnh lỗi: `screenshot/0624_0555_online/`

## Ghi chú chung — PHÁT HIỆN CHÍNH
- Menu **"Đặt online"** (route `pos-booking-route`) hiện màn hình placeholder:
  > **"Tính năng \"booking\" đang phát triển"**
- Nghĩa là **chức năng đơn online CHƯA được triển khai** trên môi trường này. Không có danh sách đơn, không có thao tác nhận/từ chối/cập nhật trạng thái.

---

## Bảng kết quả

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.1.1 | Hiển thị danh sách đơn online | N/A | Trang hiện "Tính năng booking đang phát triển" — chưa có chức năng |
| 1.1.2 | Mỗi đơn có nguồn/mã/thời gian/món/tổng tiền/trạng thái | N/A | Không có đơn để hiển thị |
| 1.2 | Thông báo đơn mới (âm thanh/badge) | N/A | Chưa triển khai |
| 2.1 | Nhận đơn (accept) | N/A | Chưa triển khai |
| 2.2 | Từ chối đơn (reject) kèm lý do | N/A | Chưa triển khai |
| 2.3 | Cập nhật trạng thái chuẩn bị → sẵn sàng → đã giao | N/A | Chưa triển khai |
| 3.1 | Chi tiết món/ghi chú/địa chỉ giao | N/A | Chưa triển khai |
| 3.2 | Thông tin khách hàng | N/A | Chưa triển khai |
| 4.1 | Đơn online hoàn tất xuất hiện trong History | N/A | Chưa triển khai |
| 4.2 | Doanh thu online cộng đúng | N/A | Chưa triển khai |
| 5.1 | Đơn mới hiển thị gần real-time | N/A | Chưa triển khai |
| 5.2 | Không mất đơn khi nhiều đơn | N/A | Chưa triển khai |

---

## Tổng hợp
- **PASS: 0 · FAIL: 0 · BLOCKED: 0 · N/A: 12 (toàn bộ)**
- **Lý do:** Tính năng "Đặt online / booking" **đang phát triển** (placeholder), chưa có chức năng để kiểm thử.

## Kết luận / khuyến nghị
- Trang điều hướng được và hiển thị thông báo "đang phát triển" rõ ràng (không lỗi).
- **Không có gì để kiểm thử** ở menu này cho đến khi tính năng được triển khai. Khi có bản dựng hỗ trợ đơn online, cần kiểm thử lại toàn bộ luồng: hiển thị đơn từ kênh online, thông báo đơn mới, nhận/từ chối, cập nhật trạng thái chế biến–giao, đồng bộ về History và doanh thu.
