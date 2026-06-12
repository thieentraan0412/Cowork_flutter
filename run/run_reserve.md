# Hướng dẫn kiểm thử — Menu RESERVE

## Mục tiêu
Claude thực hiện kiểm thử menu **Reserve** theo `Checklist/checklist_reserve.md` và ghi kết quả.

## Chuẩn bị
1. Mở https://order-flutter.nasys.vn/#/auth-route
2. Đăng nhập: store id `thientester`, username `admin`, pw `12345678`.
3. Chọn **Casher**.
4. Vào menu **Reserve**.

## Các bước thực hiện
1. Thực hiện từng mục trong `Checklist/checklist_reserve.md` theo thứ tự số.
Trong những testcase nào cần thêm link thì sử dụng trong `Link/link.md`
2. Với mỗi mục ghi: **PASS / FAIL / BLOCKED / N/A** + quan sát thực tế.
3. Trọng tâm: tạo đặt bàn mới (ràng buộc dữ liệu), sửa/hủy đặt bàn, cảnh báo trùng bàn/trùng giờ, check-in chuyển đặt bàn thành order.
4. Lưu ý: dùng dữ liệu thử nghiệm (tên/SĐT giả) và dọn dẹp đặt bàn test sau khi xong nếu có thể.
5. Khi gặp lỗi:
   - Chụp ảnh phần bị lỗi → lưu `screenshot/<MMDD_HHmm_reserve>/`.
   - Ghi các bước tái hiện.

## Ghi kết quả
- Tạo tệp `result/result_reserve_<MMDD>_<HHmm>.md`.
- Tổng hợp PASS/FAIL và danh sách lỗi kèm đường dẫn ảnh.
