# Hướng dẫn kiểm thử — Menu HOME

## Mục tiêu
Claude thực hiện kiểm thử menu **Home** theo `Checklist/checklist_home.md` và ghi lại kết quả.

> **Lưu ý quan trọng:** Đây là **tài khoản test** trên môi trường thử nghiệm.
> Được phép thực hiện **mọi thao tác** (thêm, sửa, xoá, thanh toán, huỷ, đổi cấu hình…) mà không cần xác nhận lại — cứ làm theo testcase, không bỏ qua bước nào.

## Chuẩn bị
1. Mở trình duyệt **Chrome**.
2. Truy cập https://order-flutter.nasys.vn/#/auth-route
3. Đăng nhập:
   - Store ID: `thientester`
   - Username: `admin`
   - Password: `12345678`
4. Chọn vai trò **Cashier**.
5. Vào menu **Trang chủ**.

## Các bước thực hiện
1. Thực hiện **lần lượt từng mục** trong `Checklist/checklist_home.md` theo đúng thứ tự số (1 → 1.1 → 1.1.1). **Không dừng lại** cho đến khi chạy hết checklist. **Bỏ qua** các testcase được đánh dấu `TẠM ẨN` (nằm trong HTML comment `<!-- -->`) — không thực hiện và không ghi kết quả.
2. Khi một testcase cần thêm link hoặc cần đổi setting, lấy trong `Link/Link.md`.
3. Với mỗi mục, ghi nhận trạng thái: **PASS / FAIL / BLOCKED / N/A** kèm mô tả ngắn quan sát thực tế.
4. Trọng tâm: làm **đúng các bước** mô tả trong testcase và ghi nhận chính xác lỗi phát sinh.
5. Sau khi chạy xong **tất cả** testcase: **cập nhật lại mục "Ghi chú UI thực tế"** ở đầu `Checklist/checklist_home.md` cho khớp giao diện/thuật ngữ/quirk quan sát được trong phiên (bổ sung điểm mới, sửa điểm đã thay đổi). **Nếu UI có thay đổi** so với "Ghi chú UI thực tế" trước đó, ghi rõ **từng chỗ thay đổi** vào **chính file result đã tạo ở phần "Ghi kết quả"** (`result/result_home_<MMDD>_<HHmm>.md`) — thêm mục **"Thay đổi UI"**.

## Khi gặp lỗi
- Chụp ảnh màn hình phần bị lỗi.
- Lưu vào `screenshot/<MMDD_HHmm_home>/`.
- Ghi lại các bước tái hiện lỗi để dễ kiểm tra lại.

## Ghi kết quả
- Tạo tệp `result/result_home_<MMDD>_<HHmm>.md`.
- Cấu trúc:
  - Mỗi mục checklist một dòng: **số mục + trạng thái + ghi chú**.
  - Phần cuối: tổng hợp số **PASS / FAIL**, kèm danh sách lỗi và đường dẫn ảnh chụp.
