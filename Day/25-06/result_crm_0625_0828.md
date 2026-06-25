# Kết quả kiểm thử — CRM (Quản lý khách hàng)

- Menu: crm — route `#/pos-shell-route/crm-route`
- Ngày giờ: 25/06/2026 08:52 (+07)
- Người/agent thực hiện: Claude (Cowork) — trình duyệt Chrome
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Cashier — Phiên bản 1.0.0+77

## Bảng kết quả
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.1 / 1.1.1 | PASS | "Khách hàng (28)"; thẻ KH hiện: avatar, tên, mã (cus-000XX), SĐT, "Khách vãng lai", hạng (Kim cương/Bạc/Đồng/Sắt), "Điểm: 0" |
| 1.2 / 1.2.1 | PASS | Gõ "vanphong" → lọc còn 1 KH đúng (vanphong cus-00033), tiêu đề đổi "Khách hàng (1)" |
| 2.1 | PASS | "Thêm khách hàng" mở modal: radio Cá nhân/Doanh nghiệp; bắt buộc* Tên KH, Số điện thoại, Nhóm khách hàng; thêm Email, Giới tính, Ngày sinh, CCCD, Địa chỉ |
| 2.1.1 | PASS (có dấu *) | Trường bắt buộc đánh dấu *; chưa submit để xem thông báo chặn |
| 2.1.2 | CHƯA KT | Ràng buộc SĐT hợp lệ / chống trùng SĐT — chưa submit thử (tránh tạo KH rác) |
| 2.2 | CHƯA KT | Sửa KH (qua menu "...") — chưa mở |
| 3.1 / 3.1.1 | CHƯA KT | Tích điểm sau thanh toán — tất cả KH đang "Điểm: 0"; chưa gắn KH vào đơn để kiểm tích điểm |
| 3.2 / 3.2.1 | CHƯA KT | Dùng điểm/voucher khi thanh toán — chưa test |
| 3.3 | PASS (quan sát, lưu ý) | Có hạng thành viên (Kim cương/Bạc/Đồng/Sắt) trên thẻ; tuy nhiên điểm đều = 0 → cần xác nhận quy tắc gán hạng vs điểm |
| 4.1 / 4.2 | CHƯA KT | Lịch sử mua hàng của KH (qua "...") & đối chiếu History — chưa mở |
| 5.1 | PASS | Tìm kiếm phản hồi nhanh trên 28 KH |
| 5.2 | N/A | Rò rỉ dữ liệu giữa tài khoản/cửa hàng — ngoài phạm vi 1 tài khoản |

## Tổng hợp
- PASS: 7 (list, search, add-form, hiệu năng tìm kiếm)
- CHƯA KT: thêm/sửa hoàn tất, tích điểm, dùng điểm/voucher, lịch sử mua hàng
- FAIL: 0 (chức năng)

## Danh sách lỗi / phát hiện
1. **[Quan sát — cần xác nhận] Hạng thành viên có nhưng Điểm = 0** — nhiều KH có badge hạng (Kim cương, Bạc, Đồng, Sắt) nhưng "Điểm: 0". Cần xác nhận quy tắc: hạng gán thủ công hay theo điểm? (Chưa kết luận lỗi.) Mô tả: `screenshot/0625_0828_crm/note.md`.
