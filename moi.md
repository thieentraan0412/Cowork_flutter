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
| 1.7.13 | ☐ | Chip trạng thái công nợ | 1. Mở tab Công nợ 2. Quan sát hàng chip phía trên: "Tất cả (n)", "Gần đến hạn (n)", "Quá hạn (n)", "Hôm nay (n)" 3. Đọc số đếm trong ngoặc từng chip | Hiện đủ 4 chip kèm số đếm; số liệu hợp lý (Gần đến hạn + Quá hạn ≤ Tất cả) |
| 1.7.14 | ☐ | Lọc theo chip "Quá hạn" | 1. Mở tab Công nợ 2. Bấm chip "Quá hạn (n)" 3. Quan sát danh sách và cột Trạng thái | Chỉ hiện công nợ trạng thái "Đã quá hạn N ngày"; số dòng = số trên chip |
| 1.7.15 | ☐ | Lọc theo chip "Gần đến hạn" | 1. Mở tab Công nợ 2. Bấm chip "Gần đến hạn (n)" 3. Quan sát cột Ngày đáo hạn / Hạn còn | Chỉ hiện công nợ sắp đến hạn; số dòng khớp số trên chip |
| 1.7.16 | ☐ | Bảng công nợ đủ cột | 1. Mở tab Công nợ khi có dữ liệu 2. Kiểm tra từng cột: STT, Mã công nợ, Loại đối tượng, Tên đối tượng, Mã đơn, Chi nhánh, Chưa thanh toán, Đã thanh toán, Tổng tiền, Hạn còn, Ngày đáo hạn, Trạng thái, Người tạo, Hành động | Hiển thị đầy đủ các cột, dữ liệu điền đúng từng dòng |
| 1.7.17 | ☐ | Chưa TT + Đã TT = Tổng tiền | 1. Mở tab Công nợ, chọn một dòng bất kỳ 2. Đọc 3 giá trị: Chưa thanh toán, Đã thanh toán, Tổng tiền 3. Cộng tay Chưa TT + Đã TT | Chưa thanh toán + Đã thanh toán = Tổng tiền (từng dòng) |
| 1.7.18 | ☐ | Mở modal "Thanh toán nợ" | 1. Trong bảng công nợ, tại cột Hành động bấm icon thanh toán/bút của một dòng 2. Quan sát màn hình | Mở modal "Thanh toán nợ" đúng đối tượng, hiển thị số nợ còn lại |
| 1.7.19 | ☐ | Trạng thái thanh toán (một phần / đủ) | 1. Quan sát cột Trạng thái 2. Đối chiếu Đã thanh toán so với Tổng tiền | Đã TT = 0 → chưa thanh toán; 0 < Đã TT < Tổng → "Thanh toán một phần"; Đã TT = Tổng → "Đã thanh toán đủ" |
| 1.7.20 | ☐ | Đóng modal Thanh toán nợ không lưu | 1. Mở modal "Thanh toán nợ" 2. Bấm "Đóng"/X mà không nhập gì 3. Quan sát bảng công nợ | Modal đóng, số liệu công nợ không thay đổi |

---

## Ghi chú UI thực tế (cập nhật từ phiên kiểm thử 0619 & 0623)
> Các mục **1.8 trở đi** dùng đúng thuật ngữ/giá trị thực tế trên giao diện hiện tại:
> - Mã phiếu thực tế: **PC…** (phiếu thu) / **PT…** (phiếu chi) — KHÔNG phải "vote-00001".
> - Thẻ tổng quan: **Tồn đầu kỳ · Tổng thu · Tổng chi · Số dư cuối ca**.
> - Modal Thêm phiếu: trường **"Loại nhân sự"** (Quản lý / Quầy bếp / Thu ngân / Nhân viên order / Khác) liên động **"Người nộp/Người nhận"**; nút lưu là **"Tạo mới"**; ô **Mô tả** giới hạn **50** ký tự.
> - Bộ lọc **"Loại nguồn"**: Bán hàng / Mua hàng / Trả hàng / Tự tạo.

1.8 Sửa phiếu thu chi

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.8.1 | ☐ | Nhận diện thao tác ở cột Hành động | 1. Vào trang Thu chi 2. Tại một dòng phiếu, quan sát cột "Hành động" (cuối dòng) 3. Xác định các icon: xem (mắt), sửa (bút), xóa (thùng rác) nếu có | Ghi nhận đúng các thao tác khả dụng trên mỗi phiếu (xem/sửa/xóa) |
| 1.8.2 | ☐ | Mở chế độ sửa phiếu thủ công | 1. Tìm một phiếu "Tự tạo" (do nhân viên tạo) 2. Bấm icon sửa/bút 3. Quan sát màn hình | Mở modal/form sửa với dữ liệu phiếu được điền sẵn |
| 1.8.3 | ☐ | Sửa Số tiền phiếu | 1. Mở sửa một phiếu thu thủ công (VD đang 100.000) 2. Đổi Số tiền sang 120.000 3. Bấm "Lưu"/"Cập nhật" 4. Quan sát danh sách & thẻ Tổng thu | Số tiền phiếu cập nhật 120.000; Tổng thu & Số dư cuối ca thay đổi đúng chênh lệch (+20.000) |
| 1.8.4 | ☐ | Sửa Phân loại / PTTT / Mô tả | 1. Mở sửa một phiếu thủ công 2. Đổi Phân loại thu chi, đổi PTTT, sửa Mô tả 3. Lưu 4. Mở lại chi tiết phiếu | Các trường cập nhật đúng giá trị mới khi xem lại |
| 1.8.5 | ☐ | Hủy sửa không lưu thay đổi | 1. Mở sửa một phiếu 2. Thay đổi vài trường 3. Bấm "Đóng"/Hủy (không Lưu) 4. Mở lại chi tiết | Phiếu giữ nguyên dữ liệu cũ, thay đổi không áp dụng |
| 1.8.6 | ☐ | Phiếu tự sinh không cho sửa | 1. Lọc Loại nguồn = "Bán hàng" 2. Mở một phiếu tự sinh 3. Tìm thao tác sửa | Phiếu tự sinh từ đơn bán/trả không cho sửa số tiền (chỉ xem); nút sửa ẩn/disabled |
| 1.8.7 | ☐ | Sửa Số tiền về 0 (biên) | 1. Mở sửa một phiếu thủ công 2. Đổi Số tiền = 0 3. Lưu | Hệ thống chặn, báo lỗi "số tiền phải lớn hơn 0" (đối chiếu BUG-01 ở phần Thêm) |

---

1.9 Xóa phiếu thu chi

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.9.1 | ☐ | Mở xác nhận xóa phiếu | 1. Tại một phiếu thủ công, bấm icon xóa (thùng rác) ở cột Hành động 2. Quan sát màn hình | Hiện hộp thoại xác nhận trước khi xóa, không xóa ngay |
| 1.9.2 | ☐ | Hủy xóa | 1. Bấm icon xóa một phiếu 2. Tại hộp thoại xác nhận, bấm "Hủy"/"Không" 3. Quan sát danh sách | Phiếu không bị xóa, danh sách giữ nguyên |
| 1.9.3 | ☐ | Xác nhận xóa phiếu thu thủ công | 1. Ghi nhận Tổng thu & Số dư cuối ca 2. Xóa một phiếu thu thủ công (VD 100.000), xác nhận 3. Quan sát danh sách & thẻ | Phiếu biến mất; Tổng thu −100.000; Số dư cuối ca giảm tương ứng; số bản ghi −1 |
| 1.9.4 | ☐ | Xác nhận xóa phiếu chi thủ công | 1. Ghi nhận Tổng chi & Số dư 2. Xóa một phiếu chi thủ công (VD 50.000), xác nhận 3. Quan sát thẻ | Phiếu biến mất; Tổng chi −50.000; Số dư cuối ca tăng lại 50.000 |
| 1.9.5 | ☐ | Phiếu tự sinh không cho xóa | 1. Lọc Loại nguồn = "Bán hàng" 2. Tìm thao tác xóa trên phiếu tự sinh | Phiếu tự sinh từ đơn bán/trả không cho xóa (nút ẩn/disabled hoặc bị chặn) |
| 1.9.6 | ☐ | Xóa phiếu rồi tải lại trang | 1. Xóa một phiếu thủ công 2. Tải lại trang (F5) 3. Tìm lại phiếu vừa xóa | Phiếu đã xóa không xuất hiện lại sau khi tải lại (xóa được lưu phía server) |

---

1.10 Sắp xếp & tương tác bảng

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.10.1 | ☐ | Sắp xếp theo Thời gian ghi nhận | 1. Vào Thu chi 2. Bấm tiêu đề cột "Thời gian ghi nhận" 3. Bấm lần 2 để đảo chiều | Danh sách sắp xếp tăng/giảm theo thời gian; mũi tên chiều sắp xếp đổi |
| 1.10.2 | ☐ | Sắp xếp theo Số tiền | 1. Bấm tiêu đề cột "Số tiền" 2. Quan sát thứ tự 3. Bấm lần 2 đảo chiều | Danh sách sắp xếp theo số tiền tăng dần ↔ giảm dần |
| 1.10.3 | ☐ | Thứ tự mặc định mới nhất lên đầu | 1. Tạo một phiếu mới 2. Không sắp xếp, quan sát vị trí phiếu | Phiếu mới nhất nằm đầu danh sách (mặc định sắp theo thời gian giảm dần) |
| 1.10.4 | ☐ | Cuộn ngang bảng nhiều cột | 1. Quan sát bảng 13 cột 2. Cuộn ngang | Cuộn xem hết các cột; tiêu đề cột thẳng hàng với dữ liệu |
| 1.10.5 | ☐ | Giữ sắp xếp khi chuyển trang | 1. Sắp xếp theo Số tiền giảm dần 2. Chuyển sang trang 2 3. Quan sát thứ tự | Sắp xếp được giữ nguyên xuyên suốt các trang |

---

1.11 Sinh mã phiếu & định dạng số tiền

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.11.1 | ☐ | Tiền tố mã phiếu PC/PT | 1. Tạo 1 phiếu thu và 1 phiếu chi 2. Quan sát mã phiếu sinh ra | Phiếu thu tiền tố **PC…**, phiếu chi tiền tố **PT…** |
| 1.11.2 | ☐ | Mã phiếu thu tăng dần độc lập | 1. Tạo 2 phiếu thu liên tiếp 2. Ghi mã từng phiếu | Mã phiếu thu tăng +1 mỗi lần (VD PC00001649 → PC00001650), không trùng |
| 1.11.3 | ☐ | Mã phiếu chi tăng dần độc lập | 1. Tạo 2 phiếu chi liên tiếp 2. Ghi mã | Mã phiếu chi tăng theo chuỗi riêng (VD PT00000037 → PT00000038) |
| 1.11.4 | ☐ | Không sinh mã "toàn số 0" | 1. Tạo phiếu hợp lệ nhiều lần 2. Quan sát mã sinh ra | Không xuất hiện mã PT00000000/PC00000000 (toàn số 0) — đối chiếu lỗi đã ghi nhận |
| 1.11.5 | ☐ | Số tiền hiển thị có dấu phân cách | 1. Tạo phiếu Số tiền 1500000 2. Xem trong danh sách & chi tiết | Hiển thị "1.500.000đ" (dấu chấm ngăn cách hàng nghìn, hậu tố đ) |
| 1.11.6 | ☐ | Định dạng khi gõ Số tiền | 1. Mở Thêm phiếu 2. Gõ 1500000 vào ô Số tiền 3. Quan sát ô trong lúc gõ | Ghi nhận hành vi định dạng khi gõ (hiện tại KHÔNG tự chèn dấu phẩy) |
| 1.11.7 | ☐ | Hiển thị số âm khi lọc | 1. Lọc Loại thu chi = chỉ "Phiếu chi" 2. Quan sát thẻ Tồn đầu kỳ / Số dư cuối ca | Ghi nhận: số có thể ra ÂM (VD −22.294.150) do tính lại theo bộ lọc — đối chiếu FIND-BALANCE |

---

1.12 Kiểm thử biên — Thêm phiếu

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.12.1 | ☐ | Số tiền rất lớn | 1. Mở Thêm phiếu, chọn Loại=Thu 2. Nhập số rất lớn (VD 999.999.999.999) 3. Lưu | Xử lý đúng: lưu & hiển thị đủ chữ số, hoặc chặn với thông báo giới hạn rõ ràng |
| 1.12.2 | ☐ | Số tiền có phần thập phân | 1. Mở Thêm phiếu 2. Nhập "1000.5" hoặc "1000,5" vào Số tiền 3. Lưu | Xử lý nhất quán: làm tròn hoặc chặn; không lưu giá trị sai lệch |
| 1.12.3 | ☐ | Số tiền âm | 1. Mở Thêm phiếu 2. Thử nhập "-5000" vào Số tiền 3. Lưu | Ô không nhận dấu trừ, hoặc chặn lưu với thông báo lỗi |
| 1.12.4 | ☐ | Nhập chữ vào ô Số tiền | 1. Mở Thêm phiếu 2. Gõ "abc" vào ô Số tiền 3. Quan sát | Ô chỉ nhận ký tự số, bỏ qua chữ cái |
| 1.12.5 | ☐ | Mô tả đúng 50 ký tự (biên) | 1. Mở Thêm phiếu 2. Nhập đúng 50 ký tự vào Mô tả, xem counter "50/50" 3. Thử nhập ký tự thứ 51 | Bộ đếm dừng ở 50/50; không nhập thêm được ký tự thứ 51 |
| 1.12.6 | ☐ | Mô tả ký tự đặc biệt & emoji | 1. Mở Thêm phiếu 2. Nhập Mô tả có ký tự đặc biệt (!@#), tiếng Việt có dấu, emoji 3. Lưu & xem lại chi tiết | Lưu & hiển thị đúng ký tự đã nhập, không lỗi hiển thị |
| 1.12.7 | ☐ | Bỏ trống Loại nhân sự / Người nộp | 1. Mở Thêm phiếu, chọn Loại=Thu, nhập Số tiền 2. Bỏ trống Loại nhân sự & Người nộp 3. Lưu | Ghi nhận: hệ thống cho lưu (không bắt buộc) hay chặn — đối chiếu kỳ vọng nghiệp vụ |
| 1.12.8 | ☐ | Liên động Loại nhân sự → Người nộp | 1. Mở Thêm phiếu 2. Chọn Loại nhân sự "Thu ngân" → xem Người nộp 3. Đổi sang "Quản lý" → xem lại | Người nộp tự lọc theo vai trò (Thu ngân → casher2…; Quản lý → danh sách quản lý) |
| 1.12.9 | ☐ | Chưa chọn Loại nhân sự → Người nộp | 1. Mở Thêm phiếu 2. Không chọn Loại nhân sự 3. Bấm dropdown Người nộp | Người nộp hiển thị "No data found"/rỗng khi chưa chọn Loại nhân sự |
| 1.12.10 | ☐ | Tạo nhiều phiếu liên tiếp nhanh | 1. Tạo phiếu hợp lệ, Lưu 2. Mở lại Thêm phiếu ngay, tạo tiếp 3. Lặp 3-4 lần | Mỗi phiếu lưu thành công, mã tăng đúng, không kẹt "lớp phủ ma" / double-submit |

---

1.13 Phương thức thanh toán (PTTT)

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.13.1 | ☐ | PTTT mặc định "Tiền mặt" | 1. Mở Thêm phiếu 2. Quan sát giá trị mặc định ô PTTT | Mặc định là "Tiền mặt" |
| 1.13.2 | ☐ | Danh sách PTTT đầy đủ | 1. Mở Thêm phiếu 2. Bấm dropdown PTTT 3. Liệt kê các lựa chọn | Hiển thị các phương thức: Tiền mặt, Chuyển khoản, QR (Tự động)… đúng cấu hình |
| 1.13.3 | ☐ | Tạo phiếu PTTT "Chuyển khoản" | 1. Mở Thêm phiếu, chọn PTTT "Chuyển khoản" 2. Điền hợp lệ, Lưu 3. Xem cột PTTT trong danh sách | Phiếu lưu đúng PTTT "Chuyển khoản" |
| 1.13.4 | ☐ | Đối chiếu PTTT phiếu tự sinh | 1. Lọc Loại nguồn = Bán hàng 2. Xem cột PTTT các phiếu | PTTT phiếu tự sinh phản ánh đúng phương thức của đơn gốc (Tiền mặt / Chuyển khoản / QR Tự động) |

---

1.14 Tồn quỹ & tính liên tục kỳ (nâng cao)

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.14.1 | ☐ | Cuối kỳ trước = Đầu kỳ sau (tháng) | 1. Lọc "Tháng trước", ghi Số dư cuối ca 2. Lọc "Tháng này", ghi Tồn đầu kỳ 3. So sánh | Số dư cuối ca tháng trước = Tồn đầu kỳ tháng này (tính liên tục) |
| 1.14.2 | ☐ | Liên tục theo tuần | 1. Ghi Số dư cuối ca "Tuần trước" 2. Ghi Tồn đầu kỳ "Tuần này" 3. So sánh | Hai giá trị khớp nhau |
| 1.14.3 | ☐ | Công thức số dư đúng ở mọi kỳ | 1. Với mỗi preset (Hôm nay/Tuần/Tháng): ghi Tồn đầu kỳ, Tổng thu, Tổng chi 2. Tính Đầu kỳ + Thu − Chi 3. So với Số dư cuối ca | Số dư cuối ca = Tồn đầu kỳ + Tổng thu − Tổng chi ở mọi kỳ |
| 1.14.4 | ☐ | Tồn đầu kỳ cố định khi đổi Loại thu chi | 1. Không lọc loại: ghi Tồn đầu kỳ 2. Lọc chỉ "Phiếu chi": ghi lại Tồn đầu kỳ 3. So sánh | KỲ VỌNG: Tồn đầu kỳ KHÔNG đổi theo bộ lọc loại. (Hiện đang đổi → ghi FAIL/FIND-BALANCE) |
| 1.14.5 | ☐ | Quỹ cập nhật realtime sau thêm phiếu | 1. Ghi Số dư cuối ca 2. Thêm phiếu thu 200.000, Lưu 3. Quan sát thẻ ngay (không tải lại) | Số dư cuối ca tăng đúng 200.000 ngay lập tức |

---

1.15 Loại nguồn — phiếu tự sinh & Mua hàng

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.15.1 | ☐ | Lọc Loại nguồn = Mua hàng | 1. Vào Thu chi 2. Bật lọc "Loại nguồn" = "Mua hàng" 3. Quan sát danh sách | Chỉ hiện phiếu sinh từ nghiệp vụ mua hàng (thường là phiếu Chi); nếu rỗng thì ghi nhận không có dữ liệu kỳ này |
| 1.15.2 | ☐ | Chọn nhiều Loại nguồn cùng lúc | 1. Bật lọc Loại nguồn, tích "Bán hàng" + "Tự tạo" 2. Quan sát danh sách | Hiện phiếu thuộc cả 2 nguồn đã chọn (multi-select hợp nhất) |
| 1.15.3 | ☐ | Phiếu "Tự tạo" = phiếu thủ công | 1. Tạo 1 phiếu thủ công 2. Lọc Loại nguồn = "Tự tạo" 3. Tìm phiếu vừa tạo | Phiếu thủ công vừa tạo xuất hiện trong nhóm "Tự tạo" |
| 1.15.4 | ☐ | Đối chiếu Bán hàng với đơn gốc | 1. Hoàn tất 1 đơn bán (VD 250.000, Chuyển khoản) 2. Lọc Loại nguồn = Bán hàng 3. Tìm phiếu tương ứng | Phiếu Thu, số tiền = 250.000, PTTT = Chuyển khoản, khớp đơn gốc |
| 1.15.5 | ☐ | Đối chiếu Trả hàng với đơn gốc | 1. Thực hiện 1 phiếu trả hàng 2. Lọc Loại nguồn = Trả hàng 3. Tìm phiếu | Phiếu Chi (hoàn tiền), số tiền = giá trị hàng trả, khớp đơn gốc |

---

1.16 Bộ lọc nâng cao — xóa/đặt lại & giữ trạng thái

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.16.1 | ☐ | Xóa từng bộ lọc | 1. Bật nhiều bộ lọc (Chi nhánh + Loại + Thời gian) 2. Tìm nút × trên từng filter/chip 3. Bấm xóa từng cái | Mỗi lần xóa 1 filter, danh sách & thẻ cập nhật lại tương ứng |
| 1.16.2 | ☐ | Nút "Đặt lại"/"Xóa lọc" | 1. Bật nhiều bộ lọc 2. Tìm và bấm nút đặt lại bộ lọc (nếu có) | Tất cả bộ lọc về mặc định, danh sách hiển thị toàn bộ |
| 1.16.3 | ☐ | Giữ bộ lọc khi tải lại trang | 1. Bật lọc Tháng này + CN1 2. Tải lại trang (F5) 3. Quan sát bộ lọc & danh sách | Ghi nhận: bộ lọc có được giữ sau reload hay reset về mặc định |
| 1.16.4 | ☐ | Bộ lọc cho kết quả rỗng | 1. Chọn tổ hợp lọc chắc chắn rỗng (VD Người tạo không có phiếu) 2. Quan sát | Hiện "Không có dữ liệu"; 4 thẻ tổng quan về 0 (hoặc giá trị đầu kỳ hợp lý) |
| 1.16.5 | ☐ | Tìm mã phiếu ngoài kỳ lọc | 1. Lọc Tháng này 2. Nhập mã phiếu thuộc tháng khác 3. Quan sát | Ghi nhận hành vi: mã ngoài kỳ → rỗng, hay bỏ qua bộ lọc thời gian |

---

1.17 Phân quyền & phạm vi chi nhánh

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.17.1 | ☐ | Thu ngân chỉ thấy chi nhánh của mình | 1. Đăng nhập vai trò Thu ngân (CN1) 2. Mở dropdown Chi nhánh 3. Quan sát các chi nhánh khả dụng | Chỉ hiển thị chi nhánh thuộc phạm vi thu ngân (VD CN1/cn11/cn12) |
| 1.17.2 | ☐ | Phiếu tạo gắn đúng chi nhánh | 1. Tạo phiếu thủ công khi đang ở CN1 2. Xem cột "Tên chi nhánh" của phiếu | Phiếu mới gắn đúng chi nhánh hiện hành (mã phiếu có hậu tố CN tương ứng) |
| 1.17.3 | ☐ | Người tạo phiếu = tài khoản đăng nhập | 1. Tạo phiếu thủ công 2. Xem cột "Người tạo" | Người tạo = tài khoản đang đăng nhập (admin) |

---

1.18 Trạng thái rỗng & xử lý lỗi

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.18.1 | ☐ | Danh sách rỗng hiển thị đúng | 1. Lọc đến tổ hợp không có phiếu 2. Quan sát vùng bảng | Hiện thông báo "Không có dữ liệu"/empty state, không vỡ giao diện |
| 1.18.2 | ☐ | Tải lại khi kẹt "lớp phủ ma" | 1. Khi dropdown/modal bị kẹt overlay 2. Tải lại trang (F5) 3. Thao tác lại | Sau khi tải lại, giao diện hoạt động bình thường (quirk môi trường Flutter cần lưu ý) |
| 1.18.3 | ☐ | Đóng modal bằng Esc / click ngoài | 1. Mở modal Thêm phiếu 2. Nhấn Esc hoặc click vùng ngoài modal | Modal đóng lại, không tạo phiếu |
| 1.18.4 | ☐ | Lỗi mạng khi Lưu | 1. Mở Thêm phiếu, điền hợp lệ 2. (Nếu mô phỏng được) ngắt mạng rồi bấm Tạo mới | Hiện thông báo lỗi mạng rõ ràng, không tạo phiếu trùng/rác |

---

1.19 Regression — Lỗi & lệch đã biết (kiểm lại mỗi phiên)

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.19.1 | ☐ | BUG-01: Số tiền = 0 vẫn tạo phiếu | 1. Thêm phiếu, Loại=Chi, Số tiền=0 2. Bấm "Tạo mới" 3. Quan sát | ĐÃ FIX nếu: chặn + báo "số tiền phải > 0". CÒN LỖI nếu: tạo thành công PT00000000. (Tồn từ 0616→0623) |
| 1.19.2 | ☐ | LỆCH-01: Giới hạn Mô tả 50 vs 200 | 1. Mở Thêm phiếu, xem counter ô Mô tả | Ghi nhận giới hạn hiện tại (50). Cần thống nhất spec: 50 hay 200 |
| 1.19.3 | ☐ | LỆCH-02: Label Người nộp/Người nhận | 1. Mở Thêm phiếu, Loại=Thu → xem label 2. Đổi Loại=Chi → xem lại | ĐÃ FIX nếu: Thu→"Người nộp", Chi→"Người nhận". CÒN LỆCH nếu: luôn gộp "Người nộp/Người nhận" |
| 1.19.4 | ☐ | LỆCH-03: "Loại nhân sự" vs "Loại đối tượng" | 1. Mở Thêm phiếu, xem trường liên động Người nộp 2. Đọc các giá trị | Ghi nhận: trường là "Loại nhân sự" theo vai trò. So spec "Loại đối tượng" (Khách hàng/Nhân viên) |
| 1.19.5 | ☐ | FIND-BALANCE: Đầu kỳ đổi theo lọc loại | 1. Lọc chỉ "Phiếu chi" (Tháng này) 2. Xem Tồn đầu kỳ & Số dư cuối ca | ĐÃ FIX nếu: Đầu kỳ giữ cố định. CÒN VẤN ĐỀ nếu: ra số âm (VD −22.294.150) gây hiểu nhầm |
| 1.19.6 | ☐ | Mã phiếu "toàn số 0" | 1. Tạo vài phiếu hợp lệ 2. Kiểm tra mã sinh ra | Không có mã PT00000000/PC00000000; mỗi mã là số thứ tự hợp lệ tăng dần |
| 1.19.7 | ☐ | Cải thiện: Loại nguồn đúng giá trị | 1. Mở bộ lọc "Loại nguồn" 2. Đọc các giá trị | Có đúng Bán hàng/Mua hàng/Trả hàng/Tự tạo (đã sửa từ phiên 0619 vốn theo vai trò) |
| 1.19.8 | ☐ | Cải thiện: cột Mã công nợ có dữ liệu | 1. Mở tab Công nợ 2. Xem cột "Mã công nợ" | Cột Mã công nợ có dữ liệu (#52, #51…), không còn để trống như phiên 0619 |
