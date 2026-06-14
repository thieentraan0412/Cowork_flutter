# Kết quả kiểm thử — HOME (mẫu)

- Menu: home
- Ngày giờ: 06/25 17:33
- Người/agent thực hiện: Claude
- Môi trường: https://table1.klkim.com — store `thientester` — vai trò Cashier

> ⚠️ Đây là TỆP MẪU minh họa định dạng. Thay nội dung bằng kết quả thật khi chạy `run/run_home.md`.

## Bảng kết quả
| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.1 | Trang Home tải thành công | PASS | Tải < 2s |
| 1.1.1 | Không lỗi 4xx/5xx | PASS | |
| 1.2 | Đủ 8 menu | PASS | |
| 2.1 | Chọn bàn trống mở order | PASS | |
| 2.3 | Chuyển bàn | FAIL | Bàn cũ không về trạng thái trống — xem ảnh |
| 3.1.1 | Tính thành tiền | PASS | |
| 4.1.1 | Tính tổng tiền/thuế/giảm giá | PASS | |

## Tổng hợp
- PASS: 6
- FAIL: 1
- BLOCKED: 0
- N/A: 0

## Danh sách lỗi
1. **[2.3] Chuyển bàn — bàn cũ không giải phóng**
   - Bước tái hiện: chọn bàn A có order → chuyển sang bàn B → quay lại layout.
   - Kỳ vọng: bàn A trở về trạng thái trống.
   - Thực tế: bàn A vẫn hiển thị "đang sử dụng".
   - Ảnh: `screenshot/0625_1733_home/error_move_table.png`
