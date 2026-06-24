# Checklist — Điều phối ca

## Ghi chú UI thực tế (cập nhật từ phiên khám phá 0623, phiên bản 1.0.0+67)
> - **Route thực tế:** `#/pos-shell-route/pos-shift-route`. Tên menu trên thanh điều hướng: **"Điều phối ca"**.
> - **Cột trái:** hộp **"CA HIỆN TẠI"** (badge **"Đang hoạt động"**) ở trên; phần **"LỊCH SỬ CA"** ở dưới gồm bộ lọc **Thời gian** + **Nhân viên** và danh sách thẻ ca (dạng **thẻ**, không phải bảng).
> - **Panel phải:** header ca (ngày giờ · Nhân viên · trạng thái) + nút thao tác; dòng **"Tiền mặt đầu ca"**; **4 thẻ tổng hợp** (Bán hàng / Trả hàng / Phiếu thu / Phiếu chi) — chi tiết phương thức (Tiền mặt / Chuyển khoản / Quẹt thẻ / QR tự động) **hiển thị sẵn trên thẻ, KHÔNG có nút "..."**; dòng **"Tổng tiền mặt trong ca"**; khối **"Giao dịch trong ca"**.
> - **Nút theo trạng thái ca:** ca đang mở → **"Đóng ca"** + **"Đóng và in phiếu"**; ca đã đóng → chỉ **"In phiếu ca"** (+ "Chi tiết ca").
> - **Bộ lọc giao dịch:** dropdown **Loại** (Tất cả / Phiếu bán hàng / Phiếu trả hàng / Phiếu thu / Phiếu chi) · ô tìm **"Tìm mã, chú thích"** · 2 checkbox độc lập **"Hoàn thành"** + **"Đã hủy"**.
> - **Cột bảng giao dịch:** STT · Mã voucher · Loại giao dịch · Số tiền · Thanh toán · Trạng thái.
> - **Quy ước mã:** Phiếu bán hàng **POS…**, Phiếu thu **PC…**, Phiếu chi **PT…**, ca **SCR…**; tất cả gắn hậu tố chi nhánh (VD **CN2**).
> - **Công thức quỹ:** *Tổng tiền mặt trong ca = Tiền mặt (Phiếu thu) − Tiền mặt (Phiếu chi) *; tiền mặt bán hàng được gộp tự động vào Phiếu thu. **Tiền mặt đầu ca KHÔNG cộng vào tổng.**
> - **Menu ☰ (góc phải):** CN1 · Thu ngân · Bật âm thanh · Tải lại cấu hình · Đặt máy chạy printcenter · Hiện thông tin device_id · Ngôn ngữ. (**Không** có "Mở màn hình phụ".)


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

---

1.7 Bộ lọc Thời gian (Lịch sử ca)

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.7.1 | ☐ | Giá trị mặc định bộ lọc thời gian | 1. Vào Điều phối ca 2. Quan sát ô "Thời gian" trong LỊCH SỬ CA khi vừa tải | Mặc định là khoảng ~7 ngày gần nhất tính đến hôm nay (VD "16-06-2026 - 23-06-2026") |
| 1.7.2 | ☐ | Preset "Hôm nay" | 1. Bấm ô Thời gian mở dropdown lịch 2. Chọn nhanh "Hôm nay" 3. Quan sát danh sách ca | Chỉ hiện ca mở trong ngày hôm nay; ngoài ngày bị loại |
| 1.7.3 | ☐ | Preset "Hôm qua" | 1. Mở dropdown Thời gian 2. Chọn "Hôm qua" 3. Quan sát | Chỉ hiện ca thuộc ngày hôm qua |
| 1.7.4 | ☐ | Preset "Tuần này" | 1. Mở dropdown Thời gian 2. Chọn "Tuần này" 3. Quan sát | Chỉ hiện ca trong tuần hiện tại |
| 1.7.5 | ☐ | Preset "Tháng này" | 1. Mở dropdown Thời gian 2. Chọn "Tháng này" 3. Quan sát | Chỉ hiện ca trong tháng hiện tại |
| 1.7.6 | ☐ | Preset "Quý này" | 1. Mở dropdown Thời gian 2. Chọn "Quý này" 3. Quan sát | Chỉ hiện ca trong quý hiện tại |
| 1.7.7 | ☐ | Preset "Năm nay" | 1. Mở dropdown Thời gian 2. Chọn "Năm nay" 3. Quan sát | Chỉ hiện ca trong năm hiện tại |
| 1.7.8 | ☐ | Chọn khoảng ngày tùy chỉnh | 1. Mở dropdown Thời gian 2. Chọn ngày bắt đầu và ngày kết thúc cụ thể (VD 09/06 → 15/06) 3. Áp dụng 4. Quan sát danh sách | Chỉ hiện ca có giờ mở nằm trong khoảng đã chọn (VD SCR96/95/94) |
| 1.7.9 | ☐ | Ngày bắt đầu > ngày kết thúc (biên) | 1. Mở lịch, chọn ngày bắt đầu muộn hơn ngày kết thúc 2. Quan sát phản hồi | Hệ thống chặn/đảo ngược hợp lý hoặc báo lỗi; không treo giao diện |
| 1.7.10 | ☐ | Khoảng ngày không có ca | 1. Chọn khoảng ngày chắc chắn không phát sinh ca 2. Quan sát danh sách | Hiện "Không có dữ liệu lịch sử"/empty state, không vỡ giao diện |
| 1.7.11 | ☐ | Lọc thời gian không ảnh hưởng CA HIỆN TẠI | 1. Ghi nhận hộp "CA HIỆN TẠI" 2. Đổi bộ lọc Thời gian sang khoảng không chứa ca đang mở 3. Quan sát hộp CA HIỆN TẠI | Hộp CA HIỆN TẠI vẫn hiển thị ca đang mở (độc lập với bộ lọc lịch sử) |

---

1.8 Bộ lọc Nhân viên (Lịch sử ca)

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.8.1 | ☐ | Danh sách nhân viên đầy đủ | 1. Bấm dropdown "Nhân viên" trong LỊCH SỬ CA 2. Liệt kê các lựa chọn | Hiển thị: Tất cả, Admin master, tran van a, tranvanc, tranvantest, cashier (theo cấu hình store) |
| 1.8.2 | ☐ | Chọn "Tất cả" | 1. Mở dropdown Nhân viên 2. Chọn "Tất cả" 3. Quan sát danh sách | Hiện ca của mọi nhân viên trong khoảng thời gian đang lọc |
| 1.8.3 | ☐ | Chọn 1 nhân viên cụ thể | 1. Mở dropdown Nhân viên 2. Chọn "cashier" 3. Quan sát danh sách | Chỉ hiện ca có Nhân viên = cashier |
| 1.8.4 | ☐ | Lọc theo trường "Nhân viên" của ca (không phải Người mở) | 1. Chọn một NV mà ca do người khác mở 2. Quan sát ca trả về | Lọc theo trường "Nhân viên" của ca; ca SCR97 (NV cashier, người mở cashier) khác ca có người mở Admin master |
| 1.8.5 | ☐ | Kết hợp Thời gian + Nhân viên | 1. Đặt Thời gian = khoảng 09–15/06 2. Chọn Nhân viên = "Admin master" 3. Quan sát | Chỉ hiện ca thỏa cả hai điều kiện; nếu không có → "Không có dữ liệu lịch sử" |
| 1.8.6 | ☐ | Nhân viên không có ca trong khoảng | 1. Chọn NV + khoảng ngày không có ca của NV đó 2. Quan sát | Danh sách rỗng, hiển thị empty state |

---

1.9 Hộp "CA HIỆN TẠI"

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.9.1 | ☐ | Hiển thị đủ thông tin ca đang mở | 1. Vào Điều phối ca 2. Quan sát hộp "CA HIỆN TẠI" góc trên trái | Hiện: Mã ca (SCR…), Nhân viên, Người mở, Giờ vào ca, Tiền mặt đầu ca, badge "Đang hoạt động" |
| 1.9.2 | ☐ | Bấm hộp CA HIỆN TẠI mở chi tiết | 1. Bấm vào hộp "CA HIỆN TẠI" 2. Quan sát panel bên phải | Panel phải nạp chi tiết đúng ca đang mở (header "Đang hoạt động" + 4 thẻ + giao dịch) |
| 1.9.3 | ☐ | Badge trạng thái "Đang hoạt động" | 1. Quan sát badge ở hộp CA HIỆN TẠI và header panel | Badge "Đang hoạt động" màu xanh, thống nhất giữa hộp và panel |
| 1.9.4 | ☐ | Tiền mặt đầu ca khớp lúc mở ca | 1. Đọc "Tiền mặt đầu ca" ở hộp CA HIỆN TẠI 2. So với số khai báo khi mở ca | Hiển thị đúng số tiền mặt đầu ca đã khai báo (VD 0 đ) |
| 1.9.5 | ☐ | Không có ca đang mở | 1. (Khi tài khoản chưa mở ca / sau khi đóng) quan sát hộp CA HIỆN TẠI | Hiển thị trạng thái rỗng phù hợp (VD "Chưa mở ca"), không vỡ giao diện |

---

1.10 In phiếu ca

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.10.1 | ☐ | Nút "In phiếu ca" trên panel ca đã đóng | 1. Mở chi tiết một ca đã đóng 2. Tìm nút "In phiếu ca" ở góc phải header panel | Nút "In phiếu ca" hiển thị & enabled |
| 1.10.2 | ☐ | Nút "In phiếu" trên thẻ ca (lịch sử) | 1. Quan sát thẻ ca đã đóng trong LỊCH SỬ CA 2. Tìm nút "In phiếu" trên thẻ | Nút "In phiếu" có trên thẻ ca |
| 1.10.3 | ☐ | Kích hoạt lệnh in | 1. Bấm "In phiếu ca" 2. Quan sát phản hồi | Kích hoạt lệnh in/print preview (hoặc gửi printcenter), không lỗi |
| 1.10.4 | ☐ | Nội dung phiếu in khớp số liệu ca | 1. Mở print preview 2. Đối chiếu mã ca, NV, tổng tiền mặt, tổng thu/chi với panel | Số liệu trên phiếu in khớp panel chi tiết ca |

---

1.11 Phân biệt ca đang mở vs ca đã đóng

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.11.1 | ☐ | Ca đang mở: nút đóng ca có sẵn | 1. Mở chi tiết ca đang hoạt động 2. Quan sát góc phải header panel | Hiện "Đóng ca" + "Đóng và in phiếu"; header badge "Đang hoạt động"; không có giờ đóng |
| 1.11.2 | ☐ | Ca đã đóng: chỉ có nút in | 1. Mở chi tiết ca đã đóng 2. Quan sát góc phải header panel | Chỉ hiện "In phiếu ca" (+ "Chi tiết ca"); KHÔNG có "Đóng ca"/"Đóng và in phiếu" |
| 1.11.3 | ☐ | Chỉ 1 ca đang mở tại một thời điểm | 1. Quan sát hộp CA HIỆN TẠI và danh sách lịch sử | Chỉ một ca ở trạng thái "Đang hoạt động"; các ca còn lại đều đã đóng |
| 1.11.4 | ☐ | Ca đã đóng hiển thị người đóng + giờ đóng | 1. Mở chi tiết/Chi tiết ca của ca đã đóng 2. Tìm "Người đóng", "Giờ đóng ca" | Hiển thị đúng người đóng và thời điểm đóng ca |
| 1.11.5 | ☐ | Không đóng lại được ca đã đóng | 1. Mở ca đã đóng 2. Tìm thao tác đóng ca | Không có nút đóng ca; không thể thực hiện đóng lại |

---

1.12 Đồng bộ thời gian thực với bán hàng (Trang chủ → Điều phối ca)

> **Lưu ý chung cho mục 1.12:**
> - **Luồng tạo đơn bán hàng:** Trang chủ → chọn bàn → thêm sản phẩm → bấm "Thanh toán" → chọn PTTT, nhập số tiền khách đưa → xác nhận.
> - **Phiếu bán hàng (POS…)** = tổng tiền đơn hàng (giá trị toàn bộ đơn).
> - **Phiếu thu khi bán hàng (PC…)** = số tiền khách thực trả.
> - Nếu khách trả **đủ**: PC… = POS…; nếu trả **thiếu**: PC… < POS…, phần còn lại (POS… − PC…) hệ thống tự ghi công nợ.
> - **Tổng tiền mặt trong ca** tính theo Phiếu thu (PC…), **không phải** Phiếu bán hàng (POS…).

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.12.1 | ☐ | Phiếu bán hàng (POS…) và Phiếu thu (PC…) xuất hiện trong giao dịch ca | 1. Truy cập Trang chủ, chọn một bàn bất kỳ 2. Thêm ≥ 1 sản phẩm vào đơn 3. Bấm "Thanh toán", chọn PTTT Tiền mặt, nhập số tiền khách đưa ≥ tổng đơn, xác nhận 4. Ghi nhận mã POS… và PC… sinh ra 5. Quay lại Điều phối ca → chọn ca đang mở → xem "Giao dịch trong ca" | Danh sách giao dịch hiển thị: Phiếu bán hàng POS… (= tổng tiền đơn) và Phiếu thu PC… (= số tiền khách đã trả), đều gắn đúng ca đang mở |
| 1.12.2 | ☐ | Tổng tiền mặt trong ca cập nhật theo Phiếu thu, không theo Phiếu bán hàng | 1. Ghi nhận "Tổng tiền mặt trong ca" hiện tại (= T) 2. Trang chủ → chọn bàn → tạo đơn, ghi tổng tiền đơn = X 3. Bấm "Thanh toán", chọn PTTT Tiền mặt, nhập đúng đủ X, xác nhận 4. Quay lại Điều phối ca → mở ca đang mở → đọc "Tổng tiền mặt trong ca" | Tổng tiền mặt trong ca = T + X; Phiếu thu PC… = X; Phiếu bán hàng POS… = X (khớp nhau khi khách trả đủ) |
| 1.12.3 | ☐ | Phiếu bán hàng ≠ Phiếu thu khi khách trả thiếu (công nợ) | 1. Trang chủ → chọn bàn → tạo đơn, ghi tổng tiền đơn = X 2. Bấm "Thanh toán", nhập số tiền khách đưa = Y (Y < X), xác nhận; hệ thống tự ghi phần còn lại (X − Y) là công nợ 3. Ghi nhận mã POS… và PC… sinh ra 4. Quay lại Điều phối ca → xem giao dịch ca → đọc giá trị từng phiếu | POS… = X (tổng đơn); PC… = Y (tiền khách đã trả thực tế); Tổng tiền mặt trong ca chỉ tăng Y, không tăng phần công nợ (X − Y) |
| 1.12.4 | ☐ | Thẻ Bán hàng cập nhật đúng số đơn và tổng tiền | 1. Trong Điều phối ca, ghi số "n đơn hàng" và tổng tiền Y trên thẻ Bán hàng 2. Trang chủ → chọn bàn → tạo và hoàn tất 1 đơn giá trị Z 3. Quay lại Điều phối ca → đọc lại thẻ Bán hàng | Số đơn hàng = n + 1; tổng tiền thẻ Bán hàng = Y + Z (= tổng các giá trị POS… trong ca) |
| 1.12.5 | ☐ | Bộ đếm "Tổng cộng (n)" giao dịch cập nhật | 1. Ghi "Tổng cộng n" giao dịch trong ca 2. Trang chủ → chọn bàn → tạo và hoàn tất 1 đơn (khách trả đủ tiền mặt) 3. Quay lại Điều phối ca → đọc lại bộ đếm | Số tổng giao dịch tăng ít nhất +2 (1 POS… + 1 PC… tương ứng) |
| 1.12.6 | ☐ | Reload trang giữ số liệu nhất quán | 1. Sau khi tạo đơn, ghi lại số liệu 4 thẻ + "Tổng tiền mặt trong ca" 2. Tải lại trang (F5), chọn lại ca đang mở 3. So sánh số liệu trước và sau reload | Số liệu sau reload khớp với server; không lệch POS… hay PC… |

---

1.13 Đối chiếu chéo với menu Thu chi

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.13.1 | ☐ | Phiếu thu trong ca khớp menu Thu chi | 1. Trong giao dịch ca, chọn 1 phiếu thu (PC…) ghi mã + số tiền + PTTT 2. Sang menu Thu chi tìm đúng mã 3. So sánh | Mã, số tiền, phương thức khớp nhau giữa Điều phối ca và Thu chi |
| 1.13.2 | ☐ | Phiếu chi trong ca khớp menu Thu chi | 1. Chọn 1 phiếu chi (PT…) trong ca, ghi mã + số tiền 2. Sang Thu chi tìm mã 3. So sánh | Phiếu chi khớp giữa hai màn hình |
| 1.13.3 | ☐ | Logic tiền mặt nhất quán hai màn hình | 1. Ghi "Tổng tiền mặt trong ca" 2. Đối chiếu với thu/chi tiền mặt tương ứng ở Thu chi (cùng kỳ/ca) | Hai bên phản ánh cùng dòng tiền mặt, không mâu thuẫn |

---

1.14 Mã voucher & tìm kiếm

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.14.1 | ☐ | Tiền tố mã theo loại giao dịch | 1. Quan sát cột "Mã voucher" theo từng loại | Phiếu bán hàng **POS…**, Phiếu thu **PC…**, Phiếu chi **PT…** (đúng quy ước) |
| 1.14.2 | ☐ | Mã gắn hậu tố chi nhánh | 1. Đọc mã voucher bất kỳ | Mã có hậu tố chi nhánh (VD …CN2) đúng chi nhánh ca |
| 1.14.3 | ☐ | Tìm theo mã voucher chính xác | 1. Vào ô "Tìm mã, chú thích" 2. Nhập đầy đủ một mã (VD POS15062080CN2) 3. Quan sát | Trả về đúng 1 giao dịch khớp mã |
| 1.14.4 | ☐ | Tìm theo chú thích | 1. Nhập một từ khóa trong phần chú thích/ghi chú 2. Quan sát | Trả về các giao dịch có chú thích khớp |
| 1.14.5 | ☐ | Tìm mã không tồn tại | 1. Nhập chuỗi vô nghĩa (VD "zzz999") 2. Quan sát | Danh sách giao dịch rỗng, hiển thị empty state |
| 1.14.6 | ☐ | Xóa từ khóa khôi phục danh sách | 1. Sau khi tìm, xóa hết ô tìm kiếm 2. Quan sát | Danh sách giao dịch trở lại đầy đủ theo bộ lọc hiện hành |

---

1.15 Định dạng số tiền & hiển thị

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.15.1 | ☐ | Dấu phân cách nghìn + hậu tố đ | 1. Quan sát số tiền trên thẻ và cột "Số tiền" | Hiển thị dạng "1.557.886 đ" (dấu chấm ngăn cách hàng nghìn, hậu tố đ) |
| 1.15.2 | ☐ | Giá trị 0 hiển thị đúng | 1. Tìm thẻ/giao dịch có giá trị 0 (VD Trả hàng) | Hiển thị "0 đ", không để trống hay "null" |
| 1.15.3 | ☐ | Định dạng nhất quán mọi nơi | 1. So định dạng số ở thẻ tổng hợp, dòng "Tổng tiền mặt trong ca", cột Số tiền, modal | Định dạng tiền nhất quán toàn màn hình |
| 1.15.4 | ☐ | Phân biệt màu/loại giao dịch | 1. Quan sát màu nhãn loại (Bán hàng / Phiếu thu / Phiếu chi) và trạng thái | Ghi nhận quy ước màu (VD chi màu đỏ, trạng thái "Đã thanh toán" màu phù hợp) — nhất quán |

---

1.16 Trạng thái rỗng & xử lý lỗi

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.16.1 | ☐ | Chưa chọn ca | 1. Vào Điều phối ca khi panel phải chưa chọn ca 2. Quan sát vùng panel phải | Hiển thị "Chọn một ca để xem chi tiết" |
| 1.16.2 | ☐ | Ca không có giao dịch | 1. Mở một ca không phát sinh giao dịch 2. Quan sát khối "Giao dịch trong ca" | Danh sách giao dịch rỗng + empty state; 4 thẻ về 0 |
| 1.16.3 | ☐ | Lọc loại không có dữ liệu | 1. Trong ca không có trả hàng, lọc loại = "Phiếu trả hàng" 2. Quan sát | Danh sách rỗng (đúng), không báo lỗi |
| 1.16.4 | ☐ | Bỏ cả 2 checkbox trạng thái | 1. Bỏ tích cả "Hoàn thành" và "Đã hủy" 2. Quan sát danh sách | Danh sách rỗng (không trạng thái nào được chọn) hoặc hành vi hợp lý — ghi nhận |
| 1.16.5 | ☐ | Tải lại trang khi đang xem ca | 1. Mở chi tiết một ca 2. Tải lại trang (F5) 3. Quan sát | Giao diện khôi phục bình thường (về panel mặc định "Chọn một ca…" hoặc giữ ca), không vỡ |
| 1.16.6 | ☐ | Kẹt "lớp phủ ma" (Flutter) | 1. Khi dropdown/modal kẹt overlay không thao tác được 2. Tải lại trang 3. Thao tác lại | Sau reload giao diện hoạt động lại bình thường (quirk môi trường Flutter cần lưu ý) |

---

1.17 Phân quyền & phạm vi chi nhánh

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.17.1 | ☐ | Thu ngân thấy đúng phạm vi ca | 1. Đăng nhập vai trò Thu ngân (chi nhánh CN1) 2. Quan sát danh sách ca trong LỊCH SỬ CA | Chỉ hiển thị ca thuộc phạm vi chi nhánh được phép |
| 1.17.2 | ☐ | Mã ca gắn đúng chi nhánh | 1. Đọc mã ca (SCR…CN2) của các ca 2. Đối chiếu chi nhánh hiện hành | Hậu tố chi nhánh trên mã ca khớp chi nhánh đang đăng nhập |
| 1.17.3 | ☐ | Hiển thị ca của nhiều nhân viên | 1. Với tài khoản Admin master, để Nhân viên = "Tất cả" 2. Quan sát | Hiện ca của nhiều nhân viên khác nhau (Admin master, cashier…) |
| 1.17.4 | ☐ | Phân biệt "Nhân viên" và "Người mở" ca | 1. Mở 1 ca có Người mở khác Nhân viên (VD SCR96: NV cashier, người mở Admin master) 2. Quan sát 2 trường | Hai trường hiển thị độc lập, đúng dữ liệu từng ca |

---

1.18 Menu ☰ (cấu hình thiết bị)

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.18.1 | ☐ | Mở menu ☰ | 1. Bấm biểu tượng ☰ góc trên phải 2. Quan sát menu xổ ra | Menu mở, hiển thị danh sách mục cấu hình |
| 1.18.2 | ☐ | Danh sách mục đầy đủ | 1. Đọc các mục trong menu ☰ | Gồm: CN1, Thu ngân, Bật âm thanh, Tải lại cấu hình, Đặt máy chạy printcenter, Hiện thông tin device_id, Ngôn ngữ |
| 1.18.3 | ☐ | "Tải lại cấu hình" | 1. Bấm "Tải lại cấu hình" 2. Quan sát | Hệ thống nạp lại cấu hình, không lỗi |
| 1.18.4 | ☐ | "Hiện thông tin device_id" | 1. Bấm "Hiện thông tin device_id" 2. Quan sát | Hiển thị device_id của thiết bị |
| 1.18.5 | ☐ | Đổi Ngôn ngữ | 1. Bấm "Ngôn ngữ", chọn ngôn ngữ khác 2. Quan sát giao diện | Giao diện đổi ngôn ngữ tương ứng (VI/EN/KO) |
| 1.18.6 | ☐ | Bật âm thanh | 1. Bật/tắt "Bật âm thanh" 2. Quan sát trạng thái | Tùy chọn âm thanh đổi trạng thái, lưu lại |

---

1.19 Kiểm thử biên & hiệu năng

| STT | ✓ | Testcase | Các bước thực hiện | Kết quả mong đợi |
|-----|---|----------|--------------------|------------------|
| 1.19.1 | ☐ | Ca nhiều giao dịch (37+) | 1. Mở ca có nhiều giao dịch (VD "Tổng cộng 37") 2. Cuộn danh sách giao dịch | Cuộn mượt, hiển thị đủ giao dịch, không treo |
| 1.19.2 | ☐ | Đếm "Tổng cộng (n hủy)" khớp số dòng | 1. Đọc "Tổng cộng n (m hủy)" 2. Lọc/đếm số giao dịch hoàn thành và đã hủy 3. So sánh | n = số dòng thực tế; m = số giao dịch "Đã hủy" |
| 1.19.3 | ☐ | Khoảng ngày rất rộng | 1. Đặt Thời gian = "Năm nay" 2. Quan sát danh sách ca | Tải đầy đủ ca trong năm, không lỗi hiệu năng |
| 1.19.4 | ☐ | Chuyển nhanh giữa nhiều ca | 1. Bấm lần lượt nhiều thẻ ca khác nhau liên tục 2. Quan sát panel phải | Panel phải cập nhật đúng chi tiết từng ca, không lẫn số liệu |
| 1.19.5 | ☐ | Đếm tiền mặt kiểm chứng công thức | 1. Mở ca, đọc TM Phiếu thu và TM Phiếu chi 2. Tính TM thu − TM chi 3. So với "Tổng tiền mặt trong ca" | Khớp công thức (VD 1.517.986 − 55.000 = 1.462.986) |

---

