# Hướng dẫn kiểm thử — Menu CASHBOOT

## Mục tiêu
Claude thực hiện kiểm thử menu **Cashboot** theo `Checklist/checklist_cashboot.md` và ghi kết quả.

## Chuẩn bị
1. Mở https://order-flutter.nasys.vn/#/auth-route
2. Đăng nhập: store id `thientester`, username `admin`, pw `12345678`.
3. Chọn **Casher**.
4. Vào menu **Cashboot**.

## Các bước thực hiện
1. Thực hiện từng mục trong `Checklist/checklist_cashboot.md` theo thứ tự số.
Trong những testcase nào cần thêm link thì sử dụng trong `Link/link.md`
2. Với mỗi mục ghi: **PASS / FAIL / BLOCKED / N/A** + quan sát thực tế.
3. Trọng tâm: mở ca/đóng ca, số dư đầu-cuối ca, ghi thu (paid-in)/chi (paid-out), tính chênh lệch, báo cáo khớp doanh thu tiền mặt.
4. Lưu ý: cẩn trọng với thao tác đóng ca thật — chỉ thực hiện nếu được phép, nếu không thì ghi BLOCKED.
5. Khi gặp lỗi:
   - Chụp ảnh phần bị lỗi → lưu `screenshot/<MMDD_HHmm_cashboot>/`.
   - Ghi các bước tái hiện.

## Ghi kết quả
- Tạo tệp `result/result_cashboot_<MMDD>_<HHmm>.md`.
- Tổng hợp PASS/FAIL và danh sách lỗi kèm đường dẫn ảnh.
