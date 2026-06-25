# Kết quả kiểm thử — RESERVE (Bàn đặt)

- Menu: reserve (Bàn đặt) — route `#/pos-shell-route/reservation-route`
- Ngày giờ: 25/06/2026 08:45 (+07)
- Người/agent thực hiện: Claude (Cowork) — trình duyệt Chrome
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Cashier — Phiên bản 1.0.0+77

## Bảng kết quả
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.1.1 | PASS | Danh sách đặt bàn theo ngày: tab Mon 22/06…Sun 28/06 + "Hôm nay"; hôm nay "Bàn đặt (0)" → "Chưa có lịch đặt bàn" |
| 1.1.2 | PASS (form) | Trường thông tin có trong form tạo: tên khách, SĐT, số người (lớn/trẻ em), giờ, bàn |
| 2.1 | PASS | "Đặt bàn" mở modal đầy đủ: Khách hàng, Nhân viên đặt bàn, Số lượng người lớn/trẻ em, Giờ bắt đầu, Khu vực bàn, Chọn tên bàn, Tiền đặt cọc + phương thức, Ghi chú (0/200) |
| 2.1.1 | PASS | Bắt buộc: bấm "Đặt bàn" trống → báo đỏ "Vui lòng chọn khách hàng, giờ và bàn" |
| 2.1.2 | CHƯA KT | Ràng buộc SĐT hợp lệ / giờ không ở quá khứ — chưa nhập dữ liệu để kiểm |
| 2.2 / 2.2.1 | CHƯA KT | Tạo thành công & xuất hiện trong danh sách — chưa hoàn tất (cần chọn khách + giờ + bàn) |
| 2.3 | CHƯA KT | Cảnh báo trùng bàn/giờ — chưa tạo được 2 đặt bàn để đối chiếu |
| 3.1 | CHƯA KT | Sửa đặt bàn — chưa có đặt bàn để sửa |
| 3.2 / 3.2.1 / 3.2.2 | CHƯA KT | Hủy đặt bàn & giải phóng bàn — chưa có đặt bàn |
| 4.1 / 4.1.1 | CHƯA KT | Check-in → order — chưa có đặt bàn |
| 5.1 | PASS (một phần) | Thao tác mở/đóng form, validate không gây lỗi |
| 5.2 | CHƯA KT | Cập nhật ngay sau thao tác — chưa tạo dữ liệu |

## Tổng hợp
- PASS: 5 (list, form, validation cốt lõi)
- CHƯA KT: phần còn lại (tạo/sửa/hủy/check-in đầy đủ — cần hoàn tất một đặt bàn)
- FAIL: 0 (chức năng)

## Danh sách lỗi / phát hiện
1. **[Ổn định — liên quan 1.20.2] Trang Bàn đặt render trắng khi vào lần đầu** — vào từ menu, vùng nội dung trắng ~10s; phải tải lại trang mới hiện danh sách + form. Lỗi gián đoạn. Mô tả: `screenshot/0625_0828_reserve/note.md`.
