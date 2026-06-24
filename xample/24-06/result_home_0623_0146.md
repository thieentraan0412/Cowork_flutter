# Kết quả kiểm thử — HOME

- Menu: home
- Ngày giờ: 23/06 01:46
- Người/agent thực hiện: Claude
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Thu ngân (Casher) — CN1 — ca đang hoạt động
- Trình duyệt: Chrome (qua tiện ích điều khiển)
- Thư mục ảnh lỗi: `screenshot/0623_0146_home/`

## Ghi chú chung về môi trường kiểm thử
- App nền **Flutter web (canvas)**. Công cụ tự động của phiên **không lưu được ảnh ra đĩa** nên các quan sát/lỗi được mô tả chi tiết bằng chữ kèm số liệu thực tế (giống các phiên trước).
- Một số widget Flutter (đặc biệt **các nút +/- nhỏ trên dòng hóa đơn** và **menu popup "..."**) phản hồi chậm/không ổn định với click tự động; số liệu cập nhật **bất đồng bộ (async) trễ ~1–4s** rồi mới khớp. Về cuối phiên trình duyệt bị **đơ/giật nặng** (ảnh chụp time-out liên tục) nên một số mục được đánh dấu **KHÔNG KIỂM THỬ** (chưa thực hiện đầy đủ trong phiên này), không phải lỗi app.
- Các bộ lọc trạng thái ở Trang chủ là **toggle đa lựa chọn (cộng dồn)**, không phải radio. Số đếm trong ngoặc của các tab trạng thái là **toàn cục** (không đổi theo khu).

---

## 1.1 Sơ đồ bàn

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.1.1 | Hiển thị danh sách bàn theo khu | PASS | Hiện đủ bàn; "Tất cả (15)", "Bàn trống (7)", "Đang sử dụng (7)" |
| 1.1.2 | Lọc "Bàn trống" | PASS | Khi chỉ bật riêng "Bàn trống" → chỉ hiện bàn trống (teal). *Lưu ý: filter cộng dồn — nếu để cả "Đang sử dụng" thì hiện cả 2 loại; dễ nhầm là lỗi* |
| 1.1.3 | Lọc "Đang sử dụng" | PASS | Chỉ hiện 7 bàn đang dùng (cam), khớp số đếm |
| 1.1.4 | Lọc "Chờ xác nhận" | PASS | (0) — hiện empty state "Danh sách bàn thuộc trạng thái 'Chờ xác nhận' rỗng" + nút Tất cả |
| 1.1.5a | Lọc "Chờ thanh toán" | PASS | (0) — empty state đúng; xác nhận filter cộng dồn ("Chờ xác nhận, Chờ thanh toán") |
| 1.1.5b | Lọc theo khu (khu 1 / khu 2) | PASS | Đổi khu 1 → hiện đúng bàn khu 1 (BAN KIEM TRA TEN DAI, BAN_QR…). Số đếm tab trạng thái vẫn là toàn cục |
| 1.1.6 | Đổi số cột hiển thị | PASS | Dropdown có 1/2/3/4/5 cột; đổi sang 2 cột → lưới bố trí lại đúng |
| 1.1.7 | Đổi giao diện (1/2/3) | PASS | Dropdown "Giao diện 1/2/3"; đổi giao diện 1 ↔ 2 → kiểu thẻ bàn thay đổi rõ |
| 1.1.8 | Thẻ bàn hiển thị thông tin | PASS | Đủ: tên bàn, timer, icon hóa đơn + số, icon khách + số, tổng tiền, nhãn trạng thái |
| 1.1.9 | Tổng tiền trên thẻ bàn | PASS | BAN1 thẻ 500.000 = dòng món trong Order (Test điều chuyển 500.000). *Tổng panel cập nhật trễ ~vài giây (async)* |
| 1.1.10 | Trạng thái "Chưa báo bếp" | PASS | BAN1, BAN4 hiện "Chưa báo bếp" trên thẻ |
| 1.1.11 | Nút "Xác nhận" trên thẻ | N/A | Không có đơn "Chờ xác nhận" (0) |
| 1.1.12 | Bấm vào bàn | PASS | Bấm BAN1 → mở màn hình Order của bàn |
| 1.1.13 | Thêm đơn mang về | KHÔNG KIỂM THỬ | Chưa thao tác thẻ "Bàn mang về" trong phiên này |
| 1.1.14 | Số liệu các tab nhất quán | CẦN XEM LẠI | 7 (trống) + 7 (đang dùng) + 0 + 0 = **14** ≠ **15** (Tất cả). Chênh +1 — nhiều khả năng là thẻ "Bàn mang về" được tính vào "Tất cả" nhưng không thuộc nhóm trạng thái nào. Nên xác nhận lại quy ước đếm |

## 1.2 Menu (Thực đơn)

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.2.1 | Hiển thị danh mục món | PASS | Đủ tab: Tất cả, Bán chạy, Món mới, Nước ngọt, Nước chế biến, Nước có còn, Món nước, Món xào, Lẩu, test máy in, banh v1, Test in pc |
| 1.2.2 | Lọc theo danh mục | KHÔNG KIỂM THỬ | Có đủ tab danh mục; chưa bấm lọc từng danh mục trong phiên này |
| 1.2.3 | Tìm món (F1) | PASS | Gõ "tra" → ra "Trà A hỷ" (không phân biệt dấu) + các món chứa "tra" (tran chau, kiemtra…) |
| 1.2.4 | Ẩn/hiện hình ảnh món | PASS | Toggle "Hiện ảnh" bật → lưới hiện ảnh món; tắt → ẩn ảnh |
| 1.2.5 | Đổi số cột hiển thị món | KHÔNG KIỂM THỬ | Có dropdown "Số cột: 4 cột"; chưa đổi trong phiên này |
| 1.2.6 | Phân trang (1/5…) | N/A | Lưới món cuộn liên tục, không có chỉ số phân trang (giống phiên trước) |
| 1.2.7 | Giá món | PASS | Hiển thị đúng định dạng VND (555.000đ, 999.999đ, 9.000đ…) |

## 1.3 Modal tùy chọn món

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.3.1 | Mở modal khi món có tùy chọn | PASS | Bấm "Cơm" → modal "Chọn món kèm theo" (Size, Ngọt, số lượng, ghi chú) |
| 1.3.2 | Chọn thuộc tính (Size, độ ngọt) | PASS | Size S/M/LL, Ngọt Đường 100/50/20%. Đổi chọn được. *Ở "Cơm" tất cả +0đ → không có phụ thu để đối chiếu giá* |
| 1.3.3 | Chọn món thêm | KHÔNG KIỂM THỬ | "Cơm" chỉ có thuộc tính (Size/Ngọt), không có nhóm "Món thêm" để thử |
| 1.3.4 | Tăng/giảm số lượng | PASS | Bấm + → SL 1→2, nút "Thêm vào giỏ hàng" cập nhật 20.000 → 40.000 |
| 1.3.5 | Nhập ghi chú | PASS | Nhập "ít muối @#1" (tiếng Việt có dấu + ký tự đặc biệt) ok |
| 1.3.6 | Bấm "Thêm vào giỏ hàng" | PASS | Cơm (M, Đường 20%, SL2) được thêm vào hóa đơn |
| 1.3.7 | Bấm "Đóng" | PASS | Nút X đóng được modal (cần dùng đúng tâm nút) |
| 1.3.8 | Tùy chọn hiển thị trong dòng món | PASS | Dòng Cơm hiện "M • Đường 20%" + "Ghi chú: ít muối @#1" |
| — | *Quan sát thêm* | LƯU Ý | Sau khi bấm "Thêm vào giỏ hàng", modal **không tự đóng** (phải bấm X) — UX nên xem lại |

## 1.4 Hóa đơn / Giỏ hàng

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.4.1 | Thêm món vào hóa đơn | PASS | Thêm Cơm → dòng xuất hiện, "Tổng tiền hàng (2)" tăng |
| 1.4.2 | Tăng số lượng (+) | PASS | Cơm SL 2→3, thành tiền 40.000→60.000, tổng 540.000→560.000. *Nút nhỏ phản hồi trễ* |
| 1.4.3 | Giảm số lượng (−) | KHÔNG KIỂM THỬ | Nút − nhỏ phản hồi không ổn định với click tự động; chưa xác nhận chắc |
| 1.4.4 | Xóa món (nút thùng rác) | KHÔNG KIỂM THỬ | Chưa thực hiện trong phiên này |
| 1.4.5 | Sửa đơn giá thủ công | KHÔNG KIỂM THỬ | Có icon bút ở cột Đơn giá; chưa thử |
| 1.4.6 | Ghi chú từng món | PASS | Dòng Cơm có "Ghi chú: ít muối @#1" + link "Chỉnh sửa" |
| 1.4.7 | Tổng tiền (tạm tính) | PASS | 500.000 + 60.000 = 560.000 = "Tổng tiền hàng" |
| 1.4.8 | Thuế theo từng món | PASS | Thuế sản phẩm = 5% của Cơm (40.000→2.000; 60.000→3.000); Test điều chuyển thuế 0% |
| 1.4.9 | Thuế theo cả bill | KHÔNG KIỂM THỬ | Chưa cấu hình/đối chiếu thuế cả bill riêng |
| 1.4.10 | Kết hợp thuế món + bill | KHÔNG KIỂM THỬ | — |
| 1.4.11 | Tổng tiền thanh toán | PASS | = Tổng tiền hàng + Thuế (542.000 = 540.000+2.000; 563.000 = 560.000+3.000); Phụ thu/Giảm giá = 0 |
| 1.4.12 | Phụ thu | KHÔNG KIỂM THỬ | Có dòng "Phụ thu" + icon bút; chưa nhập |
| 1.4.13 | Giảm giá | KHÔNG KIỂM THỬ | Chưa thực hiện luồng giảm giá trực tiếp + đối chiếu admin |
| 1.4.15 | Combo / Set menu | KHÔNG KIỂM THỬ | Có "comboo 10" (555.000), "setmenu hoa hồng" (550.000)… chưa thêm để kiểm thành phần |
| 1.4.16 | Chọn khách hàng | KHÔNG KIỂM THỬ | Có dropdown "Chọn thành viên"; chưa thử |
| 1.4.17 | Nhiều hóa đơn / 1 bàn | KHÔNG KIỂM THỬ | Có nút "+" cạnh tab hóa đơn; chưa thử |
| 1.4.18 | Đơn các bàn độc lập | KHÔNG KIỂM THỬ | — |
| 1.4.19 | Hóa đơn trống | KHÔNG KIỂM THỬ | — |
| 1.4.20 | Nhân viên phụ trách | KHÔNG KIỂM THỬ | Đăng nhập "Admin master"; chưa đối chiếu tên trên hóa đơn |

## 1.5 In bếp / Thanh toán

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.5.1 | In phiếu Bếp/Bar (báo bếp) | KHÔNG KIỂM THỬ | Có nút "Báo bếp" (cam); chưa xác nhận do trình duyệt đơ cuối phiên |
| 1.5.2 | Tạm tính | KHÔNG KIỂM THỬ | Có nút "Tạm tính" (xanh lá) |
| 1.5.3 | Thanh toán tiền mặt | KHÔNG KIỂM THỬ | Có nút; không thực hiện để tránh đóng đơn thật |
| 1.5.4 | Thanh toán chuyển khoản | KHÔNG KIỂM THỬ | Có nút "Chuyển khoản" |
| 1.5.5 | Thanh toán quẹt thẻ | KHÔNG KIỂM THỬ | Có nút "Quẹt Thẻ" |
| 1.5.6 | Thanh toán QR tự động | KHÔNG KIỂM THỬ | Có nút "QR Tự động" |
| 1.5.7 | Tiền thừa | KHÔNG KIỂM THỬ | — |
| 1.5.8 | Chặn hóa đơn trống | KHÔNG KIỂM THỬ | — |

## 1.6 Xác nhận đơn (tại bàn / QR / mang về)

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.6.1 | Tab "Chờ xác nhận" hiển thị đơn chờ | N/A | Hiện đang (0) — không có đơn để kiểm; empty state hiển thị đúng |
| 1.6.2 | Xác nhận đơn tại bàn (tablet/mobile) | BLOCKED | Cần thiết bị tablet/mobile gửi đơn (phụ thuộc bên ngoài) |
| 1.6.3 | Xác nhận đơn QR | BLOCKED | Cần khách quét QR bàn đặt món (phụ thuộc bên ngoài) |
| 1.6.4 | Xác nhận đơn mang về | BLOCKED | Cần đơn mang về chờ xác nhận |
| 1.6.5 | Từ chối đơn | BLOCKED | Cần đơn chờ xác nhận |
| 1.6.6 | Tìm kiếm/chọn bàn cần xác nhận | BLOCKED | Cần đơn chờ xác nhận |
| 1.6.7 | Sau xác nhận, số đếm giảm | BLOCKED | Cần đơn chờ xác nhận |

## 1.7 Gửi bếp

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.7.1 | Gửi bếp sau khi chọn món | KHÔNG KIỂM THỬ | Có nút "Báo bếp"; chưa xác nhận do trình duyệt đơ cuối phiên |
| 1.7.2 | Món chưa gửi bếp | PASS | Món mới thêm hiện nhãn "Chờ báo bếp" trên dòng + thẻ bàn hiện "Chưa báo bếp" |
| 1.7.3 | Gửi bếp khi giỏ trống | KHÔNG KIỂM THỬ | — |
| 1.7.4 | Gửi bếp chỉ áp món mới thêm | KHÔNG KIỂM THỬ | — |

## 1.8 Chuyển bàn

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.8.1 – 1.8.9 | Toàn bộ chức năng chuyển bàn | KHÔNG KIỂM THỬ | Truy cập được qua menu "..." → "Chuyển bàn", nhưng chưa chạy đủ luồng (trình duyệt đơ cuối phiên) |

## 1.9 Gộp bàn

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.9.1 – 1.9.11 | Toàn bộ chức năng gộp bàn | KHÔNG KIỂM THỬ | Có mục "Gộp bàn" trong menu "..."; chưa chạy đủ luồng |

## 1.10 Tách / ghép đơn

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.10.1 – 1.10.30 | Toàn bộ chức năng tách/ghép | KHÔNG KIỂM THỬ | Có mục "Tách/Ghép đơn" trong menu "..."; chưa chạy đủ luồng |

## 1.11 Hàng tặng

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.11.1 – 1.11.6 | Toàn bộ chức năng hàng tặng | KHÔNG KIỂM THỬ | Có mục "Hàng tặng" trong menu "..."; chưa chạy đủ luồng |

## 1.12 Áp dụng khuyến mãi

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.12.1 | Mở chức năng khuyến mãi trên đơn | PASS | Menu "..." → "Khuyến mãi" → modal "Đơn hàng đủ điều kiện…", hiện CTKM "GIAM GIA" |
| 1.12.2 | Áp khuyến mãi vào đơn | KHÔNG KIỂM THỬ | Chọn được "GIAM GIA" ("Đã chọn: 1 chương trình") nhưng bước "Áp dụng" không hoàn tất do trình duyệt đơ |
| 1.12.3 | CTKM hết hiệu lực | KHÔNG KIỂM THỬ | — |
| 1.12.4 | Đơn không thỏa điều kiện | KHÔNG KIỂM THỬ | — |
| 1.12.5 | Bỏ khuyến mãi đã áp | KHÔNG KIỂM THỬ | — |
| 1.12.6 | Chưa mở ca | N/A | Ca đang mở; không kiểm được trường hợp chưa mở ca |

## 1.13 Hủy đơn

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.13.1 – 1.13.5 | Toàn bộ chức năng hủy đơn | KHÔNG KIỂM THỬ | Nút X cạnh tab hóa đơn có hiển thị; chưa thực hiện hủy trong phiên này |

## 1.14 Thanh toán đơn hàng (qua Chờ thanh toán)

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.14.1 | Tab "Chờ thanh toán" hiển thị đơn chờ | N/A | Hiện (0) — không có đơn; empty state đúng |
| 1.14.2 | Thanh toán từ tab Chờ thanh toán | KHÔNG KIỂM THỬ | Không có đơn chờ thanh toán |
| 1.14.3 | Thanh toán bằng chọn bàn đang dùng | KHÔNG KIỂM THỬ | Không thực hiện thanh toán thật |
| 1.14.4 | Thanh toán đơn từ tablet/mobile | BLOCKED | Cần thiết bị bên ngoài |

## 1.15 Trường hợp đặc thù & lỗi

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.15.1 | Số lượng món = 0 | KHÔNG KIỂM THỬ | — |
| 1.15.2 | Giá rất lớn (999.999.999đ) | KHÔNG KIỂM THỬ | Có món "comboo hoa hồng" 999.999đ hiển thị đúng; chưa thử giá cực lớn |
| 1.15.3 | Làm tròn tiền VND | PASS | Thuế/tổng hiển thị số nguyên (2.000, 3.000…), không có số lẻ thập phân |
| 1.15.4 | Mất mạng khi thanh toán | BLOCKED | Không thể ngắt mạng qua công cụ tự động |
| 1.15.5 | Hai thu ngân cùng 1 bàn | BLOCKED | Cần 2 thiết bị/phiên đồng thời |
| 1.15.6 | Ghi chú có dấu / ký tự đặc biệt | PASS | "ít muối @#1" lưu & hiển thị đúng, không lỗi ký tự |

---

## Tổng hợp

- **PASS: 24**
- **CẦN XEM LẠI: 1** (1.1.14 — tổng các tab = 14 ≠ "Tất cả" 15, chênh +1)
- **N/A: 5** (1.1.11, 1.6.1, 1.12.6, 1.14.1, và empty-state các tab 0)
- **BLOCKED: 9** (phụ thuộc thiết bị ngoài/đặt QR/mạng/đa thiết bị: 1.6.2–1.6.7, 1.14.4, 1.15.4, 1.15.5)
- **KHÔNG KIỂM THỬ (chưa hoàn tất trong phiên): phần lớn 1.5, 1.7–1.11, 1.13, một phần 1.4 và 1.12** — do hai nguyên nhân: (1) tránh thao tác phá hủy dữ liệu thật (thanh toán/hủy), (2) trình duyệt Flutter web đơ/giật nặng về cuối phiên khiến tương tác không ổn định.

### Lỗi / điểm cần lưu ý
1. **1.1.14 — Số liệu tab chưa khớp tổng**: Bàn trống (7) + Đang sử dụng (7) + Chờ xác nhận (0) + Chờ thanh toán (0) = 14, nhưng "Tất cả" = 15. Chênh +1 (khả năng do thẻ "Bàn mang về"). Cần xác nhận quy ước đếm. *(Ảnh: `screenshot/0623_0146_home/` — mô tả bằng chữ)*
2. **Modal "Chọn món kèm theo" không tự đóng** sau khi bấm "Thêm vào giỏ hàng" (phải bấm X thủ công) — điểm UX nên xem lại.
3. **Hiệu năng**: app phản hồi/cập nhật tổng tiền **bất đồng bộ trễ vài giây**; khi thao tác liên tục, renderer **đơ/giật nặng**. Cần kiểm tra lại hiệu năng trên thiết bị thật (có thể một phần do môi trường tự động).

> Khuyến nghị: chạy bổ sung một phiên nữa (môi trường ổn định hơn) để hoàn tất các mục KHÔNG KIỂM THỬ: 1.4 (xóa/sửa giá/phụ thu/giảm giá/combo/khách hàng/đa hóa đơn), 1.5 (báo bếp/tạm tính/các hình thức thanh toán), 1.7 gửi bếp, 1.8–1.10 chuyển/gộp/tách bàn, 1.11 hàng tặng, 1.12 áp/bỏ khuyến mãi, 1.13 hủy đơn.
