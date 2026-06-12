# Hướng dẫn kiểm thử — Menu RETURN

## Mục tiêu
Claude thực hiện kiểm thử menu **Return** theo `Checklist/checklist_return.md` và ghi kết quả.

## Chuẩn bị
1. Mở https://order-flutter.nasys.vn/#/auth-route
2. Đăng nhập: store id `thientester`, username `admin`, pw `12345678`.
3. Chọn **Casher**.
4. Vào menu **Return**.

## Các bước thực hiện
1. Thực hiện từng mục trong `Checklist/checklist_return.md` theo thứ tự số.
Trong những testcase nào cần thêm link thì sử dụng trong `Link/link.md`
2. Với mỗi mục ghi: **PASS / FAIL / BLOCKED / N/A** + quan sát thực tế.
3. Trọng tâm: tìm đơn cần trả, chọn món/số lượng trả (không vượt số đã mua), tính tiền hoàn (thuế/giảm giá), hình thức hoàn tiền, cập nhật trạng thái đơn gốc và History, ảnh hưởng số dư Cashboot.
4. Lưu ý: thao tác hoàn tiền có thể ảnh hưởng dữ liệu thật — chỉ thực hiện trên đơn test hoặc ghi BLOCKED.
5. Khi gặp lỗi:
   - Chụp ảnh phần bị lỗi → lưu `screenshot/<MMDD_HHmm_return>/`.
   - Ghi các bước tái hiện.

## Ghi kết quả
- Tạo tệp `result/result_return_<MMDD>_<HHmm>.md`.
- Tổng hợp PASS/FAIL và danh sách lỗi kèm đường dẫn ảnh.
