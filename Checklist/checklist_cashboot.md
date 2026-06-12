# Checklist — Thu chi

1. Thu chi
1.1 Bộ lọc

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.1.1 | ☐ | Tìm theo Mã phiếu | 1. Đăng nhập, vào trang Thu chi 2. Tìm ô tìm kiếm "Mã phiếu" trên thanh bộ lọc 3. Nhập đúng mã phiếu có sẵn (VD: vote-00001) → quan sát kết quả 4. Xóa ô tìm kiếm, nhập chuỗi không tồn tại (VD: "xxxx999") → quan sát lại | Nhập mã đúng: trả về đúng phiếu. Nhập không khớp: danh sách rỗng |
| 1.1.2 | ☐ | Lọc theo Chi nhánh | 1. Vào trang Thu chi 2. Tìm dropdown "Chi nhánh" trên thanh bộ lọc 3. Bấm dropdown, chọn một chi nhánh cụ thể (VD: CN1) 4. Quan sát danh sách phiếu sau khi lọc | Chỉ hiện phiếu thuộc chi nhánh đã chọn |
| 1.1.3 | ☐ | Thời gian: Hôm nay / Hôm qua | 1. Vào trang Thu chi 2. Tìm bộ lọc thời gian 3. Chọn lần lượt "Hôm nay" → quan sát danh sách 4. Chọn "Hôm qua" → quan sát lại | Chỉ hiện phiếu trong ngày hôm nay / hôm qua tương ứng |
| 1.1.4 | ☐ | Thời gian: Tuần này / Tuần trước | 1. Vào trang Thu chi 2. Bấm bộ lọc thời gian 3. Chọn "Tuần này" → quan sát danh sách 4. Chọn "Tuần trước" → quan sát lại | Chỉ hiện phiếu trong khoảng tuần tương ứng |
| 1.1.5 | ☐ | Thời gian: Tháng này / Tháng trước | 1. Vào trang Thu chi 2. Bấm bộ lọc thời gian 3. Chọn "Tháng này" → quan sát danh sách 4. Chọn "Tháng trước" → quan sát lại | Chỉ hiện phiếu trong khoảng tháng tương ứng |
| 1.1.6 | ☐ | Thời gian: tùy chọn ngày | 1. Vào trang Thu chi 2. Bấm bộ lọc thời gian, chọn "Tùy chọn" hoặc "Khoảng ngày" 3. Nhập ngày bắt đầu và ngày kết thúc cụ thể 4. Xác nhận và quan sát danh sách | Chỉ hiện phiếu trong khoảng ngày đã nhập |
| 1.1.7 | ☐ | Lọc theo Người tạo | 1. Vào trang Thu chi 2. Tìm dropdown "Người tạo" trên thanh bộ lọc 3. Bấm dropdown, chọn một người dùng cụ thể 4. Quan sát danh sách phiếu | Chỉ hiện phiếu do người đã chọn tạo ra |
| 1.1.8 | ☐ | Lọc theo Loại thu chi (Thu / Chi) | 1. Vào trang Thu chi 2. Tìm dropdown "Loại thu chi" 3. Chọn "Thu" → quan sát danh sách 4. Đổi sang chọn "Chi" → quan sát lại | Chọn "Thu": chỉ hiện phiếu thu. Chọn "Chi": chỉ hiện phiếu chi |
| 1.1.9 | ☐ | Lọc theo Phân loại thu chi | 1. Vào trang Thu chi 2. Tìm dropdown "Phân loại thu chi" 3. Bấm dropdown, chọn một phân loại cụ thể 4. Quan sát danh sách phiếu | Chỉ hiện phiếu thuộc đúng phân loại đã chọn |
| 1.1.10 | ☐ | Lọc theo Loại nguồn | 1. Vào trang Thu chi 2. Tìm dropdown "Loại nguồn" 3. Lần lượt chọn từng giá trị: Bán hàng / Mua hàng / Tự tạo / Trả hàng 4. Quan sát danh sách sau mỗi lần chọn | Mỗi lần chọn chỉ hiện phiếu đúng nguồn tương ứng |
| 1.1.11 | ☐ | Kết hợp nhiều bộ lọc | 1. Vào trang Thu chi 2. Bật đồng thời nhiều bộ lọc: chọn Chi nhánh + Loại thu chi "Thu" + Thời gian "Tháng này" 3. Quan sát danh sách và các thẻ tổng quan bên trên | Danh sách chỉ hiện phiếu thỏa tất cả điều kiện; thẻ tổng quan cập nhật theo bộ lọc |

---

1.2 Tổng quan quỹ

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.2.1 | ☐ | Hiển thị Tồn quỹ đầu kỳ | 1. Vào trang Thu chi 2. Chọn khoảng thời gian cụ thể (VD: Tháng này) 3. Quan sát thẻ "Tồn quỹ đầu kỳ" | Hiển thị đúng số dư tồn quỹ tại thời điểm đầu kỳ đã lọc |
| 1.2.2 | ☐ | Hiển thị Tổng thu | 1. Vào trang Thu chi, chọn bộ lọc thời gian 2. Lọc danh sách chỉ hiện phiếu "Thu" (bằng cách bật lọc Loại = Thu) 3. Cộng tay số tiền tất cả phiếu thu trong danh sách 4. So sánh với thẻ "Tổng thu" | Tổng thu = Σ số tiền tất cả phiếu Thu trong bộ lọc |
| 1.2.3 | ☐ | Hiển thị Tổng chi | 1. Vào trang Thu chi, chọn bộ lọc thời gian 2. Lọc danh sách chỉ hiện phiếu "Chi" 3. Cộng tay số tiền tất cả phiếu chi trong danh sách 4. So sánh với thẻ "Tổng chi" | Tổng chi = Σ số tiền tất cả phiếu Chi trong bộ lọc |
| 1.2.4 | ☐ | Tồn quỹ cuối kỳ tính đúng | 1. Vào trang Thu chi 2. Ghi nhận 3 giá trị: Tồn đầu kỳ, Tổng thu, Tổng chi 3. Tính tay: Tồn đầu kỳ + Tổng thu − Tổng chi 4. So sánh kết quả với thẻ "Tồn quỹ cuối kỳ" | Tồn quỹ cuối kỳ = Tồn đầu kỳ + Tổng thu − Tổng chi |
| 1.2.5 | ☐ | Đổi bộ lọc thời gian → thẻ cập nhật | 1. Vào trang Thu chi, ghi nhận 4 giá trị thẻ tổng quan đang hiển thị 2. Thay đổi bộ lọc thời gian (VD: từ "Tháng này" sang "Hôm nay") 3. Quan sát 4 thẻ sau khi đổi lọc | Cả 4 thẻ (Tồn đầu kỳ, Tổng thu, Tổng chi, Tồn cuối kỳ) cập nhật theo kỳ mới |

---

1.3 Danh sách phiếu

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.3.1 | ☐ | Hiển thị bảng phiếu đủ cột | 1. Vào trang Thu chi 2. Quan sát bảng danh sách phiếu 3. Kiểm tra từng cột hiển thị: mã phiếu, loại, số tiền, chi nhánh, người nộp/nhận, người tạo, phân loại, PTTT, đính kèm, thời gian, mô tả | Bảng hiển thị đầy đủ tất cả các cột, dữ liệu điền đúng theo từng phiếu |
| 1.3.2 | ☐ | Phân trang | 1. Vào trang Thu chi với đủ số phiếu để có nhiều trang 2. Quan sát điều hướng trang (số trang, nút chuyển trang) 3. Bấm sang trang 2, trang 3 4. Quan sát dữ liệu từng trang | Chuyển trang đúng, dữ liệu mỗi trang không bị trùng hoặc thiếu |
| 1.3.3 | ☐ | Bấm icon xem để mở chi tiết | 1. Trong danh sách phiếu, tìm cột "Hành động" ở cuối mỗi dòng 2. Bấm icon xem (mắt/con mắt) tại một phiếu bất kỳ 3. Quan sát màn hình mở ra | Mở đúng trang hoặc modal chi tiết của phiếu đó |
| 1.3.4 | ☐ | Phiếu có đính kèm | 1. Trong danh sách phiếu, tìm một phiếu có file đính kèm (cột đính kèm hiển thị icon/link) 2. Bấm vào đính kèm đó 3. Quan sát kết quả | File đính kèm hiển thị hoặc tải xuống được, không báo lỗi |

---

1.4 Thêm phiếu

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.4.1 | ☐ | Bấm "Thêm" mở modal | 1. Vào trang Thu chi 2. Tìm và bấm nút "Thêm" (góc trên phải hoặc đầu bảng) 3. Quan sát màn hình | Modal "Thêm phiếu" mở ra |
| 1.4.2 | ☐ | Mã phiếu tự sinh | 1. Mở modal "Thêm phiếu" 2. Quan sát ô "Mã phiếu" ngay khi modal vừa mở | Mã phiếu được điền tự động (VD: vote-00001), không cần nhập tay |
| 1.4.3 | ☐ | Bỏ trống "Loại thu chi" (bắt buộc) | 1. Mở modal "Thêm phiếu" 2. Điền đầy đủ các trường khác nhưng để trống "Loại thu chi" 3. Bấm nút "Lưu" 4. Quan sát phản hồi | Hệ thống chặn lưu, hiển thị thông báo lỗi yêu cầu chọn Loại thu chi |
| 1.4.4 | ☐ | Bỏ trống "Số tiền" (bắt buộc) | 1. Mở modal "Thêm phiếu" 2. Điền đầy đủ các trường khác nhưng để trống ô "Số tiền" 3. Bấm nút "Lưu" 4. Quan sát phản hồi | Hệ thống chặn lưu, hiển thị thông báo lỗi yêu cầu nhập Số tiền |
| 1.4.5 | ☐ | Chọn Loại đối tượng / Người nộp | 1. Mở modal "Thêm phiếu" 2. Tìm dropdown "Loại đối tượng", chọn một loại (VD: Khách hàng) 3. Tìm ô "Người nộp", chọn hoặc nhập tên người nộp 4. Quan sát giá trị được ghi nhận | Loại đối tượng và Người nộp được chọn và hiển thị đúng trong form |
| 1.4.6 | ☐ | Chọn Phân loại thu chi | 1. Mở modal "Thêm phiếu" 2. Tìm dropdown "Phân loại thu chi" 3. Bấm dropdown, chọn một phân loại 4. Quan sát giá trị sau khi chọn | Phân loại được ghi nhận, hiển thị đúng trong ô |
| 1.4.7 | ☐ | Chọn Phương thức thanh toán | 1. Mở modal "Thêm phiếu" 2. Quan sát giá trị mặc định của "Phương thức thanh toán" (PTTT) 3. Đổi sang một phương thức khác (VD: Chuyển khoản) 4. Quan sát giá trị sau khi chọn | PTTT mặc định là "Tiền mặt"; đổi được sang phương thức khác và ghi nhận đúng |
| 1.4.8 | ☐ | Nhập Số tiền | 1. Mở modal "Thêm phiếu" 2. Bấm vào ô "Số tiền" 3. Thử nhập chữ cái → quan sát 4. Xóa, nhập số hợp lệ (VD: 150000) → quan sát định dạng hiển thị | Ô chỉ nhận số, tự định dạng theo kiểu tiền (VD: 150,000) |
| 1.4.9 | ☐ | Đính kèm tệp | 1. Mở modal "Thêm phiếu" 2. Tìm nút đính kèm tệp 3. Bấm và chọn một file từ máy tính 4. Quan sát file sau khi tải lên | File được tải lên thành công, hiển thị tên file trong form |
| 1.4.10 | ☐ | Mô tả giới hạn 200 ký tự | 1. Mở modal "Thêm phiếu" 2. Tìm ô "Mô tả" 3. Quan sát bộ đếm ký tự (0/200) 4. Nhập dần đến 200 ký tự → quan sát 5. Thử nhập thêm ký tự thứ 201 | Bộ đếm tăng dần; dừng tại 200, không nhập thêm được hoặc bị cắt ngắn |
| 1.4.11 | ☐ | Bấm "Lưu" hợp lệ | 1. Mở modal "Thêm phiếu" 2. Điền đầy đủ tất cả trường bắt buộc (Loại thu chi, Số tiền) 3. Bấm nút "Lưu" 4. Quan sát danh sách phiếu và thẻ tổng quan | Phiếu mới xuất hiện đầu danh sách; thẻ Tổng thu hoặc Tổng chi cập nhật tương ứng |
| 1.4.12 | ☐ | Bấm "Đóng" không tạo phiếu | 1. Mở modal "Thêm phiếu" 2. Điền một vài thông tin vào form 3. Bấm nút "Đóng" (không bấm Lưu) 4. Quan sát danh sách phiếu | Modal đóng lại; không có phiếu mới nào được tạo; danh sách không thay đổi |
| 1.4.13 | ☐ | Mã phiếu tăng dần sau mỗi lần tạo | 1. Mở modal "Thêm phiếu", ghi nhận mã phiếu hiển thị (VD: vote-00005) 2. Điền đủ trường bắt buộc, bấm "Lưu" 3. Mở lại modal "Thêm phiếu" lần 2 4. Quan sát mã phiếu mới | Mã phiếu lần 2 tăng thêm 1 (VD: vote-00006), không bị lặp lại mã cũ |
| 1.4.14 | ☐ | Nhập Số tiền = 0 | 1. Mở modal "Thêm phiếu" 2. Điền đầy đủ Loại thu chi 3. Nhập "0" vào ô Số tiền 4. Bấm "Lưu" 5. Quan sát phản hồi | Hệ thống chặn lưu, hiển thị thông báo lỗi yêu cầu số tiền lớn hơn 0 |
| 1.4.15 | ☐ | Loại đối tượng thay đổi → danh sách Người nộp thay đổi | 1. Mở modal "Thêm phiếu" 2. Bấm dropdown "Loại đối tượng", chọn "Khách hàng" → bấm dropdown "Người nộp" quan sát danh sách 3. Đổi "Loại đối tượng" sang "Nhân viên" → bấm dropdown "Người nộp" quan sát lại | Danh sách Người nộp thay đổi theo Loại đối tượng: chọn Khách hàng → chỉ list khách hàng; chọn Nhân viên → chỉ list nhân viên |
| 1.4.16 | ☐ | Loại đối tượng chưa chọn → Người nộp | 1. Mở modal "Thêm phiếu" 2. Không chọn "Loại đối tượng" 3. Bấm vào dropdown "Người nộp" 4. Quan sát trạng thái ô | Ô "Người nộp" bị disabled hoặc danh sách rỗng khi chưa chọn Loại đối tượng |
| 1.4.17 | ☐ | Loại thu chi = "Chi" → label đổi sang "Người nhận" | 1. Mở modal "Thêm phiếu" 2. Bấm dropdown "Loại thu chi", chọn "Thu" → quan sát nhãn bên phải 3. Đổi sang chọn "Chi" → quan sát lại nhãn | Chọn "Thu": nhãn hiển thị "Người nộp". Chọn "Chi": nhãn đổi thành "Người nhận" |
| 1.4.18 | ☐ | Xóa file đính kèm sau khi đã chọn | 1. Mở modal "Thêm phiếu" 2. Bấm "Chọn tệp", chọn một file từ máy 3. Quan sát file hiển thị trong ô đính kèm 4. Tìm và bấm nút xóa (X) bên cạnh tên file 5. Quan sát lại ô đính kèm | File bị xóa khỏi form, ô đính kèm trở về trạng thái "Chưa có tệp nào được chọn" |
| 1.4.19 | ☐ | Lưu phiếu thu → Tồn quỹ tăng đúng | 1. Vào trang Thu chi, ghi nhận "Tồn quỹ cuối kỳ" hiện tại (VD: 8,962,000đ) 2. Mở modal "Thêm phiếu", chọn Loại = "Thu", nhập Số tiền = 200,000đ, bấm "Lưu" 3. Quan sát thẻ "Tồn quỹ cuối kỳ" sau khi lưu | Tồn quỹ cuối kỳ tăng đúng 200,000đ (VD: thành 9,162,000đ) |
| 1.4.20 | ☐ | Lưu phiếu chi → Tồn quỹ giảm đúng | 1. Vào trang Thu chi, ghi nhận "Tồn quỹ cuối kỳ" hiện tại 2. Mở modal "Thêm phiếu", chọn Loại = "Chi", nhập Số tiền = 100,000đ, bấm "Lưu" 3. Quan sát thẻ "Tồn quỹ cuối kỳ" sau khi lưu | Tồn quỹ cuối kỳ giảm đúng 100,000đ |

---

1.5 Ghi nhận 4 loại phiếu (logic chính)

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.5.1 | ☐ | Tạo Phiếu thu thủ công | 1. Vào trang Thu chi, ghi nhận "Tổng thu" và "Tồn quỹ cuối kỳ" hiện tại 2. Bấm "Thêm", chọn Loại = "Thu", nhập số tiền (VD: 100,000đ), bấm "Lưu" 3. Quan sát danh sách và thẻ tổng quan | Phiếu mới có Loại = Thu xuất hiện; Tổng thu và Tồn quỹ cuối kỳ tăng đúng 100,000đ |
| 1.5.2 | ☐ | Tạo Phiếu chi thủ công | 1. Vào trang Thu chi, ghi nhận "Tổng chi" và "Tồn quỹ cuối kỳ" hiện tại 2. Bấm "Thêm", chọn Loại = "Chi", nhập số tiền (VD: 50,000đ), bấm "Lưu" 3. Quan sát danh sách và thẻ tổng quan | Phiếu mới có Loại = Chi xuất hiện; Tổng chi tăng và Tồn quỹ cuối kỳ giảm đúng 50,000đ |
| 1.5.3 | ☐ | Phiếu thu hiển thị đúng thông tin | 1. Trong danh sách phiếu, tìm một phiếu thu thủ công vừa tạo 2. Kiểm tra từng cột: Loại = Thu, Số tiền đúng, tên Người nộp, PTTT đã chọn | Tất cả cột hiển thị đúng với dữ liệu đã nhập lúc tạo |
| 1.5.4 | ☐ | Phiếu chi hiển thị đúng thông tin | 1. Trong danh sách phiếu, tìm một phiếu chi thủ công vừa tạo 2. Kiểm tra từng cột: Loại = Chi, Số tiền đúng, tên Người nhận, PTTT đã chọn | Tất cả cột hiển thị đúng với dữ liệu đã nhập lúc tạo |
| 1.5.5 | ☐ | Hoàn tất đơn bán → tự sinh Phiếu bán hàng | 1. Vào cashier, chọn bàn, thêm món, thực hiện thanh toán thành công 2. Quay lại trang Thu chi, lọc "Loại nguồn = Bán hàng" 3. Tìm phiếu vừa sinh ra tương ứng với đơn bán 4. Kiểm tra thông tin phiếu | Phiếu Loại = Thu, Loại nguồn = Bán hàng, số tiền = tổng đơn bán vừa thanh toán |
| 1.5.6 | ☐ | Thực hiện trả hàng → tự sinh Phiếu trả hàng | 1. Thực hiện một phiếu trả hàng (hoàn tiền) từ màn hình cashier hoặc quản lý đơn 2. Quay lại trang Thu chi, lọc "Loại nguồn = Trả hàng" 3. Tìm phiếu vừa sinh ra 4. Kiểm tra thông tin phiếu | Phiếu Loại = Chi (hoàn tiền), Loại nguồn = Trả hàng, số tiền = giá trị hàng trả |
| 1.5.7 | ☐ | Lọc Loại nguồn = Bán hàng | 1. Vào trang Thu chi 2. Bật bộ lọc "Loại nguồn", chọn "Bán hàng" 3. Quan sát toàn bộ danh sách | Chỉ hiện các phiếu được sinh tự động từ đơn bán hàng |
| 1.5.8 | ☐ | Lọc Loại nguồn = Trả hàng | 1. Vào trang Thu chi 2. Bật bộ lọc "Loại nguồn", chọn "Trả hàng" 3. Quan sát toàn bộ danh sách | Chỉ hiện các phiếu được sinh tự động từ phiếu trả hàng |
| 1.5.9 | ☐ | Lọc Loại nguồn = Tự tạo | 1. Vào trang Thu chi 2. Bật bộ lọc "Loại nguồn", chọn "Tự tạo" 3. Quan sát toàn bộ danh sách | Chỉ hiện các phiếu thu/chi được tạo thủ công bởi nhân viên |
| 1.5.10 | ☐ | Số tiền phiếu bán hàng khớp đơn gốc | 1. Ghi lại tổng tiền thanh toán của một đơn bán vừa hoàn tất (VD: 250,000đ) 2. Vào trang Thu chi, lọc Loại nguồn = Bán hàng 3. Tìm phiếu tương ứng với đơn đó 4. So sánh số tiền phiếu với tổng đơn | Số tiền phiếu bán hàng = tổng tiền thanh toán đơn gốc |
| 1.5.11 | ☐ | Số tiền phiếu trả hàng khớp đơn gốc | 1. Ghi lại giá trị hàng trả của một phiếu trả hàng vừa thực hiện 2. Vào trang Thu chi, lọc Loại nguồn = Trả hàng 3. Tìm phiếu tương ứng 4. So sánh số tiền | Số tiền phiếu trả hàng = giá trị hàng trả của đơn gốc |
| 1.5.12 | ☐ | PTTT của phiếu tự sinh khớp đơn gốc | 1. Hoàn tất một đơn bán bằng phương thức "Chuyển khoản" 2. Vào trang Thu chi, tìm phiếu sinh ra từ đơn đó 3. Kiểm tra cột "PTTT" của phiếu | PTTT của phiếu = phương thức thanh toán của đơn bán/trả gốc (VD: Chuyển khoản) |
| 1.5.13 | ☐ | Đơn bán bị hủy → phiếu không tính vào quỹ | 1. Ghi nhận Tổng thu hiện tại 2. Tạo một đơn bán rồi hủy đơn đó (không thanh toán) 3. Vào trang Thu chi, kiểm tra Tổng thu và Tồn quỹ | Tổng thu và Tồn quỹ không thay đổi; không có phiếu mới sinh ra từ đơn bị hủy |
| 1.5.14 | ☐ | Số liệu Thu chi khớp với Điều phối ca | 1. Mở tab Điều phối ca, ghi lại số tiền và PTTT của một giao dịch bất kỳ trong ca 2. Vào trang Thu chi, tìm phiếu tương ứng 3. So sánh số tiền và PTTT giữa hai màn hình | Số tiền và phương thức thanh toán khớp nhau, không bị lệch |
| 1.5.15 | ☐ | Tổng thu = Σ tất cả nguồn thu | 1. Vào trang Thu chi, bật lọc Loại = "Thu" 2. Cộng tay tất cả số tiền phiếu thu trong danh sách (bao gồm thu thủ công + bán hàng) 3. So sánh kết quả với thẻ "Tổng thu" | Tổng thu trên thẻ = Σ số tiền tất cả phiếu thu (thủ công + bán hàng) |
| 1.5.16 | ☐ | Tổng chi = Σ tất cả nguồn chi | 1. Vào trang Thu chi, bật lọc Loại = "Chi" 2. Cộng tay tất cả số tiền phiếu chi trong danh sách (bao gồm chi thủ công + trả hàng) 3. So sánh kết quả với thẻ "Tổng chi" | Tổng chi trên thẻ = Σ số tiền tất cả phiếu chi (thủ công + trả hàng) |

---

1.6 Xuất Excel

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.6.1 | ☐ | Bấm "Xuất Excel" | 1. Vào trang Thu chi 2. Áp một bộ lọc bất kỳ (VD: Tháng này) 3. Tìm và bấm nút "Xuất Excel" 4. Quan sát kết quả trình duyệt | Trình duyệt kích hoạt tải file, file Excel được tải xuống thành công |
| 1.6.2 | ☐ | File xuất đúng dữ liệu theo bộ lọc | 1. Vào trang Thu chi, áp bộ lọc cụ thể (VD: Loại = Thu, Tháng này) 2. Ghi nhận số dòng và tổng tiền hiển thị trên màn hình 3. Bấm "Xuất Excel", mở file vừa tải 4. So sánh nội dung file với dữ liệu trên màn hình | File Excel chứa đúng số dòng và dữ liệu khớp với bộ lọc đang áp dụng |

---

1.7 Công nợ (tab Công nợ)

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|--------------------|------------------|------------------|
| 1.7.1 | ☐ | Mở tab Công nợ | 1. Mở Thu chi → bấm tab "Công nợ". | Mở màn hình Công nợ với panel "Bộ Lọc" bên trái. |
| 1.7.2 | ☐ | Đối tượng mặc định | 1. Quan sát mục "Đối tượng" gồm 2 checkbox. | Có checkbox "Khách hàng" và "Nhà cung cấp", mặc định cả 2 được tích. |
| 1.7.3 | ☐ | Lọc chỉ Khách hàng | 1. Bỏ tích "Nhà cung cấp", chỉ giữ "Khách hàng". 2. Xem danh sách. | Chỉ hiển thị công nợ của Khách hàng. |
| 1.7.4 | ☐ | Lọc chỉ Nhà cung cấp | 1. Bỏ tích "Khách hàng", chỉ giữ "Nhà cung cấp". 2. Xem danh sách. | Chỉ hiển thị công nợ của Nhà cung cấp. |
| 1.7.5 | ☐ | Bỏ tích cả 2 đối tượng | 1. Bỏ tích cả 2 checkbox đối tượng. | Danh sách rỗng (không có đối tượng nào được chọn). |
| 1.7.6 | ☐ | Tìm theo Tên đối tượng | 1. Tại ô "Tên đối tượng", gõ tên một khách/NCC có công nợ. | Chỉ hiển thị công nợ của đối tượng khớp tên; tên sai → rỗng. |
| 1.7.7 | ☐ | Tìm theo Mã công nợ | 1. Tại ô "Mã công nợ", gõ một mã công nợ. | Trả đúng dòng công nợ khớp mã; không khớp → rỗng. |
| 1.7.8 | ☐ | Lọc theo Chi nhánh | 1. Mở dropdown "Chi nhánh". 2. Chọn/bỏ chọn chi nhánh (multi-select, có nút xóa ×). | Chỉ hiện công nợ của chi nhánh đã chọn; bỏ chọn thì cập nhật lại. |
| 1.7.9 | ☐ | Lọc theo Người tạo | 1. Mở dropdown "Người tạo". 2. Chọn 1 người tạo. | Chỉ hiện công nợ do người đã chọn tạo. |
| 1.7.10 | ☐ | Kết hợp nhiều bộ lọc | 1. Kết hợp nhiều bộ lọc (Đối tượng + Chi nhánh + Tên). | Kết quả giao đúng tất cả điều kiện đã chọn. |
| 1.7.11 | ☐ | Bảng công nợ hiển thị đủ thông tin | 1. Khi có dữ liệu, quan sát bảng công nợ. 2. Đọc các cột. | Hiển thị thông tin công nợ: đối tượng, mã công nợ, chi nhánh, số tiền nợ, người tạo... |
| 1.7.12 | ☐ | Xem chi tiết công nợ | 1. Bấm xem chi tiết một dòng công nợ (nếu có). | Mở chi tiết công nợ của đối tượng đúng. |
| 1.7.13 | ☐ | (tiếp tục bổ sung nếu có thêm testcase) | | |
