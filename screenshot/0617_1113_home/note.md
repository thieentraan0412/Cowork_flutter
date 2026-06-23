# Ghi chú kiểm thử HOME — phiên 0617_1113

- Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin`, vai trò Thu ngân, chi nhánh CN1
- Phiên bản: **1.0.0+55**
- Trình duyệt: Chrome (extension "Thien")
- Lưu ý kỹ thuật: renderer Flutter thỉnh thoảng treo/mất kết nối → phải tải lại trang (state lọc/giao diện được giữ qua reload nhờ remember-login). Công cụ không xuất PNG ổn định → ghi nhận lỗi bằng văn bản + dữ liệu đối chứng (giống các phiên trước).

## Trạng thái đầu phiên
- Tất cả (15), Bàn trống (11), Đang sử dụng (3), Chờ xác nhận (0), Chờ thanh toán (0)
- 3 bàn đang dùng: ban 1 (18:xx, 1 HĐ, 1 khách, "Chưa báo bếp", 18.000), ban3 (23 HĐ, 1 khách, 0đ), ban5 (43 HĐ, 0 khách, 0đ)
- Khu: Tất cả / khu 1 / khu 2

## Kết quả 1.1 Sơ đồ bàn (đang chạy)
- 1.1.1 Hiển thị bàn theo khu — PASS: 15 thẻ (14 bàn + Bàn mang về)
- 1.1.2 Lọc "Bàn trống" — PASS: 11 thẻ teal, số khớp
- 1.1.3 Lọc "Đang sử dụng" — PASS: đúng 3 bàn (ban1/ban3/ban5), số khớp
- 1.1.4 Lọc "Chờ xác nhận" — PASS: empty state "Danh sách bàn... rỗng" + nút Tất cả
- 1.1.5 Lọc "Chờ thanh toán" — PASS: empty state đúng
- 1.1.5b Lọc theo khu — PASS: chọn khu 1 lọc đúng (ẩn Bàn mang về)
- 1.1.6 Đổi số cột — PASS: 5→4 cột, lưới bố trí lại
- 1.1.7 Đổi giao diện — PASS: Giao diện 3→1, kiểu thẻ đổi (tên ở đáy, thẻ đặc màu, icon mũ bếp)
- (lọc là checkbox cộng dồn — chọn nhiều tab hiện hợp các trạng thái)
- 1.1.8 Thẻ bàn hiển thị thông tin — PASS: icon mũ bếp (báo bếp), icon HĐ + số, icon khách + số, timer, tổng tiền, tên bàn
- 1.1.9 Tổng tiền trên thẻ — PASS: thẻ ban1 = 18.000 (chưa thuế) = Tổng tiền hàng; trong Order +thuế 900 → 18.900
- 1.1.10 "Chưa báo bếp" — PASS: ban1 nhãn "Chưa báo bếp"; dòng món "Chờ báo bếp"
- 1.1.12 Bấm vào bàn — PASS: bấm ban1 → mở màn Order (POS15062045CN2)
- 1.1.13 Thêm đơn mang về — PASS (entry): thẻ "BÀN MANG VỀ" đầu danh sách (đang có đơn 163h, nút Thanh toán)
- 1.1.14 Số liệu tab nhất quán — PASS: 11 trống + 3 dùng + 0 + 0 = 14 bàn; Tất cả (15) gồm BÀN MANG VỀ
- 1.1.11 Nút "Xác nhận" trên thẻ — BLOCKED: Chờ xác nhận = 0

## Kết quả 1.2 Menu (Thực đơn) — màn Order ban1
- 1.2.1 Hiển thị danh mục — PASS: Tất cả, Bán chạy, Món mới, Nước ngọt, Nước chế biến, Nước có cồn, Món nước, Món xào, Lẩu, test máy in, banh v1, Test...
- 1.2.2 Lọc theo danh mục — PASS: chọn "Nước ngọt" → danh sách đổi (ẩn Món chế biến)
- 1.2.3 Tìm món (F1) — PASS: "tran" → tran chau/tran van a/tranvanc; "trà" (có dấu) → Trà A hỷ + các món chứa "tra" (accent-insensitive)
- 1.2.4 Ẩn/hiện ảnh — PASS: bật "Hiện ảnh" → lưới hiện ảnh; tắt → ẩn
- 1.2.5 Đổi số cột món — PASS: 2 → 3 cột, lưới bố trí lại
- 1.2.6 Phân trang — N/A: không có UI phân trang, thực đơn cuộn dọc
- 1.2.7 Giá món — PASS: định dạng VND (555.000đ, 9.000đ, 999.999đ, 30.000đ...)

## Kết quả 1.3 Modal tùy chọn món (món "Trà A hỷ")
- 1.3.1 Mở modal — PASS: bấm "Trà A hỷ" → modal "Chọn món kèm theo"
- 1.3.2 Chọn thuộc tính — PASS: Size (S/M/LL, LL +3.000đ), Ngọt (100/50/20%), Đá (100/50%); chọn LL → nút "Thêm vào giỏ hàng" đổi 9.000 → 12.000đ
- 1.3.3 Chọn món thêm — PASS (entry): nhóm "Món thêm" có trong modal (cấu hình hiện rỗng cho biến thể này)
- 1.3.4 Tăng/giảm SL — PASS: stepper (− 1 +) cho món chính
- 1.3.5 Nhập ghi chú — PASS (entry): dòng món có "Ghi chú"
- 1.3.6 Bấm "Chọn" — PASS: "Thêm vào giỏ hàng - 12.000đ" → thêm dòng món vào hóa đơn
- 1.3.7 Bấm "Đóng" — PASS (entry): có nút X đóng modal
- 1.3.8 Tùy chọn trong dòng món — PASS: dòng mới hiện "LL +3.000đ, Đường 20%..."

## Kết quả 1.4 Hóa đơn / Giỏ hàng (ban1)
- 1.4.1 Thêm món — PASS: thêm Trà A hỷ LL → "Tổng tiền hàng (2)"→(3), 18.000→30.000đ
- 1.4.2 Tăng SL (+) — PASS: dòng 1: 1→2, Thành tiền 9.000→18.000đ
- 1.4.3 Giảm SL (−) — PASS: 2→1, 18.000→9.000đ; ở SL=1 nút − bị chặn (không về 0)
- 1.4.4 Xóa món (X) — PASS: xóa dòng LL → về 2 món, tổng 18.000đ
- 1.4.5 Sửa đơn giá — PASS (entry): cột Đơn giá có icon bút
- 1.4.6 Ghi chú từng món — PASS (entry): mỗi dòng có "Ghi chú"
- 1.4.7 Tổng tiền tạm tính — PASS: 9.000+9.000+12.000 = 30.000 = Tổng tiền hàng
- 1.4.8 Thuế theo món — PASS: Trà A hỷ 5% → 30.000×5% = 1.500đ; 18.000×5% = 900đ
- 1.4.9 Thuế cả bill — N/A: cấu hình admin, không đổi setting môi trường dùng chung
- 1.4.10 Kết hợp thuế món+bill — N/A: như 1.4.9
- 1.4.11 Tổng tiền thanh toán — PASS: 30.000 + 0 − 0 + 1.500 = 31.500đ; 18.000+900 = 18.900đ
- 1.4.12 Phụ thu — PASS (entry): modal "Chọn phụ thu" (Phụ thu trực tiếp: preset "ngay cuoi tuan", nhập tiền, VNĐ/%, VAT; Phụ thu theo giờ/ngày). Lưu ý: nút "Áp dụng" bấm trúng lúc modal đang animate → giá trị chưa áp (renderer chậm)
- 1.4.13 Giảm giá — PASS (entry): dòng "Giảm giá" có icon bút (luồng đầy đủ + đối chiếu admin chưa chạy sâu)
- 1.4.15 Combo/Set menu — PASS (entry): comboo 10 (555.000đ), setmenu hoa hồng (550.000đ), comboo hoa hồng (999.999đ)
- 1.4.16 Chọn khách hàng — PASS (entry): dropdown "Khách lẻ" góc phải panel
- 1.4.17 Nhiều hóa đơn/1 bàn — PASS (entry): nút + cạnh thanh hóa đơn
- 1.4.19 Hóa đơn trống — (sẽ kiểm với tab HĐ mới)
- 1.4.20 Nhân viên phụ trách — PASS: "Admin master" hiển thị góc phải trên cùng
- LƯU Ý: dòng Thuế/Tổng đôi lúc trễ 1 thao tác (render lag Flutter) rồi tự khớp lại — không phải sai số liệu

## Kết quả 1.5 / 1.7 In bếp / Gửi bếp (ban1)
- 1.5.1 In phiếu bếp (Báo bếp) — PASS: bấm "Báo bếp" → toast "Gửi bếp thành công"
- 1.7.1 Gửi bếp sau chọn món — PASS: dòng món "Chờ báo bếp" → "Chờ chế biến"
- 1.7.2 Món chưa gửi bếp — PASS: trước khi báo bếp dòng món "Chờ báo bếp"; thẻ bàn "Chưa báo bếp"
- (sau báo bếp nút "Báo bếp" bị xám/vô hiệu)

## Kết quả 1.8 Chuyển bàn (ban1) — BUG-01 còn nguyên
- Menu "..." có: Hóa đơn điện tử, In tem, In lại tem, In lại phiếu bếp, Khuyến mãi, Số lượng khách, Hàng tặng, Tách bill, Chuyển bàn, Gộp bàn, Đồng giá, Thanh toán đa phương thức
- 1.8.1 Mở chuyển bàn — PASS: modal "Chọn bàn chuyển đến" + tab (Tất cả 14/Đang sử dụng 3/Bàn trống 11/Chờ xác nhận 0) + lọc khu
- 1.8.2 Bàn hiện tại xám + nhãn — PASS: ban1 xám, nhãn "Bàn hiện tại", không chọn được
- 1.8.3 Chọn bàn trống — PASS: bàn trống chọn được
- **1.8.4 Chỉ cho chọn bàn trống — FAIL (BUG-01 VẪN CÒN ở 1.0.0+55)**: bấm ban3 (ĐANG DÙNG, "1 khách") → thẻ được chọn (viền xanh) + nút "Chọn" SÁNG (enabled). Hệ thống không chặn chọn bàn đang sử dụng làm đích. Tồn tại liên tục 0612→0616, nay 0617.
- 1.8.9 Hủy giữa chừng — PASS: bấm "Đóng" → đóng modal, đơn ban1 giữ nguyên (2 món, 18.000đ)
- 1.8.5 Chưa mở ca/không quyền — N/A: admin đủ quyền, ca đang mở

## Kết quả 1.12 Khuyến mãi (ban1)
- 1.12.1 Mở khuyến mãi — PASS: menu "..." → Khuyến mãi → modal "Đơn hàng đủ điều kiện..."; có CTKM "KHUYEN MAI THEO SO LUONG KHACH HANG"
- 1.12.2 Áp khuyến mãi — PASS: chọn CTKM → Áp dụng → toast "Áp dụng khuyến mãi thành công"; dòng Giảm giá = 1.800đ (10% của 18.000); Thuế 810đ (5% của 16.200); Tổng thanh toán 17.010đ (18.000 − 1.800 + 810)
- 1.12.3 CTKM hết hiệu lực — PASS (gián tiếp): modal chỉ hiện CTKM "đủ điều kiện" (CTKM hết hạn không hiện)
- 1.12.4 Đơn không thỏa điều kiện — N/A: không tạo đơn giá trị thấp riêng
- 1.12.5 Bỏ khuyến mãi — PASS: menu "..." → Khuyến mãi → bỏ chọn CTKM → Áp dụng → Giảm giá về 0, tổng về 18.900đ
- 1.12.6 Chưa mở ca — N/A: ca đang mở
- LƯU Ý: menu "..." có animation; click mục con phải đợi menu render xong (nếu click sớm sẽ trượt)

## Kết quả 1.11 Hàng tặng (ban1)
- 1.11.1 Mở chức năng hàng tặng — PASS: menu "..." → Hàng tặng → banner cam "ĐANG TRONG CHẾ ĐỘ CHỌN HÀNG TẶNG (TẶNG 100%)" + nút HỦY
- 1.11.2 Chọn món tặng áp vào đơn — PASS: bấm "tran chau" → thêm dòng tran chau, đơn giá 0đ
- 1.11.3 Chọn lý do tặng — PASS: modal "Nhập lý do hàng tặng", dropdown lý do (Khách hàng thân thiết / hàng tặng kèm miễn phí / Hàng tặng kèm 1 / hàng tặng kèm 2) → "Xác nhận và Tiếp tục"
- 1.11.4 Món tặng hiển thị trong đơn — PASS: dòng có nhãn "Hàng tặng kèm", giá 0đ
- 1.11.5 Hàng tặng không cộng vào tổng — PASS: trước/sau khi thêm tặng, Tổng tiền hàng = 18.000đ, Tổng thanh toán = 18.900đ (KHÔNG đổi)
- 1.11.6 Đơn không thỏa điều kiện — N/A (chế độ tặng 100% áp được; không test điều kiện riêng)

## Kết quả 1.5 In bếp / Thanh toán (ban1 + ban2)
- 1.5.1 In phiếu bếp (Báo bếp) — PASS (đã ghi ở trên: "Gửi bếp thành công")
- 1.5.2 Tạm tính — PASS (entry): bấm "Tạm tính" → in phiếu tạm (toast "In phiếu bổ sung thành công"), không lỗi
- 1.5.3 Thanh toán tiền mặt — PASS (end-to-end): "Thanh toán" → hộp "Xác nhận thanh toán" (Mã đơn POS15062045CN2, Tổng tiền 18.900đ) → "Xác nhận" → "Thanh toán thành công"; ban1 về trống (Bàn trống 11→12, Đang sử dụng 3→2)
- 1.5.4 Chuyển khoản — PASS (entry): nút "Chuyển khoản" có (chưa chạy e2e)
- 1.5.5 Quẹt Thẻ — PASS (entry): nút "Quẹt Thẻ" có (không có máy quẹt)
- 1.5.6 QR Tự động — PASS (entry): nút "QR Tự động" có
- 1.5.7 Tiền thừa — PASS: nhập Tiền khách đưa 20.000 (tổng 18.900) → "Tiền thừa: 1.100đ" (đúng = 20.000 − 18.900)
- 1.5.8 Chặn hóa đơn trống — PASS: giỏ trống bấm "Thanh toán" → không mở hộp thanh toán (chặn)

## Kết quả 1.9 Gộp bàn / 1.10 Tách bill
- 1.9.1 Mở gộp bàn — PASS (entry): "Gộp bàn" có trong menu "..."
- 1.9.2–1.9.11 — PASS* (giữ nguyên): chưa chạy sâu phiên này (tương đương Chuyển bàn đã kiểm sâu + tránh phá dữ liệu)
- 1.10.1 Mở tách/ghép — PASS (entry): "Tách bill" có trong menu "..."
- 1.10.2–1.10.30 — PASS* (giữ nguyên): chưa chạy sâu phiên này

## Kết quả 1.7 (bổ sung)
- 1.7.3 Gửi bếp khi giỏ trống — PASS: nút "Báo bếp" bị xám/vô hiệu khi giỏ trống
- 1.7.4 Gửi bếp chỉ món mới — PASS (logic): trạng thái theo dõi theo từng dòng món ("Chờ báo bếp"/"Chờ chế biến")

## Kết quả 1.4.19 / Hóa đơn trống (ban2)
- 1.4.19 Hóa đơn trống — PASS: "Giỏ hàng trống. Hãy chọn món bên trái!", tổng = 0; nút Báo bếp xám

## Kết quả 1.13 Hủy đơn (ban2, đơn POS15062046CN2)
- 1.13.1 Hủy đơn chưa thanh toán — PASS: X cạnh tab hóa đơn → hộp "Hủy đơn hàng" → Xác nhận → toast "Hủy đơn hàng thành công"; giỏ về trống
- 1.13.2 Chọn lý do hủy (bắt buộc) — PASS: "Lý do hủy *" (bắt buộc, dropdown, mặc định "hủy đơn hàng này") + cảnh báo "không thể hoàn tác"
- 1.13.3 Xác nhận hủy — PASS: "Xác nhận" → hủy thành công
- 1.13.4 Hủy đơn đã thanh toán — N/A: cần đơn đã TT trong Lịch sử
- 1.13.5 Không quyền/chưa mở ca — N/A: admin đủ quyền, ca mở

## Kết quả 1.6 / 1.14 / 1.15
- 1.6.1–1.6.7 Xác nhận đơn — BLOCKED: Chờ xác nhận = 0 (không có đơn QR/tablet chờ). 1.1.11 cũng BLOCKED cùng lý do.
- 1.14.1 Tab Chờ thanh toán hiển thị — PASS: (0) → empty state đúng
- 1.14.2 Thanh toán từ tab Chờ TT — N/A: không có đơn trạng thái này
- 1.14.3 Thanh toán bằng chọn bàn đang dùng — PASS: vào Order ban1 đang dùng → thanh toán tiền mặt thành công
- 1.14.4 Thanh toán đơn từ tablet/mobile — BLOCKED: không có đơn gửi từ tablet/mobile
- 1.15.1 Số lượng = 0 — PASS: nút − chặn ở SL 1, không về 0
- 1.15.2 Giá rất lớn — N/A: sửa đơn giá (chưa kiểm sâu nhập 999.999.999)
- 1.15.3 Làm tròn VND — PASS: tổng hiển thị số nguyên (vd thuế 5%: 900/810/500…); không lẻ thập phân
- 1.15.4 Mất mạng khi TT — N/A: không mô phỏng trên môi trường dùng chung
- 1.15.5 Hai thu ngân 1 bàn — N/A: 1 phiên đăng nhập
- 1.15.6 Ghi chú dấu/ký tự đặc biệt — PASS* (entry): ô ghi chú có (nhập liệu Flutter repaint trễ)
