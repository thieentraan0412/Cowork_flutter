# Hướng dẫn kiểm thử — Menu ONLINE

## Mục tiêu
Claude thực hiện kiểm thử menu **Online** theo `Checklist/checklist_online.md` và ghi lại kết quả.

> **Lưu ý quan trọng:** Đây là **tài khoản test** trên môi trường thử nghiệm.
> Được phép thực hiện **mọi thao tác** (nhận, từ chối, cập nhật trạng thái đơn…) mà không cần xác nhận lại — cứ làm theo testcase, không bỏ qua bước nào.

## Chuẩn bị
1. Mở trình duyệt **Chrome**.
2. Truy cập https://order-flutter.nasys.vn/#/auth-route
3. Đăng nhập:
   - Store ID: `thientester`
   - Username: `admin`
   - Password: `12345678`
4. Chọn vai trò **Cashier**.
5. Vào menu **Online**.

## Các bước thực hiện
1. Thực hiện **lần lượt từng mục** trong `Checklist/checklist_online.md` theo đúng thứ tự số. **Không dừng lại** cho đến khi chạy hết checklist. **Bỏ qua** các testcase được đánh dấu `TẠM ẨN` (nằm trong HTML comment `<!-- -->`) — không thực hiện và không ghi kết quả.
2. Khi một testcase cần thêm link hoặc cần đổi setting, lấy trong `Link/Link.md`.
3. Với mỗi mục, ghi nhận trạng thái: **PASS / FAIL / BLOCKED / N/A** kèm mô tả ngắn quan sát thực tế.
4. Trọng tâm: hiển thị đơn online, thông báo đơn mới, nhận/từ chối đơn, cập nhật trạng thái chế biến - giao, đồng bộ về History và doanh thu.
5. Lưu ý: nếu không có đơn online thật, ghi **BLOCKED** và nêu lý do.

## Khi gặp lỗi
- Chụp ảnh màn hình phần bị lỗi.
- Lưu vào `screenshot/<MMDD_HHmm_online>/`.
- Ghi lại các bước tái hiện lỗi để dễ kiểm tra lại.

## Ghi kết quả
- Tạo tệp `result/result_online_<MMDD>_<HHmm>.md`.
- Cấu trúc:
  - Mỗi mục checklist một dòng: **số mục + trạng thái + ghi chú**.
  - Phần cuối: tổng hợp số **PASS / FAIL**, kèm danh sách lỗi và đường dẫn ảnh chụp.
