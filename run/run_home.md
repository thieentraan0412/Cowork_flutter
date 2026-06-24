# Hướng dẫn kiểm thử — Menu HOME

## Mục tiêu
Claude thực hiện kiểm thử menu **Home** theo `Checklist/checklist_home.md` và ghi kết quả.

Sử dụng trình duyệt chorme
Đây là tài khoản test nên được quyền sử dụng mọi thứ

## Chuẩn bị
1. Mở https://order-flutter.nasys.vn/#/auth-route
2. Đăng nhập: store id `thientester`, username `admin`, pw `12345678`.
3. Chọn **Casher**.
4. Vào menu **Home**.

## Các bước thực hiện
Trong những testcase nào cần thêm link thì sử dụng trong `Link/link.md`

1. Lần lượt thực hiện từng mục trong `Checklist/checklist_home.md` theo đúng thứ tự số (1 → 1.1 → 1.1.1), không dừng lại cho đến khi chạy xong,hãy sử file link.md nếu cần thêm các setting
2. Với mỗi mục, ghi nhận: **PASS / FAIL / BLOCKED / N/A** và mô tả ngắn quan sát thực tế.
3. Trọng tâm: Thực hiện đúng theo các bước đã hướng dẫn trong testcase và ghi nhận lỗi.
4. Khi gặp lỗi:
   - Chụp ảnh màn hình phần bị lỗi.
   - Lưu vào `screenshot/<MMDD_HHmm_home>/`.
   - Ghi lại các bước tái hiện lỗi.
   
## Ghi kết quả
- Tạo tệp `result/result_home_<MMDD>_<HHmm>.md`.
- Cấu trúc: mỗi mục checklist một dòng + trạng thái + ghi chú, phần cuối tổng hợp số PASS/FAIL và danh sách lỗi kèm đường dẫn ảnh.

