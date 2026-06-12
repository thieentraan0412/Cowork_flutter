# Hướng dẫn kiểm thử — Menu HISTORY

## Mục tiêu
Claude thực hiện kiểm thử menu **History** theo `Checklist/checklist_history.md` và ghi kết quả.

Sử dụng trình duyệt chorme
Đây là tài khoản test nên được quyền sử dụng mọi thứ
## Chuẩn bị
1. Mở https://order-flutter.nasys.vn/#/auth-route
2. Đăng nhập: store id `thientester`, username `admin`, pw `12345678`.
3. Chọn **Cashier**.
4. Vào menu **History**.

## Các bước thực hiện
1. Thực hiện từng mục trong `Checklist/checklist_history.md` theo thứ tự số.
Trong những testcase nào cần thêm link thì sử dụng trong `Link/link.md`
2. Với mỗi mục ghi: **PASS / FAIL / BLOCKED / N/A** + quan sát thực tế.
3. Trọng tâm: Thực hiện đúng theo các bước đã hướng dẫn trong testcase và ghi nhận lỗi nếu trong trường hợp đang kiểm tra web phát hiện thêm testcase nào thì điền thêm vào file checklist/checklist_history.md.
4. Khi gặp lỗi:
   - Chụp ảnh màn hình phần bị lỗi định dạng đuôi .png hoặc .jpg .
   - Lưu vào `screenshot/<MMDD_HHmm_home>/`.
   - Ghi lại các bước tái hiện lỗi.


## Ghi kết quả
- Tạo tệp `result/result_history_<MMDD>_<HHmm>.md`.
- Tổng hợp PASS/FAIL và danh sách lỗi kèm đường dẫn ảnh.
