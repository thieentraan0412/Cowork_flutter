# Hướng dẫn kiểm thử — Menu RETURN

## Mục tiêu
Claude thực hiện kiểm thử menu **Return** theo `Checklist/checklist_return.md` và ghi lại kết quả.

> **Lưu ý quan trọng:** Đây là **tài khoản test** trên môi trường thử nghiệm.
> Được phép thực hiện **mọi thao tác** (trả hàng, hoàn tiền…) mà không cần xác nhận lại — cứ làm theo testcase, không bỏ qua bước nào.

## Chuẩn bị
1. Mở trình duyệt **Chrome**.
2. Truy cập https://order-flutter.nasys.vn/#/auth-route
3. Đăng nhập:
   - Store ID: `thientester`
   - Username: `admin`
   - Password: `12345678`
4. Chọn vai trò **Cashier**.
5. Vào menu **Return**.

## Các bước thực hiện
1. Thực hiện **lần lượt từng mục** trong `Checklist/checklist_return.md` theo đúng thứ tự số. **Không dừng lại** cho đến khi chạy hết checklist. **Bỏ qua** các testcase được đánh dấu `TẠM ẨN` (nằm trong HTML comment `<!-- -->`) — không thực hiện và không ghi kết quả.
2. Khi một testcase cần thêm link hoặc cần đổi setting, lấy trong `Link/Link.md`.
3. Với mỗi mục, ghi nhận trạng thái: **PASS / FAIL / BLOCKED / N/A** kèm mô tả ngắn quan sát thực tế.
4. Trọng tâm: tìm đơn cần trả, chọn món/số lượng trả (không vượt số đã mua), tính tiền hoàn (thuế/giảm giá), hình thức hoàn tiền, cập nhật trạng thái đơn gốc và History, ảnh hưởng số dư Cashboot.
5. Lưu ý: thao tác hoàn tiền thực hiện trên đơn test; nếu chỉ có đơn dữ liệu thật và không chắc chắn, ghi **BLOCKED** thay vì thao tác.

## Khi gặp lỗi
- Chụp ảnh màn hình phần bị lỗi.
- Lưu vào `screenshot/<MMDD_HHmm_return>/`.
- Ghi lại các bước tái hiện lỗi để dễ kiểm tra lại.

## Ghi kết quả
- Tạo tệp `result/result_return_<MMDD>_<HHmm>.md`.
- Cấu trúc:
  - Mỗi mục checklist một dòng: **số mục + trạng thái + ghi chú**.
  - Phần cuối: tổng hợp số **PASS / FAIL**, kèm danh sách lỗi và đường dẫn ảnh chụp.
