# Hướng dẫn kiểm thử — Menu COORDINATION

## Mục tiêu
Claude thực hiện kiểm thử menu **Coordination** theo `Checklist/checklist_coordination.md` và ghi kết quả.

## Chuẩn bị
1. Mở https://order-flutter.nasys.vn/#/auth-route
2. Đăng nhập: store id `thientester`, username `admin`, pw `12345678`.
3. Chọn **Casher**.
4. Vào menu **Coordination**.

## Các bước thực hiện
1. Thực hiện từng mục trong `Checklist/checklist_coordination.md` theo thứ tự số.
Trong những testcase nào cần thêm link thì sử dụng trong `Link/link.md`
2. Với mỗi mục ghi: **PASS / FAIL / BLOCKED / N/A** + quan sát thực tế.
3. Trọng tâm: hiển thị hàng chờ chế biến, cập nhật trạng thái món (đang làm/hoàn thành), sắp xếp ưu tiên, cảnh báo món chờ lâu, đồng bộ thời gian thực với Home.
4. Gợi ý: tạo 1 order test ở Home rồi kiểm tra món xuất hiện ở Coordination.
5. Khi gặp lỗi:
   - Chụp ảnh phần bị lỗi → lưu `screenshot/<MMDD_HHmm_coordination>/`.
   - Ghi các bước tái hiện.

## Ghi kết quả
- Tạo tệp `result/result_coordination_<MMDD>_<HHmm>.md`.
- Tổng hợp PASS/FAIL và danh sách lỗi kèm đường dẫn ảnh.
