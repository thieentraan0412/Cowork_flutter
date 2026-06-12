# Hướng dẫn kiểm thử — Menu ONLINE

## Mục tiêu
Claude thực hiện kiểm thử menu **Online** theo `Checklist/checklist_online.md` và ghi kết quả.

## Chuẩn bị
1. Mở https://order-flutter.nasys.vn/#/auth-route
2. Đăng nhập: store id `thientester`, username `admin`, pw `12345678`.
3. Chọn **Casher**.
4. Vào menu **Online**.

## Các bước thực hiện
1. Thực hiện từng mục trong `Checklist/checklist_online.md` theo thứ tự số.
Trong những testcase nào cần thêm link thì sử dụng trong `Link/link.md`
2. Với mỗi mục ghi: **PASS / FAIL / BLOCKED / N/A** + quan sát thực tế.
3. Trọng tâm: hiển thị đơn online, thông báo đơn mới, nhận/từ chối đơn, cập nhật trạng thái chế biến-giao, đồng bộ về History và doanh thu.
4. Lưu ý: nếu không có đơn online thật, ghi BLOCKED và nêu lý do.
5. Khi gặp lỗi:
   - Chụp ảnh phần bị lỗi → lưu `screenshot/<MMDD_HHmm_online>/`.
   - Ghi các bước tái hiện.

## Ghi kết quả
- Tạo tệp `result/result_online_<MMDD>_<HHmm>.md`.
- Tổng hợp PASS/FAIL và danh sách lỗi kèm đường dẫn ảnh.
