# Checklist — Điều phối ca

1. Điều phối ca

1.1 Lịch sử ca

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.1.1 | ☐ | Hiển thị danh sách các ca | 1. Đăng nhập vào hệ thống 2. Truy cập link cashier history 3. Quan sát danh sách các ca hiển thị trên màn hình | Danh sách hiển thị đúng: nhân viên, người mở, mã ca, giờ mở, giờ đóng, tổng tiền mặt |
| 1.1.2 | ☐ | Ca đang mở hiển thị đúng trạng thái | 1. Đăng nhập và vào trang lịch sử ca 2. Quan sát ca đang hoạt động (chưa đóng) trong danh sách 3. Kiểm tra cột giờ đóng của ca đó | Hiện trạng thái "Đang mở" thay vì giờ đóng |
| 1.1.3 | ☐ | Lọc theo Thời gian (khoảng ngày) | 1. Vào trang lịch sử ca 2. Bấm vào bộ lọc thời gian 3. Chọn khoảng ngày cụ thể (VD: từ 01/06 đến 05/06) 4. Bấm xác nhận/áp lọc 5. Quan sát danh sách kết quả | Chỉ hiện các ca nằm trong khoảng ngày đã chọn |
| 1.1.4 | ☐ | Lọc theo Nhân viên | 1. Vào trang lịch sử ca 2. Bấm vào bộ lọc nhân viên 3. Chọn một nhân viên cụ thể từ dropdown 4. Quan sát danh sách kết quả | Chỉ hiện các ca của nhân viên đã chọn |
| 1.1.5 | ☐ | Bấm vào 1 ca để xem chi tiết | 1. Vào trang lịch sử ca 2. Bấm vào một dòng ca bất kỳ trong danh sách 3. Quan sát panel bên phải màn hình | Hiện chi tiết của ca vừa chọn ở panel bên phải |
| 1.1.6 | ☐ | Nút "In phiếu" của ca | 1. Vào trang lịch sử ca, bấm vào một ca để hiện chi tiết 2. Tìm nút "In phiếu" ở panel chi tiết bên phải 3. Bấm nút "In phiếu" 4. Quan sát kết quả | Kích hoạt lệnh in phiếu kết ca |
| 1.1.7 | ☐ | Nút "Chi tiết ca" | 1. Vào trang lịch sử ca, bấm vào một ca để hiện chi tiết 2. Tìm và bấm nút "Chi tiết ca" ở panel bên phải 3. Quan sát màn hình | Mở modal chi tiết ca |
| 1.1.8 | ☐ | Nút "Mở màn hình phụ" | 1. Vào trang lịch sử ca, bấm vào ca đang mở để hiện chi tiết 2. Tìm và bấm nút "Mở màn hình phụ" ở panel bên phải 3. Quan sát kết quả | Mở màn hình phụ của ca đang mở |

---

1.2 Thông tin ca & đóng ca

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.2.1 | ☐ | Hiển thị header ca đúng thông tin | 1. Vào trang lịch sử ca 2. Bấm vào một ca để mở chi tiết ở panel bên phải 3. Quan sát phần header (tiêu đề) của panel chi tiết | Hiển thị đúng ngày giờ, tên nhân viên, trạng thái ca |
| 1.2.2 | ☐ | Hiển thị Tiền mặt đầu ca | 1. Mở chi tiết một ca bất kỳ 2. Tìm mục "Tiền mặt đầu ca" trong panel chi tiết 3. So sánh với số tiền nhân viên đã khai báo lúc mở ca | Hiển thị đúng số tiền mặt đã khai báo khi mở ca |
| 1.2.3 | ☐ | Nút "Đóng ca" | 1. Mở chi tiết của ca đang ở trạng thái "Đang mở" 2. Tìm và bấm nút "Đóng ca" 3. Xác nhận thao tác nếu có hộp thoại xác nhận 4. Quan sát trạng thái ca sau khi đóng | Ca chuyển sang trạng thái đóng, giờ đóng được ghi nhận chính xác |
| 1.2.4 | ☐ | Nút "Đóng và in phiếu" | 1. Mở chi tiết của ca đang ở trạng thái "Đang mở" 2. Tìm và bấm nút "Đóng và in phiếu" 3. Xác nhận nếu có hộp thoại 4. Quan sát kết quả | Ca bị đóng đồng thời in phiếu kết ca |
| 1.2.5 | ☐ | Ca đã đóng không cho thao tác lại | 1. Bấm vào một ca đã có giờ đóng (trạng thái đã đóng) 2. Quan sát panel chi tiết bên phải 3. Kiểm tra xem nút "Đóng ca" / "Đóng và in phiếu" có hiển thị hay không | Không hiển thị nút đóng ca; không thể thực hiện thao tác đóng lại ca đã đóng |

---

1.3 Thẻ tổng hợp (Bán hàng / Trả hàng / Phiếu thu / Phiếu chi)

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.3.1 | ☐ | Thẻ Bán hàng hiển thị đúng | 1. Mở chi tiết một ca bất kỳ 2. Tìm thẻ "Bán hàng" trong phần tổng hợp 3. Quan sát số đơn hàng và tổng tiền mặt bán hàng | Hiển thị đúng số đơn hàng và tổng tiền mặt bán hàng |
| 1.3.2 | ☐ | Thẻ Trả hàng hiển thị đúng | 1. Mở chi tiết một ca có phát sinh trả hàng 2. Tìm thẻ "Trả hàng" trong phần tổng hợp 3. Kiểm tra số tiền hiển thị | Hiển thị đúng tổng tiền trả hàng trong ca |
| 1.3.3 | ☐ | Thẻ Phiếu thu hiển thị đúng | 1. Mở chi tiết một ca có phát sinh phiếu thu 2. Tìm thẻ "Phiếu thu" trong phần tổng hợp 3. Kiểm tra số tiền hiển thị | Hiển thị đúng tổng tiền thu trong ca |
| 1.3.4 | ☐ | Thẻ Phiếu chi hiển thị đúng | 1. Mở chi tiết một ca có phát sinh phiếu chi 2. Tìm thẻ "Phiếu chi" trong phần tổng hợp 3. Kiểm tra số tiền hiển thị | Hiển thị đúng tổng tiền chi trong ca |
| 1.3.5 | ☐ | Bấm "..." trên thẻ để xem chi tiết phương thức | 1. Mở chi tiết một ca 2. Trên bất kỳ thẻ tổng hợp nào (VD: Bán hàng), bấm nút "..." 3. Quan sát thông tin hiện ra | Hiện chi tiết phân theo từng phương thức: tiền mặt / chuyển khoản / quẹt thẻ / QR / khác |
| 1.3.6 | ☐ | Tổng các phương thức khớp với tổng thẻ | 1. Mở chi tiết thẻ bằng cách bấm "..." 2. Cộng tay các giá trị từng phương thức (tiền mặt + CK + thẻ + QR + khác) 3. So sánh với số tổng hiển thị trên thẻ | Tổng các phương thức = tổng hiển thị trên thẻ |

---

1.4 Giao dịch trong ca

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.4.1 | ☐ | Hiển thị danh sách giao dịch | 1. Mở chi tiết một ca 2. Tìm tab hoặc mục "Giao dịch" trong panel chi tiết 3. Quan sát danh sách giao dịch | Hiển thị đúng các cột: STT, mã chứng từ, loại, số tiền, phương thức, trạng thái |
| 1.4.2 | ☐ | Đếm đúng tổng số giao dịch | 1. Mở danh sách giao dịch của một ca 2. Đếm thủ công số dòng giao dịch hiển thị 3. So sánh với số tổng hiển thị trên giao diện | Số tổng giao dịch khớp với số dòng thực tế |
| 1.4.3 | ☐ | Lọc loại: Phiếu bán hàng | 1. Trong danh sách giao dịch, tìm dropdown hoặc tab lọc loại 2. Chọn "Phiếu bán hàng" 3. Quan sát kết quả lọc | Chỉ hiện các phiếu bán hàng |
| 1.4.4 | ☐ | Lọc loại: Phiếu trả hàng | 1. Trong danh sách giao dịch, bấm vào bộ lọc loại 2. Chọn "Phiếu trả hàng" 3. Quan sát kết quả lọc | Chỉ hiện các phiếu trả hàng |
| 1.4.5 | ☐ | Lọc loại: Phiếu thu | 1. Trong danh sách giao dịch, bấm vào bộ lọc loại 2. Chọn "Phiếu thu" 3. Quan sát kết quả lọc | Chỉ hiện các phiếu thu |
| 1.4.6 | ☐ | Lọc loại: Phiếu chi | 1. Trong danh sách giao dịch, bấm vào bộ lọc loại 2. Chọn "Phiếu chi" 3. Quan sát kết quả lọc | Chỉ hiện các phiếu chi |
| 1.4.7 | ☐ | Lọc loại: Tất cả | 1. Trong danh sách giao dịch, bấm vào bộ lọc loại 2. Chọn "Tất cả" 3. Quan sát kết quả lọc | Hiển thị mọi loại giao dịch |
| 1.4.8 | ☐ | Lọc trạng thái "Hoàn thành" | 1. Trong danh sách giao dịch, tìm bộ lọc trạng thái 2. Chọn "Hoàn thành" 3. Quan sát kết quả | Chỉ hiện các giao dịch đã hoàn thành |
| 1.4.9 | ☐ | Lọc trạng thái "Đã hủy" | 1. Trong danh sách giao dịch, tìm bộ lọc trạng thái 2. Chọn "Đã hủy" 3. Quan sát kết quả | Chỉ hiện các giao dịch đã hủy |
| 1.4.10 | ☐ | Tìm theo mã / chú thích | 1. Trong danh sách giao dịch, tìm ô tìm kiếm 2. Nhập mã chứng từ hoặc từ khóa trong chú thích 3. Quan sát kết quả tìm kiếm | Trả về đúng giao dịch khớp với từ khóa |

---

1.5 Đối soát ca (logic tính)

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.5.1 | ☐ | Tổng tiền mặt trong ca tính đúng công thức | 1. Mở chi tiết một ca đã có đủ các loại giao dịch 2. Ghi lại: tiền mặt bán hàng, tiền mặt phiếu thu, tiền mặt trả hàng, tiền mặt phiếu chi 3. Tính tay: (tiền mặt bán hàng + phiếu thu) − (trả hàng + phiếu chi) 4. So sánh với "Tổng tiền mặt trong ca" hiển thị | Tổng tiền mặt trong ca = tiền mặt bán hàng + phiếu thu − trả hàng − phiếu chi |
| 1.5.2 | ☐ | Tiền mặt đầu ca KHÔNG cộng vào tổng | 1. Mở chi tiết một ca 2. Ghi nhận số "Tiền mặt đầu ca" 3. Tính tổng tiền mặt trong ca theo công thức (không cộng đầu ca) 4. So sánh với con số "Tổng tiền mặt trong ca" hiển thị | Tiền mặt đầu ca không được cộng vào "Tổng tiền mặt trong ca" |
| 1.5.3 | ☐ | Chỉ tính giao dịch tiền mặt vào tổng | 1. Mở chi tiết ca có giao dịch bằng nhiều phương thức (tiền mặt + CK + QR) 2. Quan sát "Tổng tiền mặt trong ca" 3. Kiểm tra xem các giao dịch CK / thẻ / QR có được cộng vào không | Chỉ các giao dịch tiền mặt được tính; CK, thẻ, QR không ảnh hưởng tổng tiền mặt trong ca |
| 1.5.4 | ☐ | Phiếu bán hàng ghi nhận vào ca | 1. Tạo và hoàn tất một đơn bán hàng trong ca đang mở 2. Quay lại trang lịch sử ca, mở chi tiết ca đang mở 3. Kiểm tra danh sách giao dịch | Đơn bán vừa tạo xuất hiện trong danh sách giao dịch ca |
| 1.5.5 | ☐ | Phiếu trả hàng làm giảm tổng đúng | 1. Tạo phiếu trả hàng tiền mặt trong ca đang mở 2. Ghi lại tổng tiền mặt trong ca trước và sau khi tạo phiếu trả 3. So sánh chênh lệch với số tiền trả | Tổng tiền mặt trong ca giảm đúng bằng số tiền trả hàng |
| 1.5.6 | ☐ | Phiếu thu cộng vào ca đúng | 1. Tạo phiếu thu tiền mặt trong ca đang mở 2. Ghi lại tổng tiền mặt trong ca trước và sau khi tạo phiếu thu 3. So sánh chênh lệch với số tiền thu | Tổng tiền mặt trong ca tăng đúng bằng số tiền thu |
| 1.5.7 | ☐ | Phiếu chi trừ khỏi ca đúng | 1. Tạo phiếu chi tiền mặt trong ca đang mở 2. Ghi lại tổng tiền mặt trong ca trước và sau khi tạo phiếu chi 3. So sánh chênh lệch với số tiền chi | Tổng tiền mặt trong ca giảm đúng bằng số tiền chi |
| 1.5.8 | ☐ | Giao dịch đã hủy không tính vào tổng | 1. Trong danh sách giao dịch ca, lọc trạng thái "Đã hủy" để xác định giao dịch bị hủy 2. Lọc trạng thái "Hoàn thành", tính tay tổng tiền các giao dịch hoàn thành 3. So sánh với "Tổng tiền mặt trong ca" hiển thị | Tổng tiền chỉ tính giao dịch hoàn thành; giao dịch đã hủy không được cộng vào |

---

1.6 Chi tiết ca (modal)

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.6.1 | ☐ | Mở modal Chi tiết ca | 1. Mở chi tiết một ca ở panel bên phải 2. Bấm nút "Chi tiết ca" 3. Quan sát modal hiện ra | Modal mở ra, hiển thị đúng mã ca, ngày giờ, tên nhân viên |
| 1.6.2 | ☐ | Bảng Thu/Chi theo phương thức trong modal | 1. Mở modal Chi tiết ca 2. Quan sát bảng Thu/Chi được phân theo từng phương thức thanh toán 3. So sánh số liệu với các thẻ tổng hợp ở panel chính | Số liệu trong modal khớp với số liệu trên các thẻ tổng hợp |
| 1.6.3 | ☐ | Tổng tiền mặt trong ca (modal) khớp panel chính | 1. Ghi nhận số "Tổng tiền mặt trong ca" hiển thị tại panel chi tiết chính 2. Mở modal Chi tiết ca 3. Tìm và ghi nhận số "Tổng tiền mặt trong ca" trong modal 4. So sánh hai con số | Giá trị tổng tiền mặt trong modal khớp với panel chính |
| 1.6.4 | ☐ | Bấm "Đóng" để thoát modal | 1. Mở modal Chi tiết ca 2. Bấm nút "Đóng" 3. Quan sát màn hình | Modal đóng lại, quay về panel chi tiết ca bên phải |
