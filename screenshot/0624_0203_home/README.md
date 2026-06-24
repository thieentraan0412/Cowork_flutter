# Ảnh lỗi — phiên HOME 24/06 02:03

Công cụ điều khiển trình duyệt của phiên **không lưu được ảnh ra đĩa** (đã xác nhận: tham số `save_to_disk` không có tác dụng trong môi trường này) — giống các phiên kiểm thử trước. Vì vậy các lỗi/quan sát được **mô tả chi tiết bằng chữ kèm số liệu** trong tệp kết quả:

→ `result/result_home_0624_0203.md`

## Các điểm lỗi chính (mô tả thay ảnh)

1. **Tổng tiền cập nhật bất đồng bộ (1.20.1 / 1.4.24)** — FAIL
   - Thêm món "Cơm" (SL2, 40.000) vào đơn BAN1: dòng "Thành tiền" hiện 40.000 ngay, nhưng "Tổng tiền hàng" còn hiện 500.000 (cũ) khoảng 3–7s rồi mới nhảy lên 540.000; Phụ thu 50.000→54.000, Thuế 0→2.000, Tổng thanh toán →596.000 cũng trễ tương tự.
   - Bấm +/- số lượng: dòng đổi ngay (40.000↔60.000) nhưng các dòng tổng trễ 1 nhịp.

2. **Renderer đơ/giật buộc reload (1.20.2)** — FAIL
   - Sau ~15 thao tác, click ngừng tác dụng, chụp màn hình time-out (renderer frozen), modal "Tách/Ghép đơn" không đóng được bằng nút Đóng/X/Esc → phải tải lại trang. Xảy ra 2 lần trong phiên.

3. **Tương tác overlay/menu không ổn định**
   - Nút chọn vai trò "Thu ngân", bấm thẻ bàn, dropdown thanh công cụ (số cột/giao diện/chế độ xem), các mục trong menu "..." thường chỉ ăn hover, phải bấm lại nhiều lần.
