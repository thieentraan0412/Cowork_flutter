# Hướng dẫn kiểm thử — Menu RESERVE

## Mục tiêu
Claude thực hiện kiểm thử menu **Reserve** theo `Checklist/checklist_reserve.md` và ghi lại kết quả.

> **Lưu ý quan trọng:** Đây là **tài khoản test** trên môi trường thử nghiệm.
> Được phép thực hiện **mọi thao tác** (tạo, sửa, huỷ đặt bàn, check-in…) mà không cần xác nhận lại — cứ làm theo testcase, không bỏ qua bước nào.

## Chuẩn bị
1. Mở trình duyệt **Chrome**.
2. Truy cập https://order-flutter.nasys.vn/#/auth-route
3. Đăng nhập:
   - Store ID: `thientester`
   - Username: `admin`
   - Password: `12345678`
4. Chọn vai trò **Cashier**.
5. Vào menu **Reserve**.

## Các bước thực hiện
1. Thực hiện **lần lượt từng mục** trong `Checklist/checklist_reserve.md` theo đúng thứ tự số. **Không dừng lại** cho đến khi chạy hết checklist. **Bỏ qua** các testcase được đánh dấu `TẠM ẨN` (nằm trong HTML comment `<!-- -->`) — không thực hiện và không ghi kết quả.
2. Khi một testcase cần thêm link hoặc cần đổi setting, lấy trong `Link/Link.md`.
3. Với mỗi mục, ghi nhận trạng thái: **PASS / FAIL / BLOCKED / N/A** kèm mô tả ngắn quan sát thực tế.
4. Trọng tâm: tạo đặt bàn mới (ràng buộc dữ liệu), sửa/hủy đặt bàn, cảnh báo trùng bàn/trùng giờ, check-in chuyển đặt bàn thành order.
5. Lưu ý: dùng dữ liệu thử nghiệm (tên/SĐT giả) và dọn dẹp đặt bàn test sau khi xong nếu có thể.

## Khi gặp lỗi
- Chụp ảnh màn hình phần bị lỗi.
- Lưu vào `screenshot/<MMDD_HHmm_reserve>/`.
- Ghi lại các bước tái hiện lỗi để dễ kiểm tra lại.

## Ghi kết quả
- Tạo tệp `result/result_reserve_<MMDD>_<HHmm>.md`.
- Cấu trúc:
  - Mỗi mục checklist một dòng: **số mục + trạng thái + ghi chú**.
  - Phần cuối: tổng hợp số **PASS / FAIL**, kèm danh sách lỗi và đường dẫn ảnh chụp.
