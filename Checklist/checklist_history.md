# Checklist — Menu HISTORY

1. Lịch sử
1.1 Bộ lọc loại đơn

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.1.1 | ☐ | Lọc tab "Tất cả" | 1. Đăng nhập, truy cập link cashier history 2. Quan sát các tab lọc loại đơn phía trên danh sách 3. Bấm tab "Tất cả" 4. Quan sát danh sách đơn | Hiển thị tất cả đơn không phân biệt loại |
| 1.1.2 | ☐ | Lọc tab "Tại bàn" | 1. Vào trang lịch sử 2. Bấm tab "Tại bàn" 3. Quan sát từng đơn trong danh sách | Chỉ hiện các đơn loại tại bàn |
| 1.1.3 | ☐ | Lọc tab "Mang về" | 1. Vào trang lịch sử 2. Bấm tab "Mang về" 3. Quan sát danh sách | Chỉ hiện các đơn mang về |
| 1.1.4 | ☐ | Lọc tab "Đặt online" | 1. Vào trang lịch sử 2. Bấm tab "Đặt online" 3. Quan sát danh sách | Chỉ hiện đơn đặt online; nếu không có đơn nào thì danh sách rỗng |
| 1.1.5 | ☐ | Dropdown "Chọn bàn" | 1. Vào trang lịch sử 2. Tìm dropdown "Chọn bàn" trên thanh bộ lọc 3. Bấm dropdown, chọn một bàn cụ thể (VD: Bàn 1) 4. Quan sát danh sách đơn | Chỉ hiện các đơn thuộc bàn đã chọn |
| 1.1.6 | ☐ | (Mới) Bàn không bị trùng tên trong dropdown chọn bàn | 1. Vào tab "Tại bàn" 2. Mở dropdown "Tất cả bàn" 3. Quan sát danh sách bàn | Mỗi bàn chỉ xuất hiện 1 lần; chọn bàn có đơn phải ra đúng đơn của bàn đó (phát hiện 0616: "ban 1"/"ban 2" bị lặp 2 lần, chọn "ban 1" mục đầu ra rỗng dù có đơn ban1) |
| 1.1.7 | ☐ | (Mới) Tab "Tại bàn" loại đúng đơn mang về | 1. Vào tab "Tại bàn" 2. Quan sát danh sách & tổng số đơn | Chỉ hiển thị đơn tại bàn, KHÔNG gồm đơn "Mang về". **BUG 0619: tab "Tại bàn" vẫn hiển thị cả đơn "Bàn mang về" (tổng = tab Tất cả)** |

1.2 Tìm kiếm & bộ lọc

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.2.1 | ☐ | Tìm theo mã đơn | 1. Vào trang lịch sử 2. Tìm ô tìm kiếm trên thanh bộ lọc 3. Nhập đúng mã đơn có sẵn (VD: DH-00123) 4. Quan sát kết quả | Trả về đúng đơn có mã tương ứng |
| 1.2.2 | ☐ | Tìm theo số điện thoại | 1. Vào trang lịch sử 2. Nhập số điện thoại khách hàng vào ô tìm kiếm 3. Quan sát kết quả | Trả về các đơn của khách hàng có số điện thoại đó |
| 1.2.3 | ☐ | Tìm không khớp | 1. Vào trang lịch sử 2. Nhập chuỗi bất kỳ không tồn tại (VD: "xxxx9999") vào ô tìm kiếm 3. Quan sát danh sách | Danh sách rỗng, không hiện đơn nào |
| 1.2.4 | ☐ | Trạng thái: Đã thanh toán thành công | 1. Vào trang lịch sử 2. Tìm dropdown lọc trạng thái 3. Chọn "Đã thanh toán thành công" 4. Quan sát danh sách | Chỉ hiện các đơn đã thanh toán thành công |
| 1.2.5 | ☐ | Trạng thái: Chưa thanh toán | 1. Vào trang lịch sử 2. Bấm dropdown trạng thái 3. Chọn "Chưa thanh toán" 4. Quan sát danh sách | Chỉ hiện các đơn chưa thanh toán |
| 1.2.6 | ☐ | Trạng thái: Đã hủy | 1. Vào trang lịch sử 2. Bấm dropdown trạng thái 3. Chọn "Đã hủy" 4. Quan sát danh sách | Chỉ hiện các đơn đã bị hủy |
| 1.2.7 | ☐ | Trạng thái: Đã xử lý trả hàng | 1. Vào trang lịch sử 2. Bấm dropdown trạng thái 3. Chọn "Đã xử lý trả hàng" 4. Quan sát danh sách | Chỉ hiện các đơn đã xử lý trả hàng |
| 1.2.8 | ☐ | Trạng thái: Công nợ | 1. Vào trang lịch sử 2. Bấm dropdown trạng thái 3. Chọn "Công nợ" 4. Quan sát danh sách | Chỉ hiện các đơn đang ở trạng thái công nợ |
| 1.2.9 | ☐ | Lọc theo Tài khoản (nhân viên) | 1. Vào trang lịch sử 2. Tìm dropdown "Tài khoản" hoặc "Nhân viên" 3. Chọn một nhân viên cụ thể 4. Quan sát danh sách | Chỉ hiện các đơn do nhân viên đó tạo |
| 1.2.10 | ☐ | Khoảng ngày: Hôm nay | 1. Vào trang lịch sử 2. Bấm bộ lọc thời gian 3. Chọn "Hôm nay" 4. Quan sát danh sách | Chỉ hiện đơn được tạo trong ngày hôm nay |
| 1.2.11 | ☐ | Khoảng ngày: Hôm qua | 1. Vào trang lịch sử 2. Bấm bộ lọc thời gian 3. Chọn "Hôm qua" 4. Quan sát danh sách | Chỉ hiện đơn được tạo ngày hôm qua |
| 1.2.12 | ☐ | Khoảng ngày: Tuần này | 1. Vào trang lịch sử 2. Bấm bộ lọc thời gian 3. Chọn "Tuần này" 4. Quan sát danh sách | Chỉ hiện đơn trong tuần hiện tại |
| 1.2.13 | ☐ | Khoảng ngày: Tháng này | 1. Vào trang lịch sử 2. Bấm bộ lọc thời gian 3. Chọn "Tháng này" 4. Quan sát danh sách | Chỉ hiện đơn trong tháng hiện tại |
| 1.2.14 | ☐ | Khoảng ngày: Tùy chọn | 1. Vào trang lịch sử 2. Bấm bộ lọc thời gian, chọn "Tùy chọn" 3. Nhập ngày bắt đầu và ngày kết thúc cụ thể 4. Xác nhận và quan sát danh sách | Chỉ hiện đơn trong khoảng ngày đã nhập |
| 1.2.15 | ☐ | Kết hợp nhiều bộ lọc | 1. Vào trang lịch sử 2. Bật đồng thời: tab "Tại bàn" + Trạng thái "Đã thanh toán" + Thời gian "Hôm nay" 3. Quan sát danh sách kết quả | Chỉ hiện đơn thỏa tất cả điều kiện đã chọn |
| 1.2.16 | ☐ | Ngày bắt đầu > ngày kết thúc | 1. Vào trang lịch sử, bật lọc thời gian tùy chọn 2. Nhập ngày bắt đầu lớn hơn ngày kết thúc (VD: từ 10/06 đến 01/06) 3. Xác nhận và quan sát phản hồi | Hệ thống chặn hoặc hiển thị thông báo lỗi, không trả kết quả sai |
| 1.2.17 | ☐ | (Mới) Lọc khoảng ngày nhiều ngày phải trả đúng đơn trong khoảng | 1. Đảm bảo có đơn ở ≥2 ngày liên tiếp (VD hôm nay + hôm qua) 2. Chọn "Tuần này" (và "Tháng này") 3. Quan sát danh sách | Danh sách hiển thị TẤT CẢ đơn trong khoảng (≥ tổng đơn của các ngày trong khoảng). **BUG 0616: khoảng nhiều ngày trả về RỖNG dù chứa ngày có đơn — chỉ mốc 1 ngày chạy đúng** |
| 1.2.18 | ☐ | (Mới) Lọc theo trạng thái thực tế của hệ thống | 1. Mở dropdown "Trạng thái" 2. Lần lượt chọn: Đang xử lý / Hoàn thành / Đã hủy / Đã trả hàng / Chờ thanh toán 3. Quan sát danh sách mỗi lần | Mỗi trạng thái lọc đúng nhóm đơn tương ứng. (Lưu ý: tập trạng thái thực tế khác checklist gốc — không có "Công nợ"; "Hoàn thành"=đã thanh toán, "Chờ thanh toán"=chưa thanh toán) — **0619: tập trạng thái nay ĐÃ khớp checklist gốc: Đã thanh toán / Chưa thanh toán / Đã hủy / Đã xử lý trả hàng / Công nợ** |
| 1.2.19 | ☐ | (Mới) Tìm kiếm theo tên khách hàng | 1. Mở chi tiết 1 đơn có tên khách (VD "tranvana") 2. Nhập đúng tên khách vào ô tìm kiếm 3. Enter, quan sát | Trả về đơn của khách đó. **BUG 0619: tìm theo TÊN khách (tranvana) → rỗng; trong khi tìm theo mã đơn & SĐT vẫn đúng** (0623: vẫn lỗi) |
| 1.2.20 | ☐ | (Mới) Nút "Xuất Excel" | 1. Vào trang lịch sử, đặt bộ lọc (VD Tháng này) 2. Bấm nút "Xuất Excel" trên thanh bộ lọc 3. Quan sát file tải về | Xuất ra file Excel chứa đúng danh sách đơn theo bộ lọc đang áp dụng |

1.3 Danh sách đơn

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.3.1 | ☐ | Thẻ đơn hiển thị đủ thông tin | 1. Vào trang lịch sử 2. Quan sát một thẻ đơn bất kỳ trong danh sách 3. Kiểm tra từng thông tin: tên bàn, tài khoản nhân viên, ngày giờ, mã đơn, số tiền | Thẻ hiển thị đúng tên bàn, tài khoản, ngày giờ, mã đơn, số tiền |
| 1.3.2 | ☐ | Trạng thái thanh toán hiển thị đúng | 1. Vào trang lịch sử 2. Tìm một đơn đã thanh toán và một đơn chưa thanh toán 3. Quan sát nhãn trạng thái trên mỗi thẻ đơn | Đơn đã thanh toán hiển thị "Đã thanh toán"; đơn chưa thanh toán hiển thị "Chưa thanh toán" |
| 1.3.3 | ☐ | Trạng thái HĐĐT hiển thị đúng | 1. Vào trang lịch sử 2. Tìm đơn có cột/nhãn trạng thái hóa đơn điện tử (HĐĐT) 3. Quan sát giá trị hiển thị | Hiển thị đúng trạng thái: "Không xác định" hoặc "Chờ ký" tùy theo đơn |
| 1.3.4 | ☐ | Màu thẻ theo trạng thái | 1. Vào trang lịch sử 2. Quan sát màu nền hoặc màu viền các thẻ đơn 3. So sánh màu giữa đơn chưa thanh toán và đơn đã thanh toán | Đơn chưa thanh toán màu xám; đơn đã thanh toán màu xanh |
| 1.3.5 | ☐ | Số tiền trên thẻ khớp chi tiết đơn | 1. Quan sát số tiền hiển thị trên thẻ đơn, ghi nhận lại 2. Bấm vào thẻ đơn đó để mở chi tiết 3. So sánh số tiền trong modal chi tiết với số tiền trên thẻ | Số tiền trên thẻ = tổng tiền thanh toán trong chi tiết đơn |

1.4 Chi tiết đơn hàng

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.4.1 | ☐ | Bấm vào đơn mở modal chi tiết | 1. Vào trang lịch sử 2. Bấm vào bất kỳ thẻ đơn nào trong danh sách 3. Quan sát màn hình | Modal "Chi tiết đơn hàng" mở ra, tiêu đề hiển thị đúng mã đơn |
| 1.4.2 | ☐ | Thông tin đơn hiển thị đúng | 1. Mở modal chi tiết một đơn bất kỳ 2. Kiểm tra lần lượt: tên bàn, tên khách hàng, tên nhân viên, ngày giờ tạo đơn | Tất cả thông tin khớp với dữ liệu thực tế của đơn |
| 1.4.3 | ☐ | Danh sách món hiển thị đúng | 1. Mở modal chi tiết đơn 2. Quan sát bảng danh sách món bên trong modal 3. Kiểm tra từng dòng: tên món, số lượng, đơn giá, thành tiền | Tên, SL, đơn giá, thành tiền của từng dòng món hiển thị đúng |
| 1.4.4 | ☐ | Tổng tiền hàng tính đúng | 1. Mở modal chi tiết đơn 2. Cộng tay thành tiền của tất cả dòng món (Σ thành tiền) 3. So sánh với dòng "Tổng tiền hàng" trong modal | Tổng tiền hàng = Σ thành tiền các món |
| 1.4.5 | ☐ | Phụ thu / Giảm giá / Tiền điểm / VAT tính đúng | 1. Mở modal chi tiết đơn có áp phụ thu, giảm giá hoặc điểm thưởng 2. Quan sát từng dòng: Phụ thu, Giảm giá, Tiền điểm, VAT 3. Kiểm tra từng giá trị có đúng với lúc tạo đơn không | Mỗi dòng phụ thu / giảm giá / điểm / VAT hiển thị đúng giá trị đã áp |
| 1.4.6 | ☐ | Tổng tiền thanh toán tính đúng công thức | 1. Mở modal chi tiết đơn 2. Ghi nhận: Tổng tiền hàng, Phụ thu, Giảm giá, Tiền điểm, VAT 3. Tính tay: Tổng hàng + Phụ thu − Giảm giá − Tiền điểm + VAT 4. So sánh với "Tổng tiền thanh toán" hiển thị | Tổng tiền thanh toán = Tổng hàng + Phụ thu − Giảm giá − Tiền điểm + VAT |
| 1.4.7 | ☐ | Phương thức thanh toán hiển thị đúng | 1. Mở modal chi tiết đơn đã thanh toán 2. Tìm mục "Phương thức thanh toán" trong modal 3. So sánh với phương thức đã chọn lúc thanh toán (Tiền mặt / CK / Thẻ / QR) | Phương thức hiển thị đúng với lúc thanh toán thực tế |
| 1.4.8 | ☐ | Bấm "Đóng" thoát modal | 1. Mở modal chi tiết đơn 2. Bấm nút "Đóng" 3. Quan sát màn hình và bộ lọc đang áp | Modal đóng lại, quay về danh sách; bộ lọc và trang hiện tại giữ nguyên |
