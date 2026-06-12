# Hướng dẫn kiểm thử — Menu CRM

## Mục tiêu
Claude thực hiện kiểm thử menu **CRM** theo `Checklist/checklist_crm.md` và ghi kết quả.

## Chuẩn bị
1. Mở https://order-flutter.nasys.vn/#/auth-route
2. Đăng nhập: store id `thientester`, username `admin`, pw `12345678`.
3. Chọn **Casher**.
4. Vào menu **CRM**.

## Các bước thực hiện
1. Thực hiện từng mục trong `Checklist/checklist_crm.md` theo thứ tự số.
Trong những testcase nào cần thêm link thì sử dụng trong `Link/link.md`
2. Với mỗi mục ghi: **PASS / FAIL / BLOCKED / N/A** + quan sát thực tế.
3. Trọng tâm: danh sách & tìm kiếm khách, thêm/sửa khách (ràng buộc SĐT, chống trùng), tích điểm sau thanh toán, dùng điểm/voucher, hạng thành viên, lịch sử mua hàng khớp History.
4. Lưu ý: dùng dữ liệu khách giả; không sửa thông tin khách thật.
5. Khi gặp lỗi:
   - Chụp ảnh phần bị lỗi → lưu `screenshot/<MMDD_HHmm_crm>/`.
   - Ghi các bước tái hiện.

## Ghi kết quả
- Tạo tệp `result/result_crm_<MMDD>_<HHmm>.md`.
- Tổng hợp PASS/FAIL và danh sách lỗi kèm đường dẫn ảnh.
