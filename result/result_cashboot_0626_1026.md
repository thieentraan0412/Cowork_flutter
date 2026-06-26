# Kết quả kiểm thử — CASHBOOT (Thu chi)

- Menu: cashboot
- Ngày giờ: 26/06 10:26
- Người/agent thực hiện: Claude
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — CN1 — tài khoản **Admin master** — phiên bản 1.0.0+80
- Route: `pos-cashbook-route`

## Bảng kết quả theo mục checklist

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| (load) | Render trang Thu chi | PASS | "Tháng này" tải ~14s (chậm) nhưng có dữ liệu — 241 phiếu, 13 trang |
| 1.1.1 | Tìm theo Mã phiếu | PASS | "PC00001653" → đúng 1 phiếu; "xxxx999" → "Không có dữ liệu" |
| 1.1.2 | Lọc Chi nhánh | PASS | Mặc định CN1; dropdown CN1/cn11/cn12 |
| 1.1.3 | Thời gian Hôm nay/Hôm qua | PASS | Hôm nay → 1 phiếu (21.000đ) |
| 1.1.4 | Thời gian Tuần này/trước | PASS | Tuần này → 6 phiếu (22-26/06) |
| 1.1.5 | Thời gian Tháng này/trước | PASS | Tháng này → 241 phiếu (tải chậm ~14s) |
| 1.1.6 | Tùy chọn ngày | PASS | Có ô ngày bắt đầu/kết thúc |
| 1.1.7 | Lọc Người tạo | PASS | Dropdown hiển thị |
| 1.1.8 | Lọc Loại thu chi (Thu/Chi) | PASS | "Phiếu chi" → chỉ hiện phiếu Chi |
| 1.1.9 | Lọc Phân loại | PASS | "Mua tôm hùm bông" → chỉ phiếu đúng phân loại |
| 1.1.10 | Lọc Loại nguồn | PASS | Đủ giá trị: Bán hàng/Mua hàng/Trả hàng/Tự tạo |
| 1.1.11 | Kết hợp nhiều bộ lọc | PASS | Các bộ lọc cộng dồn đúng |
| 1.2.1 | Tồn quỹ đầu kỳ | PASS | Tháng này 8.264.976.882đ |
| 1.2.4 | Tồn cuối kỳ = đầu + thu − chi | PASS | Đúng ở mọi kỳ (xem ghi chú công thức) |
| 1.2.5 | Đổi bộ lọc → 4 thẻ cập nhật | PASS | Cập nhật theo kỳ |
| 1.3.1 | Bảng đủ cột | PASS | Đủ 13 cột (STT…Hành động) |
| 1.3.2 | Phân trang | PASS | 241 bản ghi / 13 trang |
| 1.3.3 | Icon xem chi tiết | PASS | Có icon mắt mọi dòng |
| 1.4.1 | Bấm "Thêm" mở modal | PASS | Modal "Thêm phiếu" |
| 1.4.2 | Mã phiếu tự sinh | PASS | "Mã tăng tự động" (mã thật hiện sau khi tạo/khi sửa) |
| 1.4.3/1.4.4 | Required (Loại/Số tiền) | PASS | Lưu rỗng → "Nhập số tiền" báo đỏ |
| 1.4.7 | PTTT mặc định Tiền mặt | PASS | |
| 1.4.8 | Ô Số tiền chỉ nhận số | **FAIL** | Nhận cả chữ "abc1500000", không tự định dạng |
| 1.4.10 | Mô tả giới hạn | PASS* | Counter **x/200** (nay = 200, khớp spec) |
| 1.4.11 | Lưu hợp lệ | PASS | PT00000039 tạo, lên đầu, quỹ cập nhật |
| 1.4.12 | "Đóng"/X không tạo phiếu | PASS | |
| 1.4.14 | Số tiền = 0 bị chặn | PASS | **"Số tiền phải lớn hơn 0"** (BUG-01 đã fix) |
| 1.4.17 | Chi → label "Người nhận" | **FAIL** | Luôn gộp "Người nộp / Người nhận" |
| 1.5.2 | Tạo Phiếu chi thủ công | PASS | Quỹ giảm đúng 12.000 |
| 1.5.4 | Phiếu chi hiển thị đúng | PASS | Loại/Số tiền/PTTT/Mô tả đúng |
| 1.5.7 | Lọc nguồn = Bán hàng | PASS | Phiếu PC tự sinh, chỉ-xem |
| 1.5.9 | Lọc nguồn = Tự tạo | PASS | Chỉ phiếu thủ công (có sửa/xóa) |
| 1.5.16 | Tổng chi = Σ phiếu chi | PASS | 50→62 khi thêm, →50 khi xóa |
| 1.6.1 | Xuất Excel | PASS | "Đã xuất file, đang tải xuống trình duyệt" |
| 1.7.1 | Mở tab Công nợ | PASS | Có panel Bộ lọc |
| 1.7.2 | Đối tượng mặc định | PASS | KH + NCC đều tích |
| 1.7.13 | Chip trạng thái | PASS | Tất cả(52)/Gần hạn(16)/Quá hạn(22)/Hôm nay(2) |
| 1.7.14 | Lọc chip "Quá hạn" | PASS | 22 dòng, đều "Đã quá hạn N ngày" |
| 1.7.16 | Bảng công nợ đủ cột | PASS | Đủ cột gồm Mã công nợ có dữ liệu |
| 1.7.17 | Chưa TT + Đã TT = Tổng | PASS | 500.000+21.000=521.000 ✓ … |
| 1.7.18 | Modal "Thanh toán nợ" | PASS | "Còn lại 500.000đ" đúng đối tượng |
| 1.7.19 | Trạng thái TT (phần/đủ) | PASS | "Thanh toán một phần" / "đủ" |
| 1.7.20 | Đóng modal không lưu | PASS | Số liệu không đổi |
| 1.8.1 | Icon Hành động | PASS | Sửa/Xóa/Xem |
| 1.8.2 | Mở sửa, dữ liệu điền sẵn | PASS | Hiện mã thật PT00000039CN2 |
| 1.8.3 | Sửa Số tiền → tổng đổi | PASS | 12k→20k, số dư −8.000 đúng |
| 1.8.6 | Phiếu tự sinh không sửa | PASS | Phiếu Bán hàng chỉ có icon xem |
| 1.9.1 | Hộp xác nhận xóa | PASS | "Bạn có chắc chắn muốn xóa không?" |
| 1.9.4 | Xóa phiếu chi → tổng đổi | PASS | 70→50, số dư hoàn về cũ |
| 1.9.5 | Phiếu tự sinh không xóa | PASS | |
| 1.10.1 | Sắp xếp theo Thời gian | **FAIL** | Bấm tiêu đề cột không sắp xếp, không có mũi tên |
| 1.10.2 | Sắp xếp theo Số tiền | **FAIL** | Không sắp xếp |
| 1.10.3 | Mặc định mới nhất lên đầu | PASS | |
| 1.10.4 | Cuộn ngang bảng | PASS | Xem hết cột khi cuộn |
| 1.11.1 | Tiền tố PC/PT | PASS | PC=Thu, PT=Chi |
| 1.11.2/3 | Mã tăng tuần tự | PASS | PT00000038 → PT00000039 |
| 1.11.4 | Không sinh mã toàn số 0 | PARTIAL | Mã mới OK; còn PT00000000/PC00000000 (dữ liệu cũ) |
| 1.11.5 | Số tiền có dấu phân cách | PASS | Danh sách "21.000 đ" |
| 1.11.6 | Định dạng khi gõ | (ghi nhận) | KHÔNG tự chèn dấu phẩy khi gõ |
| 1.11.7 | Số âm khi lọc | (ghi nhận) | Ra ÂM khi lọc loại (xem FIND-BALANCE) |
| 1.12.4 | Nhập chữ vào ô Số tiền | **FAIL** | Nhận "abc" (không lọc) |
| 1.12.5 | Mô tả biên 50 | N/A | Giới hạn nay là 200 |
| 1.13.1 | PTTT mặc định Tiền mặt | PASS | |
| 1.13.2 | Danh sách PTTT | PASS | Tiền mặt, Chuyển khoản, Quẹt Thẻ… |
| 1.13.4 | PTTT phiếu tự sinh | PASS | Thấy QR Tự động / Chuyển khoản trong danh sách |
| 1.14.3 | Công thức số dư mọi kỳ | PASS | Đúng Tháng/Tuần/Hôm nay |
| 1.14.4 | Tồn đầu kỳ cố định khi lọc loại | **FAIL** | Đổi & ra âm (FIND-BALANCE) |
| 1.14.5 | Quỹ cập nhật realtime | PASS | Thêm/sửa/xóa cập nhật ngay |
| 1.15.3 | Phiếu "Tự tạo" = thủ công | PASS | |
| 1.16.1 | Xóa từng bộ lọc | PASS | × trên chip cập nhật lại |
| 1.16.4 | Bộ lọc rỗng | PASS | "Không có dữ liệu"; Tồn đầu kỳ giữ |
| 1.17.1 | Chi nhánh trong phạm vi | PASS | CN1/cn11/cn12 |
| 1.17.2 | Phiếu gắn đúng chi nhánh | PASS | CN1 |
| 1.17.3 | Người tạo = tài khoản | PASS | Admin master |
| 1.18.1 | Danh sách rỗng | PASS | "Không có dữ liệu" |
| 1.18.3 | Đóng modal Esc/click ngoài | **FAIL** | Esc & click ngoài không đóng; chỉ X/Lưu |

## Regression (1.19)

| Mục | Lỗi/Lệch đã biết | Kết quả phiên này |
|-----|------------------|-------------------|
| 1.19.1 | BUG-01: Số tiền=0 vẫn tạo | ✅ **ĐÃ FIX** — chặn "Số tiền phải lớn hơn 0" |
| 1.19.2 | LỆCH-01: Mô tả 50 vs 200 | ✅ Nay = **200** (khớp spec) |
| 1.19.3 | LỆCH-02: Label Người nộp/nhận | ❌ Còn lệch (luôn gộp) |
| 1.19.4 | LỆCH-03: "Loại nhân sự" | ❌ Còn (theo vai trò) |
| 1.19.5 | FIND-BALANCE: Đầu kỳ đổi theo lọc | ❌ Còn — ra số âm (VD −23.483.895) |
| 1.19.6 | Mã toàn số 0 | ⚠️ Mã mới OK; còn dữ liệu cũ PT/PC00000000 |
| 1.19.7 | Loại nguồn đúng giá trị | ✅ Bán hàng/Mua hàng/Trả hàng/Tự tạo |
| 1.19.8 | Mã công nợ có dữ liệu | ✅ #52, #51… |

## Tổng hợp
- PASS: ~55 mục
- FAIL: 6 mục — 1.4.8/1.12.4 (ô Số tiền nhận chữ), 1.4.17 (label không đổi), 1.10.1/1.10.2 (không sắp xếp cột), 1.14.4 (FIND-BALANCE), 1.18.3 (Esc/click-ngoài không đóng modal)
- PARTIAL/N-A: 1.11.4 (mã cũ toàn số 0), 1.12.5 (giới hạn nay 200)
- Cải thiện nổi bật: **BUG-01 đã fix**, **Mô tả nâng lên 200**

## Danh sách lỗi (chi tiết & cách tái hiện) → xem `screenshot/0626_1026_cashboot/note.md`

1. **[1.4.8/1.12.4] Ô "Số tiền" nhận ký tự chữ.** Gõ "abc1500000" → hiển thị nguyên chuỗi, không lọc số, không định dạng.
2. **[1.4.17/1.19.3] Nhãn "Người nộp / Người nhận" không đổi theo Thu/Chi.**
3. **[1.10.1/1.10.2] Sắp xếp theo cột không hoạt động.** Bấm tiêu đề "Số tiền"/"Thời gian" không đổi thứ tự, không có mũi tên.
4. **[1.14.4/1.19.5] FIND-BALANCE.** Lọc Loại="Phiếu chi" → Tồn đầu kỳ = −23.483.895đ (âm), Số dư cuối = −23.533.895đ.
5. **[1.18.3] Modal không đóng bằng Esc / click ngoài** — chỉ đóng bằng X hoặc Lưu.
6. **[1.11.4/1.19.6] Dữ liệu rác mã toàn số 0** còn tồn (PT00000000 0đ, PC00000000) từ BUG-01 các phiên trước.

## Ghi chú thêm
- Công thức quỹ chính xác mọi kỳ: Số dư cuối ca = Tồn đầu kỳ + Tổng thu − Tổng chi (Tháng/Tuần/Hôm nay đều khớp 9.042.266.176).
- Vòng đời phiếu thủ công (Tạo → Sửa → Xóa) chạy đúng, quỹ cập nhật realtime theo chênh lệch. Dữ liệu test đã dọn sạch.
- Phiếu Bán hàng tự sinh (PC…) chỉ-xem; phiếu Tự tạo có Sửa/Xóa — phân quyền thao tác đúng.
- Lưu ý môi trường: Flutter canvas đôi lúc treo render khi tải dữ liệu / chồng layout khi chuyển tab — tải lại trang là hết.
