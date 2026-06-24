# Kết quả kiểm thử — CRM (Quản lý khách hàng)

- Menu: crm — route `#/pos-shell-route/pos-crm-route`
- Ngày giờ: 24/06 05:55 (UTC)
- Người/agent thực hiện: Claude (Cowork)
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Thu ngân — CN1
- Trình duyệt: Chrome (qua tiện ích điều khiển) — Browser 1
- Thư mục ảnh lỗi: `screenshot/0624_0555_crm/`

## Ghi chú chung — PHÁT HIỆN CHÍNH
- Menu **"CRM"** (route `pos-crm-route`) hiển thị placeholder:
  > **"Tính năng \"crm\" đang phát triển"**
- Nghĩa là **chức năng CRM (quản lý khách hàng) trên POS thu ngân CHƯA được triển khai** trên môi trường này.
- *Lưu ý:* Việc gắn khách vào hóa đơn vẫn có ở màn Order (dropdown "Chọn thành viên" — xem Home 1.4.21), nhưng **menu CRM chuyên biệt theo checklist này chưa có chức năng.**

---

## Bảng kết quả

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.1.1 | Danh sách khách: tên, SĐT, điểm, hạng | N/A | Trang hiện "Tính năng crm đang phát triển" |
| 1.2.1 | Tìm kiếm khách theo tên/SĐT | N/A | Chưa triển khai |
| 2.1.1 | Thêm khách, kiểm tra SĐT hợp lệ | N/A | Chưa triển khai |
| 2.1.2 | Không cho trùng SĐT | N/A | Chưa triển khai |
| 2.2 | Sửa thông tin khách | N/A | Chưa triển khai |
| 3.1.1 | Tích điểm sau thanh toán đúng quy tắc | N/A | Chưa triển khai (menu CRM) |
| 3.2.1 | Dùng điểm/voucher, trừ điểm & giảm tiền đúng | N/A | Chưa triển khai |
| 3.3 | Hạng thành viên theo ngưỡng điểm | N/A | Chưa triển khai |
| 4.1 | Xem lịch sử mua hàng của khách | N/A | Chưa triển khai |
| 4.2 | Dữ liệu khớp History | N/A | Chưa triển khai |
| 5.1 / 5.2 | Tìm nhanh / không lộ thông tin khách | N/A | Chưa triển khai |

---

## Tổng hợp
- **PASS: 0 · FAIL: 0 · BLOCKED: 0 · N/A: toàn bộ**
- **Lý do:** Menu "CRM" **đang phát triển** (placeholder), chưa có chức năng để kiểm thử.

## Kết luận / khuyến nghị
- Trang điều hướng được, hiển thị thông báo "đang phát triển" rõ ràng (không lỗi).
- **Không có gì để kiểm thử** ở menu CRM cho đến khi triển khai. Khi có bản dựng, cần kiểm thử: danh sách & tìm kiếm khách, thêm/sửa (ràng buộc SĐT, chống trùng), tích điểm sau thanh toán, dùng điểm/voucher, hạng thành viên, lịch sử mua hàng khớp History.
- Hiện tại nghiệp vụ liên quan khách hàng chỉ thấy ở màn Order (dropdown "Chọn thành viên") — không thuộc phạm vi menu CRM.
