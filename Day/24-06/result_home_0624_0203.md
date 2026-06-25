# Kết quả kiểm thử — HOME

- Menu: home
- Ngày giờ: 24/06 02:03 (UTC)
- Người/agent thực hiện: Claude
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Thu ngân (Casher) — CN1 — ca đang hoạt động
- Trình duyệt: Chrome (qua tiện ích điều khiển) — Browser 2
- Thư mục ảnh lỗi: `screenshot/0624_0203_home/`

## Ghi chú chung về môi trường kiểm thử
- App nền **Flutter web (canvas)**. Công cụ tự động của phiên **không lưu được ảnh ra đĩa** (đã xác nhận lại trong phiên này — `save_to_disk` không có tác dụng), nên các quan sát/lỗi được mô tả chi tiết bằng chữ kèm số liệu thực tế (giống các phiên trước).
- **Đặc điểm tương tác tự động (rất quan trọng):** các thao tác *thay đổi tại chỗ* (bộ lọc trạng thái, ô tìm món, chọn món trong lưới, nút +/- số lượng, chọn thuộc tính trong modal, nhập ghi chú) phản hồi **ổn định**. Ngược lại, các thao tác *mở/đóng overlay hoặc điều hướng* (nút chọn vai trò "Thu ngân", bấm vào **thẻ bàn**, các **dropdown thanh công cụ** "số cột/giao diện/chế độ xem", **mục trong menu "..."**, nút **đóng modal**) phản hồi **chập chờn** — thường chỉ ăn hover, phải bấm lại nhiều lần hoặc đợi mới ăn.
- App **xuống cấp dần** sau ~15 thao tác: renderer **đơ/giật nặng** (chụp màn hình time-out), click ngừng phản hồi, **buộc phải tải lại trang** (reload) để khôi phục. Trong phiên đã reload **2 lần**. Đây chính là biểu hiện cần ghi nhận ở mục **1.20.2**.
- Các bộ lọc trạng thái ở Trang chủ là **toggle đa lựa chọn (cộng dồn)**, không phải radio. Số đếm trong ngoặc của các tab trạng thái là **toàn cục** (không đổi theo khu).
- Số liệu Trang chủ khi vào: **Tất cả (15)**, Bàn trống (8), Đang sử dụng (6), Chờ xác nhận (0), Chờ thanh toán (0).

---

## 1.1 Sơ đồ bàn

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.1.1 | Hiển thị danh sách bàn theo khu | PASS | Hiện đủ bàn; "Tất cả (15)", có thẻ "BÀN MANG VỀ" (mang về) đầu danh sách |
| 1.1.2 | Lọc "Bàn trống" | PASS | Bật riêng → đúng **8** bàn trống (teal): BAN2, BAN1, BAN2, BAN KIEM TRA TEN DAI, BAN_QR, BAN4, BAN8, BAN10. Số đếm khớp |
| 1.1.3 | Lọc "Đang sử dụng" | PASS | Bật riêng → đúng **6** bàn (vàng): BAN1, BAN3, BAN5, BAN6, BAN7, BAN9. Số đếm khớp |
| 1.1.4 | Lọc "Chờ xác nhận" | PASS | (0) — empty state "Danh sách bàn thuộc trạng thái 'Chờ xác nhận' rỗng" + nút Tất cả |
| 1.1.5a | Lọc "Chờ thanh toán" | PASS | (0) — empty state "...'Chờ thanh toán' rỗng" đúng |
| 1.1.5b | Lọc theo khu (khu 1 / khu 2) | PASS | Dropdown có **Tất cả / khu 1 / khu 2**. Chọn khu 1 → chỉ hiện bàn khu 1 (thẻ "BÀN MANG VỀ" biến mất) |
| 1.1.6 | Đổi số cột hiển thị | KHÔNG KIỂM THỬ | Dropdown "5 cột" có hiển thị nhưng **không mở được** bằng click tự động (lỗi tương tác Flutter) |
| 1.1.7 | Đổi giao diện (1/2/3) | KHÔNG KIỂM THỬ | Dropdown "Giao diện 1" có hiển thị, không mở được bằng click tự động |
| 1.1.8 | Thẻ bàn hiển thị thông tin | PASS | Đủ: tên bàn, timer, icon hóa đơn + số, icon khách + số, tổng tiền, nhãn trạng thái (màu) |
| 1.1.9 | Tổng tiền trên thẻ bàn | PASS | Thẻ BAN1 = 500.000 = "Tổng tiền hàng" trong Order (chưa gồm thuế/phụ thu). Sau khi thêm món, thẻ cập nhật 540.000 = tổng tiền hàng mới |
| 1.1.10 | Trạng thái "Chưa báo bếp" | PASS (một phần) | Món mới thêm hiển thị "Chờ báo bếp"; thẻ bàn có nhãn trạng thái tương ứng |
| 1.1.11 | Nút "Xác nhận" trên thẻ | N/A | Không có đơn "Chờ xác nhận" (0) |
| 1.1.12 | Bấm vào bàn | PASS | Bấm thẻ bàn → mở màn hình Order (cần app ở trạng thái còn phản hồi; lúc đơ thì không mở được) |
| 1.1.13 | Thêm đơn mang về | KHÔNG KIỂM THỬ | Chưa bấm thẻ "BÀN MANG VỀ" trong phiên này |
| 1.1.14 | Số liệu các tab nhất quán | PASS | 8 (trống) + 6 (đang dùng) + 0 + 0 = **14**; "Tất cả" = **15**. Chênh +1 = thẻ "BÀN MANG VỀ" (đúng quy ước 1.1.18) |
| 1.1.15 | Đổi chế độ xem "Danh sách"/"Sơ đồ" | KHÔNG KIỂM THỬ | Dropdown "Danh sách" có hiển thị, không mở được bằng click tự động |
| 1.1.16 | Bộ lọc trạng thái cộng dồn | PASS | Bật "Bàn trống" + "Đang sử dụng" → hiện **hợp (union)** cả 2 loại (14 bàn). Tắt bớt 1 filter → danh sách thu lại đúng. Là toggle cộng dồn, KHÔNG phải radio |
| 1.1.17 | Số đếm tab trạng thái là toàn cục | PASS | Đổi khu "Tất cả" → "khu 1": số đếm tab (15/8/6/0/0) **KHÔNG đổi**; chỉ lưới bàn lọc theo khu |
| 1.1.18 | Thẻ "Bàn mang về" tính vào "Tất cả" | PASS | "BÀN MANG VỀ" được tính vào "Tất cả" nhưng không thuộc nhóm trạng thái → "Tất cả" (15) lớn hơn tổng các tab (14) đúng 1 đơn vị |

## 1.2 Menu (Thực đơn)

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.2.1 | Hiển thị danh mục món | PASS | Đủ tab: Tất cả, Bán chạy, Món mới, Nước ngọt, Nước chế biến, Nước có còn, Món nước, Món xào, Lẩu, test máy in, banh v1, Test in pc |
| 1.2.2 | Lọc theo danh mục | PASS | Chọn "Nước ngọt" → danh sách đổi (VD "Món chế biến" biến mất khỏi lưới) |
| 1.2.3 | Tìm món (F1) | PASS | Gõ "tra" → lọc đúng các món chứa "tra" |
| 1.2.4 | Ẩn/hiện hình ảnh món | KHÔNG KIỂM THỬ | Toggle "Hiện ảnh" có hiển thị (đang tắt → lưới chỉ tên + giá); chưa bật/tắt được trong phiên |
| 1.2.5 | Đổi số cột hiển thị món | KHÔNG KIỂM THỬ | Dropdown "4 cột" có; chưa đổi |
| 1.2.6 | Phân trang (1/5…) | N/A | Lưới món cuộn liên tục, không có chỉ số phân trang (giống phiên trước) |
| 1.2.7 | Giá món | PASS | Đúng định dạng VND: 555.000đ, 550.000đ, 10.000đ, 9.000đ, 999.999đ, 30.000đ… |
| 1.2.8 | Phạm vi tìm món theo danh mục | KHÔNG KIỂM THỬ | Chưa thử tìm trong 1 danh mục cụ thể |
| 1.2.9 | Tìm món không phân biệt dấu | PASS | Gõ không dấu "tra" → ra cả **"Trà A hỷ"** (có dấu) lẫn **"tran chau"** (không dấu), kiemtra, Nuoc trai cay… |

## 1.3 Modal tùy chọn món

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.3.1 | Mở modal khi món có tùy chọn | PASS | Bấm "Cơm" → modal "Chọn món kèm theo" (Size, Ngọt, số lượng, ghi chú) |
| 1.3.2 | Chọn thuộc tính (Size, độ ngọt) | PASS | Size S/M/LL; Ngọt Đường 100/50/20%. Chọn M + Đường 50% ok. *Tất cả +0đ → không có phụ thu để đối chiếu giá* |
| 1.3.3 | Chọn món thêm | KHÔNG KIỂM THỬ | "Cơm" chỉ có thuộc tính (Size/Ngọt), không có nhóm "Món thêm" |
| 1.3.4 | Tăng/giảm số lượng | PASS | Bấm + → SL 1→2; nút cập nhật "Thêm vào giỏ hàng - 20.000đ" → **40.000đ** |
| 1.3.5 | Nhập ghi chú | PASS | Nhập "ít cay @#1" (tiếng Việt có dấu + ký tự đặc biệt) ok |
| 1.3.6 | Bấm "Thêm vào giỏ hàng" | PASS | Cơm (M, Đường 50%, SL2) thêm vào hóa đơn |
| 1.3.7 | Bấm "Đóng" | KHÔNG KIỂM THỬ | Chưa thử đóng modal khi không chọn gì |
| 1.3.8 | Tùy chọn hiển thị trong dòng món | PASS | Dòng Cơm hiện "M", "Đường 50%", "Ghi chú: ít cay @#1" |

## 1.4 Hóa đơn / Giỏ hàng

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.4.1 | Thêm món vào hóa đơn | PASS | Thêm Cơm → dòng xuất hiện, "Tổng tiền hàng (1)"→"(2)" |
| 1.4.2 | Tăng số lượng (+) | PASS | Cơm SL 2→3, thành tiền 40.000→60.000 (đơn giá × SL). *Tổng tiền trễ async* |
| 1.4.3 | Giảm số lượng (−) | PASS | Cơm SL 3→2, thành tiền 60.000→40.000 |
| 1.4.4 | Xóa món (thùng rác) | KHÔNG KIỂM THỬ | Có icon thùng rác đỏ cuối dòng; chưa bấm |
| 1.4.5 | Sửa đơn giá thủ công | KHÔNG KIỂM THỬ | Có icon bút ở cột Đơn giá; chưa thử |
| 1.4.6 | Ghi chú từng món | PASS | Dòng Cơm có "Ghi chú: ít cay @#1" + link "Chỉnh sửa" |
| 1.4.7 | Tổng tiền (tạm tính) | PASS | 500.000 + 40.000 = **540.000** = "Tổng tiền hàng" |
| 1.4.8 | Thuế theo từng món | PASS | "Thuế sản phẩm" = **2.000** = 5% × 40.000 (Cơm); "Test điều chuyển" thuế 0% |
| 1.4.9 | Thuế theo cả bill | KHÔNG KIỂM THỬ | Chưa cấu hình/đối chiếu thuế cả bill riêng |
| 1.4.10 | Kết hợp thuế món + bill | KHÔNG KIỂM THỬ | — |
| 1.4.11 | Tổng tiền thanh toán | PASS | **596.000** = 540.000 (hàng) + 54.000 (phụ thu) − 0 (giảm) + 2.000 (thuế) |
| 1.4.12 | Phụ thu | PASS | Phụ thu "[ngay cuoi tuan]" = **54.000** = 10% của 540.000 (đơn BAN1 đã có phụ thu cấu hình sẵn) |
| 1.4.13 | Giảm giá | KHÔNG KIỂM THỬ | Có dòng "Giảm giá" + icon bút; chưa thực hiện luồng + đối chiếu admin |
| 1.4.15 | Combo / Set menu | KHÔNG KIỂM THỬ | Có "comboo 10" (555.000), "setmenu hoa hồng" (550.000), "comboo hoa hồng" (999.999)…; chưa thêm để kiểm thành phần |
| 1.4.16 / 1.4.21 | Chọn khách hàng / "Chọn thành viên" | KHÔNG KIỂM THỬ | Có dropdown **"Chọn thành viên"** (đúng nhãn thực tế, không phải "Khách lẻ"); chưa mở |
| 1.4.17 | Nhiều hóa đơn / 1 bàn | PASS | **BAN6 có 3 hóa đơn** (POS…057 60.000, POS…058 30.000, POS…059 60.000) → mở ra modal "Chọn đơn hàng"; trong Order có tab "POS…057CN2" + nhãn **"+2"** và nút "+" thêm hóa đơn |
| 1.4.18 | Đơn các bàn độc lập | KHÔNG KIỂM THỬ | — |
| 1.4.19 | Hóa đơn trống | PASS | Lúc mới mở Order hiện "Giỏ hàng trống. Hãy chọn món bên trái!", tổng tiền = 0đ; nút "Báo bếp" bị mờ (disabled) |
| 1.4.20 | Nhân viên phụ trách | PASS (một phần) | Đăng nhập "Admin master"; hiển thị ở góc phải app |
| 1.4.22 | Modal sửa giá — ô "Giá mới" là output | KHÔNG KIỂM THỬ | Chưa mở modal "Thay đổi giá bán" |
| 1.4.23 | Phụ thu khi để "Không áp dụng" | KHÔNG KIỂM THỬ | Chưa mở modal "Chọn phụ thu" |
| 1.4.24 | Tổng tiền cập nhật bất đồng bộ | **FAIL (xác nhận lỗi)** | "Thành tiền" của dòng đổi **ngay**, nhưng "Tổng tiền hàng / Phụ thu / Thuế / Tổng thanh toán" **trễ ~3–7s** mới khớp. Tái hiện nhiều lần (thêm món, +/-). Xem mục 1.20.1 |

## 1.5 In bếp / Thanh toán

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.5.1 | In phiếu Bếp/Bar (báo bếp) | KHÔNG KIỂM THỬ | Nút "Báo bếp" (cam khi có món chờ, **mờ khi không có món mới**); không thực hiện để tránh thao tác thật |
| 1.5.2 | Tạm tính | KHÔNG KIỂM THỬ | Có nút "Tạm tính" (xanh lá) |
| 1.5.3 | Thanh toán tiền mặt | KHÔNG KIỂM THỬ | Có nút "Tiền mặt"; không hoàn tất để tránh đóng đơn thật |
| 1.5.4 | Thanh toán chuyển khoản | KHÔNG KIỂM THỬ | Có nút "Chuyển khoản" |
| 1.5.5 | Thanh toán quẹt thẻ | KHÔNG KIỂM THỬ | Có nút "Quẹt Thẻ" |
| 1.5.6 | Thanh toán QR tự động | KHÔNG KIỂM THỬ | Có nút "QR Tự động" |
| 1.5.7 | Tiền thừa | KHÔNG KIỂM THỬ | Có ô "Tiền khách đưa" trong panel |
| 1.5.8 | Chặn hóa đơn trống | PASS (một phần) | Khi giỏ trống, nút "Báo bếp" bị **mờ/disabled** (không cho thao tác) |

## 1.6 Xác nhận đơn (tại bàn / QR / mang về)

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.6.1 | Tab "Chờ xác nhận" hiển thị đơn chờ | N/A | Hiện (0) — empty state đúng |
| 1.6.2 | Xác nhận đơn tại bàn (tablet/mobile) | BLOCKED | Cần thiết bị tablet/mobile gửi đơn (phụ thuộc ngoài) |
| 1.6.3 | Xác nhận đơn QR | BLOCKED | Cần khách quét QR bàn đặt món |
| 1.6.4 | Xác nhận đơn mang về | BLOCKED | Cần đơn mang về chờ xác nhận |
| 1.6.5 | Từ chối đơn | BLOCKED | Cần đơn chờ xác nhận |
| 1.6.6 | Tìm kiếm/chọn bàn cần xác nhận | BLOCKED | Cần đơn chờ xác nhận |
| 1.6.7 | Sau xác nhận, số đếm giảm | BLOCKED | Cần đơn chờ xác nhận |

## 1.7 Gửi bếp

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.7.1 | Gửi bếp sau khi chọn món | PASS (một phần) | Trên đơn BAN6 (POS…057), món "cf sua new" ở trạng thái **"Chờ chế biến"** (= đã gửi bếp, đang chờ chế biến); nút "Báo bếp" mờ vì không còn món mới |
| 1.7.2 | Món chưa gửi bếp | PASS | Món mới ("Test điều chuyển", "Cơm") hiển thị nhãn **"Chờ báo bếp"** trên dòng |
| 1.7.3 | Gửi bếp khi giỏ trống | KHÔNG KIỂM THỬ | Quan sát: nút "Báo bếp" mờ khi giỏ trống (gợi ý sẽ chặn) |
| 1.7.4 | Gửi bếp chỉ áp món mới thêm | KHÔNG KIỂM THỬ | — |

## 1.8 Chuyển bàn

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.8.1 | Mở chức năng chuyển bàn | PASS (một phần) | **"Chuyển bàn" có trong menu "..."** của hóa đơn (xác nhận tồn tại/truy cập được) |
| 1.8.2 – 1.8.9 | Luồng chuyển bàn chi tiết | KHÔNG KIỂM THỬ | Chưa chạy đủ luồng (mục menu mở chập chờn; tránh thay đổi dữ liệu thật) |

## 1.9 Gộp bàn

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.9.1 | Mở chức năng gộp bàn | PASS (một phần) | **"Gộp bàn" có trong menu "..."** (xác nhận tồn tại/truy cập được) |
| 1.9.2 – 1.9.11 | Luồng gộp bàn chi tiết | KHÔNG KIỂM THỬ | Chưa chạy đủ luồng |

## 1.10 Tách / ghép đơn

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.10.1 | Mở chức năng tách/ghép | PASS | Menu "..." → "Tách/Ghép đơn" → mở giao diện đúng |
| 1.10.3 | Giao diện đúng thông tin bàn nguồn | PASS | Panel hiển thị đúng đơn BAN1: "Test điều chuyển" (SL tối đa 1), "Cơm" (M, Đường 50%, SL tối đa 2) |
| 1.10.4 | Chọn bàn/hóa đơn đích | PASS | Có dropdown **"Bàn nhận"** (ban1) và **"Hóa đơn nhận"** (mặc định "Tạo đơn mới") |
| 1.10.20 | Xác nhận khi chưa chọn món | PASS | "Tạm tính (0 món) 0đ"; nút **"Xác nhận" bị mờ/disabled** khi SL tách = 0 |
| 1.10.19 | Hủy/Đóng giữa chừng | CẦN XEM LẠI | Khi app đơ, các nút "Đóng"/X/Esc **không đóng được modal** (lỗi tương tác tự động — không kết luận được hành vi nghiệp vụ) |
| 1.10.2, 1.10.5–1.10.18, 1.10.21–1.10.30 | Các luồng tách/ghép chi tiết | KHÔNG KIỂM THỬ | Chưa thực hiện tách/ghép thật (tránh đổi dữ liệu) |

## 1.11 Hàng tặng

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.11.1 | Mở chức năng hàng tặng | PASS (một phần) | "Hàng tặng" có trong menu "..." |
| 1.11.6 | Đơn không thỏa điều kiện | PASS (một phần) | Trên đơn BAN1, mục **"Hàng tặng" bị mờ/disabled** (đơn chưa đủ điều kiện); trên đơn BAN6 thì sáng (cho chọn) |
| 1.11.2 – 1.11.5 | Chi tiết món tặng | KHÔNG KIỂM THỬ | Chưa mở danh sách hàng tặng |

## 1.12 Áp dụng khuyến mãi

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.12.1 | Mở chức năng khuyến mãi | PASS (một phần) | "Khuyến mãi" có trong menu "..."; modal **không mở được** ổn định bằng click tự động |
| 1.12.2 – 1.12.5 | Áp/bỏ khuyến mãi | KHÔNG KIỂM THỬ | — |
| 1.12.6 | Chưa mở ca | N/A | Ca đang mở |

## 1.13 Hủy đơn

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.13.1 – 1.13.5 | Toàn bộ chức năng hủy đơn | KHÔNG KIỂM THỬ | Có nút X cạnh tab hóa đơn; không thực hiện hủy để tránh phá dữ liệu thật |

## 1.14 Thanh toán đơn hàng (qua Chờ thanh toán)

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.14.1 | Tab "Chờ thanh toán" hiển thị đơn chờ | N/A | Hiện (0) — empty state đúng |
| 1.14.2 | Thanh toán từ tab Chờ thanh toán | KHÔNG KIỂM THỬ | Không có đơn chờ thanh toán |
| 1.14.3 | Thanh toán bằng chọn bàn đang dùng | KHÔNG KIỂM THỬ | Không thực hiện thanh toán thật |
| 1.14.4 | Thanh toán đơn từ tablet/mobile | BLOCKED | Cần thiết bị bên ngoài |

## 1.15 Trường hợp đặc thù & lỗi

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.15.1 | Số lượng món = 0 | KHÔNG KIỂM THỬ | — |
| 1.15.2 | Giá rất lớn | PASS (một phần) | Món "comboo hoa hồng" **999.999đ** hiển thị đúng, không tràn giao diện; chưa thử 999.999.999đ |
| 1.15.3 | Làm tròn tiền VND | PASS | Thuế/tổng hiển thị **số nguyên** (2.000, 54.000, 596.000…), không có số lẻ thập phân |
| 1.15.4 | Mất mạng khi thanh toán | BLOCKED | Không thể ngắt mạng qua công cụ tự động |
| 1.15.5 | Hai thu ngân cùng 1 bàn | BLOCKED | Cần 2 thiết bị/phiên đồng thời |
| 1.15.6 | Ghi chú có dấu / ký tự đặc biệt | PASS | "ít cay @#1" lưu & hiển thị đúng, không lỗi ký tự |

## 1.16 In tem / In lại tem / In lại phiếu bếp

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.16.1 | In tem món | PASS (một phần) | "In tem" có trong menu "..." (truy cập được); chưa kích hoạt in |
| 1.16.2 | In lại tem | PASS (một phần) | "In lại tem" có trong menu "..." |
| 1.16.3 | In lại phiếu bếp | PASS (một phần) | "In lại phiếu bếp" có trong menu "..." |
| 1.16.4 | In tem khi giỏ trống | KHÔNG KIỂM THỬ | — |
| 1.16.5 | Cảnh báo chưa cấu hình máy in | KHÔNG KIỂM THỬ | Chưa kích hoạt được lệnh in để xem toast cảnh báo |

## 1.17 Hóa đơn điện tử

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.17.1 | Mở form Hóa đơn điện tử | PASS | Menu "..." → "Hóa đơn điện tử" → form có nhóm **"Thông tin hóa đơn"** (Ngày phát hành) và **"Thông tin bên mua"** (radio Cá nhân / Doanh nghiệp) |
| 1.17.2 | Bên mua loại "Cá nhân" | PASS | Hiện đúng: **Họ tên (\*)**, CCCD/CMND, Số điện thoại, Hộ chiếu, **Địa chỉ (\*)**, Email, Mã đơn vị QHNS |
| 1.17.3 | Bên mua loại "Doanh nghiệp" | KHÔNG KIỂM THỬ | Radio "Doanh nghiệp" **không chuyển được** bằng click tự động (lỗi tương tác) |
| 1.17.4 | Bắt buộc Họ tên & Địa chỉ | PASS (một phần) | "Họ tên" và "Địa chỉ" có dấu **(\*)** bắt buộc; chưa chạy validation submit |
| 1.17.5 | Ngày phát hành mặc định | PASS | Mặc định **24/06/2026** (đúng ngày hiện tại), định dạng dd/MM/yyyy |
| 1.17.6 | Áp dụng phát hành HĐĐT | KHÔNG KIỂM THỬ | Có nút "Áp dụng"; chưa hoàn tất |
| 1.17.7 | Email/SĐT sai định dạng | KHÔNG KIỂM THỬ | — |

## 1.18 Đồng giá

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.18.1 | Mở chức năng Đồng giá | PASS (một phần) | "Đồng giá" có trong menu "..." (truy cập được); modal chưa mở ổn định |
| 1.18.2 – 1.18.4 | Chi tiết đồng giá | KHÔNG KIỂM THỬ | — |

## 1.19 Thanh toán đa phương thức

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.19.1 | Bật chế độ thanh toán đa phương thức | PASS (một phần) | "Thanh toán đa phương thức" có trong menu "..." (truy cập được) |
| 1.19.2 – 1.19.6 | Chia tiền nhiều phương thức | KHÔNG KIỂM THỬ | — |

## 1.20 Hiệu năng & ổn định (Flutter web)

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.20.1 | Tổng tiền cập nhật tức thì | **FAIL** | Tổng tiền cập nhật **trễ ~3–7s** (bất đồng bộ) sau khi thêm/+/- món. "Thành tiền" dòng đổi ngay nhưng "Tổng tiền hàng/Phụ thu/Thuế/Tổng thanh toán" trễ → dễ gây hiểu nhầm số tiền lúc thao tác nhanh |
| 1.20.2 | App không treo khi thao tác liên tục | **FAIL** | Sau ~15 thao tác, renderer **đơ/giật nặng**: click không tác dụng, chụp màn hình time-out, modal không đóng được → **buộc reload** (đã reload 2 lần trong phiên) |
| 1.20.3 | Khôi phục dữ liệu sau reload | PASS | Sau reload + chọn lại Thu ngân, đơn BAN1 **giữ nguyên** dữ liệu (Test điều chuyển + Cơm vừa thêm = thẻ bàn 540.000); không tạo đơn trùng |

---

## Tổng hợp

- **PASS: 40** (gồm "PASS một phần" có bằng chứng rõ): 1.1.1–1.1.5b, 1.1.8, 1.1.9, 1.1.10, 1.1.12, 1.1.14, 1.1.16–1.1.18, 1.2.1–1.2.3, 1.2.7, 1.2.9, 1.3.1, 1.3.2, 1.3.4–1.3.6, 1.3.8, 1.4.1–1.4.3, 1.4.6–1.4.8, 1.4.11, 1.4.12, 1.4.17, 1.4.19, 1.4.20, 1.5.8, 1.7.1, 1.7.2, 1.8.1, 1.9.1, 1.10.1, 1.10.3, 1.10.4, 1.10.20, 1.11.6, 1.15.2, 1.15.3, 1.15.6, 1.16.1–1.16.3, 1.17.1, 1.17.2, 1.17.4, 1.17.5, 1.20.3
- **FAIL: 3** — **1.4.24 / 1.20.1** (tổng tiền cập nhật trễ bất đồng bộ), **1.20.2** (renderer đơ/giật buộc reload)
- **N/A: 5** — 1.1.11, 1.6.1, 1.12.6, 1.14.1 (các tab trạng thái = 0), 1.2.6 (không có phân trang)
- **BLOCKED: 9** — 1.6.2–1.6.7, 1.14.4, 1.15.4, 1.15.5 (phụ thuộc tablet/mobile/QR/mạng/đa thiết bị)
- **CẦN XEM LẠI: 1** — 1.10.19 (không đóng được modal khi app đơ; không kết luận hành vi nghiệp vụ)
- **KHÔNG KIỂM THỬ (chưa hoàn tất trong phiên):** phần lớn 1.5 (các hình thức thanh toán), 1.13 (hủy đơn), nhiều mục chi tiết của 1.4 (xóa/sửa giá/giảm giá/combo/khách hàng), 1.8–1.9 (chuyển/gộp bàn), 1.10 (các luồng tách/ghép), 1.11–1.12 (hàng tặng/khuyến mãi áp dụng), 1.16.4–1.16.5, 1.17.3/1.17.6/1.17.7, 1.18–1.19 — do (1) tránh thao tác phá hủy dữ liệu thật (thanh toán/hủy/tách/ghép), và (2) **giới hạn tương tác tự động trên Flutter web**: các thao tác mở/đóng overlay & menu "..." không ổn định, app đơ phải reload.

### Lỗi / điểm cần lưu ý chính
1. **Hiệu năng — tổng tiền cập nhật bất đồng bộ (1.20.1 / 1.4.24)**: cột "Thành tiền" của dòng đổi ngay, nhưng các dòng tổng (Tổng tiền hàng / Phụ thu / Thuế / Tổng thanh toán) **trễ ~3–7s** mới khớp. Tái hiện nhiều lần. Cần kiểm tra để tránh hiểu nhầm số tiền lúc thanh toán nhanh. *(Ảnh: `screenshot/0624_0203_home/` — mô tả bằng chữ; công cụ phiên không lưu được ảnh)*
2. **Ổn định — renderer đơ/giật buộc reload (1.20.2)**: sau một chuỗi thao tác, app ngừng phản hồi click, modal không đóng được, phải tải lại trang. Cần kiểm tra lại hiệu năng trên thiết bị thật (một phần có thể do môi trường điều khiển tự động, nhưng độ giật lặp lại đáng lưu ý).
3. **Quan sát tích cực (đúng kỳ vọng):** logic tính tiền chính xác — Tổng thanh toán = Tổng tiền hàng + Phụ thu(10%) − Giảm giá + Thuế(theo món); thuế theo từng món đúng %; tìm món không phân biệt dấu; ghi chú tiếng Việt + ký tự đặc biệt ok; số đếm bộ lọc khớp; số đếm trạng thái toàn cục; "Bàn mang về" tính vào "Tất cả" lệch +1 đúng quy ước.

> Khuyến nghị: chạy bổ sung trên **thiết bị/môi trường thật (thao tác tay)** để hoàn tất các mục KHÔNG KIỂM THỬ phụ thuộc thao tác overlay/menu "..." (thanh toán, hủy đơn, chuyển/gộp/tách-ghép bàn, hàng tặng, khuyến mãi áp dụng, đồng giá, đa phương thức, in tem) — vì các thao tác này không ổn định khi điều khiển tự động trên Flutter web canvas. Hai mục FAIL về hiệu năng (1.20.1, 1.20.2) nên được ưu tiên kiểm tra lại.

---

## Phụ lục — Phiên 2 (chạy lại các case chưa test, đã được phép thao tác mọi thứ trên tài khoản test)

Người dùng xác nhận được phép thực hiện mọi thao tác (kể cả thanh toán/hủy/tách-gộp). Đã đăng nhập lại và thử chạy tiếp các case overlay-phụ thuộc.

**Bổ sung PASS:**
- **1.5.1 In phiếu Bếp/Bar (Báo bếp)** — PASS: tạo đơn mới ở BAN2, thêm "tran chau" (10.000), bấm **"Báo bếp"** → nút hiện spinner xử lý → trạng thái món chuyển từ **"Chờ báo bếp"** sang **"Đã báo bếp"**; nút "Báo bếp" tự mờ sau khi gửi (không còn món mới).
- **1.7.1 Gửi bếp sau khi chọn món** — PASS (xác nhận trọn vẹn qua thao tác trên).
- **1.3.2 / 1.3.3 (bổ sung cấu trúc)**: Modal "Chọn món kèm theo" của món **"Trà A hỷ"** giàu tùy chọn hơn — Size có **LL = +3.000đ** (thuộc tính CÓ phụ thu), nhóm Ngọt, nhóm **Đá** (Đá 100%/50%), và **"Món thêm" → Nước ngọt → "coca cola 5%" (+5.000đ)** kèm nút +/- số lượng. → Xác nhận tồn tại nhóm "Món thêm" (1.3.3) và thuộc tính có phụ thu (1.3.2).
- **1.4.19 / 1.4.1** tái xác nhận trên đơn mới BAN2 (hóa đơn trống → "Giỏ hàng trống…", thêm món → tổng/thuế cập nhật).

**Kết luận quan trọng về khả năng tự động hóa (lý do nhiều case vẫn KHÔNG KIỂM THỬ):**
Trên app Flutter web canvas này, **việc MỞ các overlay** (dropdown "Chọn thành viên"/số cột/giao diện/chế độ xem, modal Phụ thu/Giảm giá/Thay đổi giá, hộp thoại Thanh toán, các mục trong menu "...": Khuyến mãi/Hàng tặng/Đồng giá/Đa phương thức/HĐĐT/In tem, giao diện Tách-ghép/Chuyển/Gộp bàn, Hủy đơn) **không kích hoạt được ổn định** bằng điều khiển tự động — cả click thật (CDP) lẫn sự kiện pointer tổng hợp (JS) đều thất bại phần lớn thời gian, ngay cả khi vừa tải lại trang. Tỷ lệ mở thành công thấp và ngẫu nhiên; nhiều lần phải thử lại 3–5 lần mới mở được 1 modal, và app đơ sau ~15 thao tác phải reload.

→ Vì vậy các case còn lại (đa số 1.4 nâng cao, 1.5 thanh toán, 1.8/1.9/1.10 thực thi, 1.11/1.12/1.13, 1.16–1.19) **không thể hoàn tất bằng kiểm thử tự động** trong môi trường hiện tại. **Đây là giới hạn công cụ/đặc thù app, không phải vấn đề quyền** (người dùng đã cấp quyền). Khuyến nghị: kiểm thử các case này **thủ công trên thiết bị thật**, hoặc dùng giải pháp tự động hỗ trợ Flutter semantics tốt hơn (VD bật Flutter accessibility ổn định / driver chuyên cho Flutter).
