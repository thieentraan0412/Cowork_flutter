Tiến hành công việc kiểm thử như sau.

Truy cập vào https://order-flutter.nasys.vn/#/auth-route và nhập:
store id: thientester
username: admin
pw: 12345678
Sau khi nhập xong, chọn casher.

Danh sách các menu cần kiểm thử:
home, history, reserve, online, coordination, cashboot, return, crm

1. Tập hợp tất cả các tệp liên quan đến kiểm thử vào thư mục test_order/.

2. Trong thư mục test_order/Checklist/, tập hợp tệp checklist cho từng menu (checklist_menu1.md, checklist_menu2.md). Viết và lưu một checklist cơ bản.
Đánh số cho mọi mục checklist theo cách sau:
1.
1.1
1.1.1

3. Trong thư mục test_order/run/, lưu mỗi menu một tệp chứa nội dung hướng dẫn Claude thực hiện kiểm thử. (run_menu1.md, run_menu2.md)

4. Trong thư mục test_order/result/, lưu kết quả kiểm thử thành tệp có tên menu+ngày+giờ.md. (result_home_0625_1733.md)

5. Trong thư mục test_order/screenshot/ngày_giờ_tênmenu/, chụp và lưu ảnh màn hình của những phần bị lỗi.

Hãy tạo các tệp .md theo hướng dẫn ở trên.
