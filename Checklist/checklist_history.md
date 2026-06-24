# Checklist — Menu HISTORY

1. Lịch sử
1.1 Bộ lọc loại đơn

> **Lưu ý:**
> - Muốn kiểm tra bàn hiển thị đúng không → vào trang quản lí admin → click "Cài đặt" → vào "Quản lí bàn" để kiểm tra.
> - Khi search theo đơn tại bàn, thì không hiện đơn mang về.

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.1.1 | ☐ | Lọc tab "Tất cả" | 1. Đăng nhập, truy cập link cashier history 2. Quan sát các tab lọc loại đơn phía trên danh sách 3. Bấm tab "Tất cả" 4. Quan sát danh sách đơn | Hiển thị tất cả đơn không phân biệt loại |
| 1.1.2 | ☐ | Lọc tab "Tại bàn" | 1. Vào trang lịch sử 2. Bấm tab "Tại bàn" 3. Quan sát từng đơn trong danh sách | Chỉ hiện các đơn loại tại bàn |
| 1.1.3 | ☐ | Lọc tab "Mang về" | 1. Vào trang lịch sử 2. Bấm tab "Mang về" 3. Quan sát danh sách | Chỉ hiện các đơn mang về |
| 1.1.4 | ☐ | Lọc tab "Đặt online" | 1. Vào trang lịch sử 2. Bấm tab "Đặt online" 3. Quan sát danh sách | Chỉ hiện đơn đặt online; nếu không có đơn nào thì danh sách rỗng |
| 1.1.5 | ☐ | Dropdown "Chọn bàn" | 1. Vào trang lịch sử 2. Tìm dropdown "Chọn bàn" trên thanh bộ lọc 3. Bấm dropdown, chọn một bàn cụ thể (VD: Bàn 1) 4. Quan sát danh sách đơn | Chỉ hiện các đơn thuộc bàn đã chọn |
| 1.1.6 | ☐ | (Mới) Bàn không bị trùng tên trong dropdown chọn bàn | 1. Vào trang quản lí admin 2. Click "Cài đặt" 3. Vào "Quản lí bàn" 4. Quan sát danh sách bàn hiển thị | Mỗi bàn chỉ xuất hiện 1 lần; chọn bàn có đơn phải ra đúng đơn của bàn đó (phát hiện 0616: "ban 1"/"ban 2" bị lặp 2 lần, chọn "ban 1" mục đầu ra rỗng dù có đơn ban1) |
| 1.1.7 | ☐ | (Mới) Tab "Tại bàn" loại đúng đơn mang về | 1. Vào tab "Tại bàn" 2. Quan sát danh sách & tổng số đơn | Chỉ hiển thị đơn tại bàn, KHÔNG gồm đơn "Mang về".|

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
| 1.2.17 | ☐ | (Mới) Lọc khoảng ngày nhiều ngày phải trả đúng đơn trong khoảng | 1. Đảm bảo có đơn ở ≥2 ngày liên tiếp (VD hôm nay + hôm qua) 2. Chọn "Tuần này" (và "Tháng này") 3. Quan sát danh sách | Danh sách hiển thị TẤT CẢ đơn trong khoảng (≥ tổng đơn của các ngày trong khoảng).|
| 1.2.18 | ☐ | (Mới) Lọc theo trạng thái thực tế của hệ thống | 1. Mở dropdown "Trạng thái" 2. Lần lượt chọn: Đang xử lý / Hoàn thành / Đã hủy / Đã trả hàng / Chờ thanh toán 3. Quan sát danh sách mỗi lần | Mỗi trạng thái lọc đúng nhóm đơn tương ứng. (Lưu ý: tập trạng thái thực tế khác checklist gốc — không có "Công nợ"; "Hoàn thành"=đã thanh toán, "Chờ thanh toán"=chưa thanh toán) 
| 1.2.19 | ☐ | (Mới) Tìm kiếm theo tên khách hàng | 1. Mở chi tiết 1 đơn có tên khách (VD "tranvana") 2. Nhập đúng tên khách vào ô tìm kiếm 3. Enter, quan sát | Trả về đơn của khách đó. (0623: vẫn lỗi) |
| 1.2.20 | ☐ | (Mới) Nút "Xuất Excel" | 1. Vào trang lịch sử, đặt bộ lọc (VD Tháng này) 2. Bấm nút "Xuất Excel" trên thanh bộ lọc 3. Quan sát file tải về | Xuất ra file Excel chứa đúng danh sách đơn theo bộ lọc đang áp dụng |
| 1.2.21 | ☐ | (Mới) Khoảng ngày: Quý này | 1. Vào trang lịch sử 2. Bấm bộ lọc thời gian 3. Chọn "Quý này" 4. Bấm "Áp dụng", quan sát danh sách | Chỉ hiện đơn trong quý hiện tại (VD 01/04–30/06/2026); tổng ≥ số đơn của "Tháng này" (phát hiện 0623: hộp thoại thời gian có thêm mốc "Quý này" & "Năm nay" chưa có trong checklist gốc) |
| 1.2.22 | ☐ | (Mới) Khoảng ngày: Năm nay | 1. Vào trang lịch sử 2. Bấm bộ lọc thời gian 3. Chọn "Năm nay" 4. Bấm "Áp dụng", quan sát danh sách | Chỉ hiện đơn trong năm hiện tại (01/01–31/12/2026) |
| 1.2.23 | ☐ | (Mới) Lịch chặn chọn ngày tương lai | 1. Mở bộ lọc thời gian → xem lịch tháng hiện tại 2. Thử bấm chọn một ngày trong tương lai (VD 24–30/06 khi hôm nay 23/06) | Các ngày tương lai bị làm mờ và không cho chọn; chỉ chọn được ngày ≤ hôm nay |
| 1.2.24 | ☐ | (Mới) Hộp thoại ngày — nút "Hủy" | 1. Mở bộ lọc thời gian 2. Chọn một mốc khác mốc hiện tại (VD "Tháng này") 3. Bấm "Hủy" | Hộp thoại đóng, KHÔNG áp dụng thay đổi; bộ lọc giữ nguyên mốc trước đó |
| 1.2.25 | ☐ | (Mới) Hộp thoại ngày — nút "Áp dụng" | 1. Mở bộ lọc thời gian 2. Chọn một mốc (VD "Tháng này") 3. Bấm "Áp dụng" | Hộp thoại đóng, danh sách cập nhật theo mốc đã chọn; nhãn nút bộ lọc đổi tương ứng |
| 1.2.26 | ☐ | (Mới) Bộ lọc mặc định khi mở trang | 1. Đăng nhập, vào Lịch sử lần đầu 2. Quan sát trạng thái các bộ lọc | Mặc định: tab "Tất cả", Trạng thái "Tất cả", "Tất cả bàn", thời gian "Hôm nay"; danh sách chỉ hiện đơn hôm nay |
| 1.2.27 | ☐ | (Mới) Dropdown "Trạng thái" đủ mục | 1. Mở dropdown "Trạng thái" 2. Quan sát danh sách mục | Có đúng 6 mục: Tất cả / Đã thanh toán / Chưa thanh toán / Đã hủy / Đã xử lý trả hàng / Công nợ (xác nhận 0623) |

1.3 Danh sách đơn

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.3.1 | ☐ | Thẻ đơn hiển thị đủ thông tin | 1. Vào trang lịch sử 2. Quan sát một thẻ đơn bất kỳ trong danh sách 3. Kiểm tra từng thông tin: tên bàn, tài khoản nhân viên, ngày giờ, mã đơn, số tiền | Thẻ hiển thị đúng tên bàn, tài khoản, ngày giờ, mã đơn, số tiền |
| 1.3.2 | ☐ | Trạng thái thanh toán hiển thị đúng | **Chuẩn bị dữ liệu (nếu chưa có):** (a) Đơn chưa TT: Trang chủ → chọn bàn → thêm món → KHÔNG bấm Thanh toán, để đơn mở. (b) Đơn đã TT: Trang chủ → chọn bàn → thêm món → bấm "Thanh toán" → nhập tiền khách = tổng đơn → xác nhận. (c) Đơn công nợ: như (b) nhưng nhập tiền khách < tổng đơn. 1. Vào Lịch sử 2. Tìm lần lượt 3 đơn vừa tạo 3. Quan sát nhãn trạng thái trên mỗi thẻ | Đơn chưa TT hiển thị "Chưa thanh toán" (thẻ xám); đơn đã TT hiển thị "Đã thanh toán" (thẻ xanh); đơn công nợ hiển thị "Công nợ" |
| 1.3.3 | ☐ | Trạng thái HĐĐT hiển thị đúng | 1. Vào trang lịch sử 2. Tìm đơn có cột/nhãn trạng thái hóa đơn điện tử (HĐĐT) 3. Quan sát giá trị hiển thị | Hiển thị đúng trạng thái: "Không xác định" hoặc "Chờ ký" tùy theo đơn |
| 1.3.4 | ☐ | Màu thẻ theo trạng thái | 1. Vào trang lịch sử 2. Quan sát màu nền hoặc màu viền các thẻ đơn 3. So sánh màu giữa đơn chưa thanh toán và đơn đã thanh toán | Đơn chưa thanh toán màu xám; đơn đã thanh toán màu xanh |
| 1.3.5 | ☐ | Số tiền trên thẻ khớp chi tiết đơn | 1. Quan sát số tiền hiển thị trên thẻ đơn, ghi nhận lại 2. Bấm vào thẻ đơn đó để mở chi tiết 3. So sánh số tiền trong modal chi tiết với số tiền trên thẻ | Số tiền trên thẻ = tổng tiền thanh toán trong chi tiết đơn |
| 1.3.6 | ☐ | (Mới) Bộ đếm "Tổng: X đơn" | 1. Vào trang lịch sử 2. Quan sát dòng "Tổng: X đơn" phía trên danh sách 3. Lần lượt đổi bộ lọc (tab / trạng thái / thời gian) | Số ở "Tổng" khớp số thẻ đơn đang hiển thị và cập nhật đúng mỗi khi đổi bộ lọc |

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
| 1.4.9 | ☐ | (Mới) Bấm thân thẻ không mở chi tiết | 1. Vào trang lịch sử 2. Bấm vào phần thân thẻ đơn (không phải nút "...") 3. Quan sát màn hình | KHÔNG mở modal khi bấm thân thẻ; chỉ mở được chi tiết qua menu "..." → "Chi tiết" (xác nhận 0623) |
| 1.4.10 | ☐ | (Mới) Menu "..." của đơn chưa thanh toán | 1. Bấm nút "..." trên thẻ đơn ở trạng thái "Chưa thanh toán" 2. Quan sát các mục trong menu | Menu chỉ có mục "Chi tiết" (đơn chưa thanh toán không có In/Hủy/Trả hàng) — cần đối chiếu thêm menu của đơn đã thanh toán |
| 1.4.11 | ☐ | (Mới) Modal hiển thị "Số khách" | 1. Mở modal chi tiết một đơn 2. Tìm dòng "Số khách" trong khối "Thông tin đơn hàng" | Hiển thị đúng số khách của đơn (VD: 1) |
| 1.4.12 | ☐ | (Mới) Modal hiển thị mục "Ghi chú" | 1. Mở modal chi tiết một đơn 2. Tìm mục "Ghi chú" bên dưới khối thông tin đơn | Có ô "Ghi chú": hiển thị nội dung nếu đơn có ghi chú, để trống nếu không |
| 1.4.13 | ☐ | (Mới) Tiêu đề & badge trạng thái trong modal | 1. Mở modal chi tiết một đơn 2. Quan sát tiêu đề và nhãn trạng thái góc phải | Tiêu đề "Chi tiết hóa đơn"; hiển thị badge trạng thái (VD "Chưa thanh toán") khớp trạng thái trên thẻ |
| 1.4.14 | ☐ | (Mới) Menu "..." của đơn ĐÃ THANH TOÁN | 1. Bấm "..." trên thẻ đơn trạng thái "Đã thanh toán" 2. Quan sát các mục trong menu | Có 5 mục: Chi tiết / In lại bill / In lại tem / In lại HĐĐT / Trả hàng (phát hiện 0624) |
| 1.4.15 | ☐ | (Mới) Menu "..." của đơn CÔNG NỢ | 1. Bấm "..." trên thẻ đơn trạng thái "Công nợ" 2. Quan sát các mục trong menu | Có 5 mục: Chi tiết / In lại bill / In lại tem / In lại HĐĐT / **Thanh toán nợ** (khác đơn đã TT: có "Thanh toán nợ" thay cho "Trả hàng") (phát hiện 0624) |
| 1.4.16 | ☐ | (Mới) Menu "..." của đơn ĐÃ HỦY | 1. Bấm "..." trên thẻ đơn trạng thái "Đã hủy" 2. Quan sát các mục trong menu | Có 5 mục: Chi tiết / In lại bill / In lại tem / In lại HĐĐT / Trả hàng (phát hiện 0624) |
| 1.4.17 | ☐ | (Mới) Modal hiển thị dòng "Tích điểm" | 1. Mở modal chi tiết một đơn 2. Tìm dòng "Tích điểm" trong khối thanh toán (giữa "Giảm giá" và "VAT") | Hiển thị số điểm tích lũy của đơn (VD 5210); không trừ vào tổng thanh toán (phát hiện 0624 trên POS15062070CN2) |

---

1.5 Tạo đơn từ Trang chủ và kiểm tra trong Lịch sử

> **Lưu ý chung cho mục 1.5:**
> - **Luồng tạo đơn bán hàng:** Trang chủ → chọn bàn → thêm sản phẩm → bấm "Thanh toán" → chọn PTTT, nhập số tiền → xác nhận.
> - **Đơn chưa thanh toán:** Tạo đơn tại bàn, KHÔNG bấm "Thanh toán" — đơn vẫn đang mở.
> - **Đơn đã thanh toán:** Bấm "Thanh toán", nhập số tiền khách = tổng đơn, xác nhận.
> - **Đơn công nợ:** Bấm "Thanh toán", nhập số tiền khách < tổng đơn — hệ thống tự ghi phần còn lại là công nợ.
> - Phiếu bán hàng (POS…) = tổng tiền đơn; Phiếu thu (PC…) = số tiền khách đã trả thực tế.

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.5.1 | ☐ | Đơn chưa thanh toán xuất hiện trong Lịch sử | 1. Trang chủ → chọn bàn → thêm ≥ 1 sản phẩm 2. KHÔNG bấm "Thanh toán", để nguyên đơn đang mở 3. Vào Lịch sử → đặt bộ lọc Trạng thái = "Chưa thanh toán" hoặc "Tất cả" 4. Tìm đơn vừa tạo theo bàn/thời gian | Đơn xuất hiện trong danh sách với trạng thái "Chưa thanh toán"; thẻ màu xám |
| 1.5.2 | ☐ | Đơn đã thanh toán đầy đủ xuất hiện trong Lịch sử | 1. Trang chủ → chọn bàn → thêm ≥ 1 sản phẩm 2. Bấm "Thanh toán", ghi tổng đơn = X 3. Chọn PTTT Tiền mặt, nhập tiền khách = X, xác nhận 4. Vào Lịch sử → tìm đơn vừa tạo | Đơn xuất hiện với trạng thái "Đã thanh toán"; thẻ màu xanh; số tiền = X |
| 1.5.3 | ☐ | Đơn công nợ (thanh toán một phần) xuất hiện trong Lịch sử | 1. Trang chủ → chọn bàn → thêm ≥ 1 sản phẩm (tổng đơn = X) 2. Bấm "Thanh toán", nhập tiền khách = Y (Y < X), xác nhận; hệ thống tự ghi nợ phần còn lại (X − Y) 3. Vào Lịch sử → tìm đơn vừa tạo | Đơn xuất hiện với trạng thái "Công nợ"; số tiền hiển thị trên thẻ = X (tổng đơn) |
| 1.5.4 | ☐ | Chi tiết đơn công nợ hiển thị đúng phần đã trả và còn nợ | 1. Tạo đơn công nợ như 1.5.3 (tổng X, đã trả Y, nợ X − Y) 2. Vào Lịch sử → bấm "..." → "Chi tiết" trên đơn đó 3. Quan sát khối thanh toán trong modal chi tiết | Modal hiển thị: Tổng đơn = X; Đã thanh toán = Y (Phiếu thu PC…); Còn lại / Công nợ = X − Y; tổng khớp công thức |
| 1.5.5 | ☐ | Mã đơn, tên bàn, số tiền trong Lịch sử khớp đơn vừa tạo | 1. Tạo và hoàn tất 1 đơn (đã TT), ghi mã POS…, tên bàn, tổng tiền 2. Vào Lịch sử → tìm đơn theo mã hoặc thời gian 3. So sánh thông tin trên thẻ và trong modal chi tiết với dữ liệu ghi trước | Mã đơn, tên bàn, tổng tiền, PTTT, trạng thái trong Lịch sử khớp đúng với đơn vừa tạo |
| 1.5.6 | ☐ | Đơn mới xuất hiện ngay trong Lịch sử (real-time) | 1. Mở sẵn trang Lịch sử (bộ lọc "Hôm nay") ở một tab hoặc ghi nhận tổng số đơn 2. Sang Trang chủ → chọn bàn → tạo và hoàn tất đơn 3. Quay lại Lịch sử (reload hoặc tự cập nhật) 4. Quan sát danh sách | Đơn mới xuất hiện ngay; tổng số đơn tăng đúng +1; không cần đăng xuất/đăng nhập lại |
| 1.5.7 | ☐ | Lọc "Chưa thanh toán" chỉ trả đơn chưa TT (không lẫn công nợ) | 1. Tạo đủ 3 loại đơn: chưa TT, đã TT, công nợ (theo luồng 1.5.1–1.5.3) 2. Vào Lịch sử → lọc Trạng thái = "Chưa thanh toán" 3. Quan sát kết quả | Chỉ hiện đơn chưa thanh toán; đơn công nợ KHÔNG xuất hiện trong nhóm này |
| 1.5.8 | ☐ | Lọc "Công nợ" chỉ trả đơn công nợ | 1. Đã có đủ 3 loại đơn từ 1.5.1–1.5.3 2. Lọc Trạng thái = "Công nợ" 3. Quan sát kết quả | Chỉ hiện đơn thanh toán một phần; đơn chưa TT và đã TT KHÔNG xuất hiện |

---

1.6 Luồng tạo công nợ và xem chi tiết thanh toán trong Lịch sử

> **Luồng đầy đủ cần kiểm thử:**
> Trang chủ → chọn bàn → thêm sản phẩm → bấm "Thanh toán" → chọn PTTT **Tiền mặt** → nhập số tiền khách trả **< tổng đơn** → xác nhận (hệ thống tự ghi phần còn lại là công nợ) → vào **Lịch sử** → tìm kiếm đơn → bấm "..." → "Chi tiết" → xem chi tiết thanh toán công nợ.
>
> **Ký hiệu dùng trong bảng:** X = tổng tiền đơn hàng · Y = số tiền khách trả (Y < X) · Nợ = X − Y

**[Giai đoạn 1] Tạo đơn và thanh toán sinh công nợ (tại Trang chủ)**

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.6.1 | ☐ | Màn hình thanh toán hiển thị đúng tổng đơn | 1. Trang chủ → chọn bàn → thêm ≥ 1 sản phẩm 2. Bấm "Thanh toán" 3. Quan sát tổng tiền hiển thị trên màn hình thanh toán | Tổng tiền trên màn hình thanh toán = X (khớp tổng giá các món đã thêm) |
| 1.6.2 | ☐ | Chọn PTTT Tiền mặt trên màn hình thanh toán | 1. Trên màn hình thanh toán, tìm mục phương thức thanh toán 2. Chọn "Tiền mặt" 3. Quan sát ô nhập tiền khách | PTTT Tiền mặt được chọn; ô nhập "Tiền khách đưa" hiển thị và có thể nhập số |
| 1.6.3 | ☐ | Nhập tiền khách < tổng đơn → hiển thị số tiền còn thiếu | 1. Trên màn hình thanh toán (PTTT Tiền mặt), nhập tiền khách = Y (Y < X) 2. Quan sát phần phản hồi bên dưới ô nhập (tiền thừa/tiền thiếu) | Hiển thị số tiền còn thiếu = X − Y (hoặc "Còn nợ: X−Y"); KHÔNG hiển thị "Tiền thừa" |
| 1.6.4 | ☐ | Xác nhận thanh toán → tạo thành công đơn công nợ | 1. Đã nhập Y < X, bấm "Xác nhận" hoặc "Thanh toán" 2. Quan sát thông báo / màn hình kết quả sau thanh toán | Hệ thống xác nhận thành công; sinh mã Phiếu bán hàng (POS…) và Phiếu thu (PC…); ghi nhận X, Y, Nợ = X − Y |
| 1.6.5 | ☐ | Màn hình xác nhận hiển thị đúng số nợ còn lại | 1. Sau khi xác nhận thanh toán công nợ, quan sát màn hình kết quả 2. Tìm dòng tổng đơn, tiền đã trả, số tiền còn nợ | Tổng đơn = X; Tiền đã trả (Tiền mặt) = Y; Công nợ = X − Y; các giá trị khớp với số nhập |

**[Giai đoạn 2] Tìm đơn công nợ trong Lịch sử**

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.6.6 | ☐ | Đơn công nợ xuất hiện ngay trong Lịch sử sau khi tạo | 1. Sau khi tạo công nợ, vào menu Lịch sử 2. Bộ lọc mặc định "Hôm nay" + "Tất cả" 3. Quan sát danh sách | Đơn vừa tạo xuất hiện trong danh sách; trạng thái "Công nợ" |
| 1.6.7 | ☐ | Tìm kiếm đơn công nợ theo mã POS… | 1. Vào Lịch sử, nhập mã POS… (ghi nhận ở bước 1.6.4) vào ô tìm kiếm 2. Quan sát kết quả | Trả về đúng 1 đơn có mã POS… vừa nhập; trạng thái hiển thị "Công nợ" |
| 1.6.8 | ☐ | Lọc trạng thái "Công nợ" hiển thị đơn vừa tạo | 1. Vào Lịch sử 2. Mở dropdown Trạng thái → chọn "Công nợ" 3. Quan sát danh sách | Đơn công nợ vừa tạo xuất hiện trong danh sách; các đơn đã TT và chưa TT không xuất hiện |
| 1.6.9 | ☐ | Thẻ đơn công nợ hiển thị đủ thông tin | 1. Tìm ra đơn công nợ trong danh sách (lọc "Công nợ" hoặc tìm mã) 2. Quan sát thẻ đơn: tên bàn, nhân viên, ngày giờ, mã đơn, số tiền, trạng thái | Thẻ hiển thị đủ: tên bàn đúng, mã POS…, số tiền = X (tổng đơn), badge/nhãn "Công nợ" |

**[Giai đoạn 3] Mở chi tiết và kiểm tra thông tin thanh toán công nợ**

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.6.10 | ☐ | Bấm "..." → menu hiển thị đúng cho đơn công nợ | 1. Tìm thẻ đơn công nợ trong Lịch sử 2. Bấm nút "..." trên thẻ 3. Quan sát các mục trong menu | Menu hiện: Chi tiết / In lại bill / In lại tem / In lại HĐĐT / **Thanh toán nợ** (không có "Trả hàng") |
| 1.6.11 | ☐ | Bấm "Chi tiết" mở modal chi tiết đúng đơn | 1. Bấm "..." → chọn "Chi tiết" trên đơn công nợ 2. Quan sát modal mở ra | Modal "Chi tiết hóa đơn" mở; tiêu đề/mã đơn khớp đơn công nợ vừa chọn |
| 1.6.12 | ☐ | Modal chi tiết: badge trạng thái "Công nợ" | 1. Mở modal chi tiết đơn công nợ 2. Quan sát badge/nhãn trạng thái trong modal | Badge hiển thị "Công nợ"; màu sắc phân biệt với "Đã thanh toán" và "Chưa thanh toán" |
| 1.6.13 | ☐ | Modal chi tiết: tổng tiền đơn = X | 1. Trong modal chi tiết đơn công nợ, tìm dòng "Tổng tiền thanh toán" hoặc tổng đơn 2. So sánh với X (tổng đơn lúc tạo) | Tổng tiền đơn hiển thị = X |
| 1.6.14 | ☐ | Modal chi tiết: số tiền đã trả = Y (Tiền mặt) | 1. Trong modal chi tiết, tìm mục "Đã thanh toán" hoặc phần thanh toán tiền mặt 2. So sánh với Y (số tiền khách đã trả) | Hiển thị đã thanh toán = Y; PTTT ghi rõ "Tiền mặt" |
| 1.6.15 | ☐ | Modal chi tiết: số tiền còn nợ = X − Y | 1. Trong modal chi tiết, tìm dòng "Công nợ" hoặc "Còn lại" 2. So sánh với X − Y | Hiển thị đúng số nợ còn lại = X − Y; không âm, không bị làm tròn sai |
| 1.6.16 | ☐ | Công thức khớp: Tổng đơn = Đã trả + Còn nợ | 1. Trong modal chi tiết, đọc 3 giá trị: Tổng đơn, Đã trả, Còn nợ 2. Kiểm tra: Đã trả + Còn nợ = Tổng đơn | Tổng đơn X = Y (đã trả) + (X − Y) (còn nợ); không lệch |
| 1.6.17 | ☐ | Modal chi tiết: danh sách món và tổng hàng đúng | 1. Trong modal chi tiết đơn công nợ, quan sát bảng danh sách món 2. Cộng tay thành tiền các dòng món 3. So sánh với "Tổng tiền hàng" | Danh sách món hiển thị đúng; Tổng tiền hàng = Σ thành tiền các món |
| 1.6.18 | ☐ | Đóng modal → quay về danh sách Lịch sử | 1. Trong modal chi tiết đơn công nợ, bấm "Đóng" 2. Quan sát màn hình | Modal đóng; quay về danh sách Lịch sử; bộ lọc đang áp không bị reset |

**[Giai đoạn 4] Kiểm tra chéo và biên**

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.6.19 | ☐ | Tiền khách nhập = 0 → hệ thống có cho phép tạo công nợ không | 1. Màn hình thanh toán, chọn Tiền mặt 2. Nhập tiền khách = 0 (hoặc bỏ trống) 3. Bấm xác nhận 4. Quan sát phản hồi | Ghi nhận hành vi: hệ thống chặn lỗi / cảnh báo / hoặc cho phép tạo nợ 100% — ghi nhận kết quả thực tế |
| 1.6.20 | ☐ | Tiền khách nhập = X (đúng bằng tổng) → không tạo công nợ | 1. Màn hình thanh toán, chọn Tiền mặt 2. Nhập tiền khách = X (bằng tổng đơn) 3. Xác nhận 4. Vào Lịch sử kiểm tra | Đơn tạo thành công với trạng thái "Đã thanh toán", KHÔNG phải "Công nợ" |
| 1.6.21 | ☐ | Tiền khách nhập > X → tiền thừa, không tạo công nợ | 1. Màn hình thanh toán, chọn Tiền mặt 2. Nhập tiền khách > X (VD X + 10.000) 3. Quan sát dòng tiền thừa 4. Xác nhận, kiểm tra Lịch sử | Hiển thị "Tiền thừa = nhập − X"; đơn tạo với trạng thái "Đã thanh toán", KHÔNG phải "Công nợ" |
| 1.6.22 | ☐ | Reload trang Lịch sử giữ nguyên đơn công nợ | 1. Sau khi tạo công nợ, vào Lịch sử tìm thấy đơn 2. Tải lại trang (F5) 3. Lọc lại "Công nợ", tìm đơn đó 4. Mở chi tiết | Đơn vẫn hiển thị "Công nợ"; số tiền đã trả Y và nợ X−Y không bị thay đổi sau reload |

