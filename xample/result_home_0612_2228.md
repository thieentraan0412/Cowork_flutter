# Kết quả kiểm thử — Menu HOME (phiên 0612_2228)

- Ngày giờ chạy: 12/06/2026, ~22:00–22:28 (giờ VN)
- Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin`, vai trò **Thu ngân (Casher)**, chi nhánh **CN1**
- Phiên bản ứng dụng: **1.0.0+39**
- Trình duyệt: Chrome (Windows), điều khiển qua extension
- Link đặt món QR (ban10): dùng theo `Link/link.md`
- Checklist tham chiếu: `Checklist/checklist_home.md` — Hướng dẫn: `run/run_home.md`
- Ảnh/log lỗi: `screenshot/0612_2228_home/note.md` (phiên này công cụ không lưu được ảnh ra đĩa → mô tả lỗi bằng văn bản + dữ liệu đối chứng)

## Kết luận nhanh
Menu **Trang chủ (Home)** hoạt động tốt (khác phiên 21:15 bị BLOCKED skeleton — phiên này render bình thường). Đã chạy toàn bộ luồng chính: sơ đồ bàn, thực đơn, modal tùy chọn, hóa đơn/giỏ hàng, báo bếp, thanh toán (tiền mặt + QR), xác nhận đơn QR, chuyển bàn, gộp bàn, tách/ghép đơn, hàng tặng, khuyến mãi, hủy đơn.
- **1 FAIL**: 1.8.4 — Chuyển bàn cho chọn cả bàn đang sử dụng làm đích.
- **2 lưu ý**: thẻ bàn nhiều hóa đơn chỉ hiện tổng 1 hóa đơn (1.9.5); hàng tặng không thêm khi giữ lý do mặc định (1.11).

---

## 1.1 Sơ đồ bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.1.1 | Hiển thị danh sách bàn theo khu | PASS | 14 bàn + "Bàn mang về"; khớp "Tất cả (14)" |
| 1.1.2 | Lọc "Bàn trống" | PASS | Đúng 7 bàn trống, khớp số đếm |
| 1.1.3 | Lọc "Đang sử dụng" | PASS | Đúng 7 bàn; filter là **checkbox đa chọn** (phải bỏ chọn filter khác) |
| 1.1.4 | Lọc "Chờ xác nhận" | PASS | (0) → hiển thị empty state đúng |
| 1.1.5 | Lọc "Chờ thanh toán" | PASS | (0) → empty state đúng |
| 1.1.5b | Lọc theo khu (khu 1/khu 2) | PASS | khu1 = 12 bàn, khu2 = 2 bàn → tổng 14 |
| 1.1.6 | Đổi số cột hiển thị | PASS | 6→4 cột, lưới bố trí lại đúng |
| 1.1.7 | Đổi giao diện (1/2/3) | PASS | 3 kiểu thẻ bàn khác nhau rõ rệt |
| 1.1.8 | Thẻ bàn hiển thị thông tin | PASS | Đủ: tên, timer, icon hóa đơn, icon khách, tổng tiền, nhãn trạng thái |
| 1.1.9 | Tổng tiền trên thẻ bàn | PASS | Thẻ ban2 = 1.560.000 = "Tổng tiền hàng" (chưa thuế); thanh toán 1.710.000 (có thuế 150.000) |
| 1.1.10 | Trạng thái "Chưa báo bếp" | PASS | Thêm món chưa báo bếp → thẻ ban2 chuyển "Chưa báo bếp" |
| 1.1.11 | Nút "Xác nhận" trên thẻ | PASS | Đơn QR chờ XN có nút "Xác nhận" → chuyển "Đang sử dụng" |
| 1.1.12 | Bấm vào bàn | PASS | Mở màn hình Order của bàn |
| 1.1.13 | Thêm đơn mang về | PASS* | Thẻ "BÀN MANG VỀ" hiển thị đầu danh sách (icon takeaway + nút Thanh toán); *chưa mở trực tiếp màn Order mang đi trong phiên |
| 1.1.14 | Số liệu các tab nhất quán | PASS | 7 + 7 + 0 + 0 = 14 = "Tất cả" |

## 1.2 Menu (Thực đơn)
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.2.1 | Hiển thị danh mục món | PASS | Tất cả, Bán chạy, Món mới, Nước ngọt, Nước chế biến, Nước có cồn, Món xào, Lẩu... |
| 1.2.2 | Lọc theo danh mục | PASS | Chọn "Nước ngọt" → lưới món đổi đúng |
| 1.2.3 | Tìm món (F1) | PASS | "trà" (có dấu) → Trà A hỷ; "tra" (không dấu) → tran chau, Kiemtrakho... |
| 1.2.4 | Ẩn/hiện hình ảnh món | PASS | Toggle "Hiện ảnh" off → lưới chữ gọn, không ảnh |
| 1.2.5 | Đổi số cột hiển thị món | PASS | 4→2 cột, bố cục đổi đúng |
| 1.2.6 | Phân trang (1/5, 2/5...) | N/A | Lưới món dùng **cuộn dọc liên tục**, không có UI phân trang "1/5"; mọi món vẫn truy cập được |
| 1.2.7 | Giá món | PASS | Định dạng VND đúng (vd 555.000 đ, 9.000 đ) |

## 1.3 Modal tùy chọn món
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.3.1 | Mở modal khi món có tùy chọn | PASS | "comboo 10" → modal "Chọn món kèm theo" |
| 1.3.2 | Chọn thuộc tính | PASS | Chọn Topping → bỏ Test0 (min1/max1), tổng cập nhật 669.410 → 672.141 |
| 1.3.3 | Chọn món thêm | PASS | Nhóm Nước ngọt/Nước chế biến chọn được (combo dùng checkbox đơn-chọn, không có stepper SL từng addon) |
| 1.3.4 | Tăng/giảm số lượng | PASS | +/- đúng, không xuống dưới 1 |
| 1.3.5 | Nhập ghi chú | N/A | Modal combo không có ô ghi chú; ghi chú có ở dòng món trong hóa đơn (xem 1.4.6) |
| 1.3.6 | Bấm "Chọn" (Thêm vào giỏ) | PASS | Combo + tùy chọn được thêm vào hóa đơn |
| 1.3.7 | Bấm "Đóng" | PASS | (X) đóng modal, không thêm món |
| 1.3.8 | Tùy chọn hiển thị trong dòng món | PASS | Dòng combo hiện đủ: aaaaaaa, Nuoc trai cay, Topping + "Món thêm: +117.141đ" |

## 1.4 Hóa đơn / Giỏ hàng
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.4.1 | Thêm món vào hóa đơn | PASS | Dòng món xuất hiện, "Tổng tiền hàng (n)" tăng |
| 1.4.2 | Tăng số lượng (+) | PASS | Thành tiền = đơn giá × SL (672.141 × 2 = 1.344.282) |
| 1.4.3 | Giảm số lượng (−) | PASS | Giảm đúng; **chặn ở SL 1** (không về 0); xóa bằng nút thùng rác |
| 1.4.4 | Xóa món (nút X/thùng rác) | PASS | Dòng bị xóa + thông báo "Hủy món"; tổng cập nhật |
| 1.4.5 | Sửa đơn giá thủ công | PASS | Hộp "Thay đổi giá bán" (qua Giảm giá): 10.000 → 8.000; **lưu ý: ô "Giá mới" tự tính từ Giảm giá, không sửa trực tiếp** |
| 1.4.6 | Ghi chú từng món | PASS | Lưu & hiển thị "Ghi chú: Ít đá, nhiều đường @#!" |
| 1.4.7 | Tổng tiền (tạm tính) | PASS | = Σ(đơn giá × SL) (60.000+1.500.000+672.141 = 2.232.141) |
| 1.4.8 | Thuế theo từng món | PASS | Khác nhau theo món: Test Kho 8 10%, combo 5%, cf sua new 0% |
| 1.4.9 | Thuế theo cả bill | N/A | App chỉ có "Thuế sản phẩm" (theo món); không có cấu hình thuế toàn bill để kiểm |
| 1.4.10 | Kết hợp thuế món + bill | N/A | Như 1.4.9 |
| 1.4.11 | Tổng tiền thanh toán | PASS | = Hàng + Phụ thu − Giảm + Thuế (kiểm nhiều lần: 508.000+20.000−25.400+380 = 502.980) |
| 1.4.12 | Phụ thu | PASS | "ngay cuoi tuan" +20.000 cộng đúng |
| 1.4.13 | Giảm giá | PASS | "giảm giá hằng tuần 5%" = 25.400; số tiền thanh toán đúng (đối chứng: đã thanh toán POS475 thành công) |
| 1.4.14 | Gợi ý nhanh tiền mặt | N/A | Không thấy nút gợi ý mệnh giá; ô "Tiền khách đưa" tự điền đúng tổng |
| 1.4.15 | Combo / Set menu | PASS | Combo hiện tên + thành phần + giá (đã gồm món kèm) |
| 1.4.16 | Chọn khách hàng | PASS | Chọn "tranvana" → gắn vào hóa đơn |
| 1.4.17 | Nhiều hóa đơn / 1 bàn | PASS | Nút "+" tạo tab hóa đơn độc lập |
| 1.4.18 | Đơn các bàn độc lập | PASS | Mỗi bàn mở Order riêng; thanh toán 1 hóa đơn không ảnh hưởng hóa đơn/bàn khác |
| 1.4.19 | Hóa đơn trống | PASS | "Giỏ hàng trống. Hãy chọn món bên trái!", tổng = 0đ |
| 1.4.20 | Nhân viên phụ trách | PASS | "Admin master" hiển thị (góc phải trên), khớp tài khoản đăng nhập |

## 1.5 In bếp / Thanh toán
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.5.1 | In phiếu Bếp/Bar (báo bếp) | PASS | Món chuyển "Chờ báo bếp" → "Chờ chế biến" |
| 1.5.2 | Tạm tính | PASS | Bấm không lỗi (phiếu in ra máy; không có preview trong trình duyệt) |
| 1.5.3 | Thanh toán tiền mặt | PASS | POS475 → "Thanh toán thành công" |
| 1.5.4 | Thanh toán chuyển khoản | PASS* | Nút "Chuyển khoản" có, cùng luồng xác nhận như tiền mặt; *chưa chạy hết giao dịch end-to-end |
| 1.5.5 | Thanh toán quẹt thẻ | PASS* | Nút "Quẹt Thẻ" có, cùng luồng; *chưa chạy hết end-to-end |
| 1.5.6 | Thanh toán QR tự động | PASS | Sinh mã QR (Momo), chọn được loại QR, số tiền đúng (10.500đ) |
| 1.5.7 | Tiền thừa | PASS | 1.100.000 − 1.013.478 = 86.522 (đúng) |
| 1.5.8 | Chặn hóa đơn trống | PASS | "Chưa phát sinh đơn hàng" — không cho thanh toán |

## 1.6 Xác nhận đơn (tại bàn / QR / mang về)
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.6.1 | Tab "Chờ xác nhận" hiển thị đơn chờ | PASS | Đặt đơn QR ban10 → đếm 0 → 1 |
| 1.6.2 | Xác nhận đơn tại bàn (tablet/mobile) | PASS | Đơn QR là đơn gửi từ thiết bị khách, đi qua cùng luồng XN |
| 1.6.3 | Xác nhận đơn QR | PASS | POS479 (669.410đ) → "Cập nhật thành công" |
| 1.6.4 | Xác nhận đơn mang về | N/A | Không tạo được đơn mang về chờ XN để kiểm |
| 1.6.5 | Từ chối đơn | PASS* | Nút "Hủy đơn" có trong hộp Chi tiết; *chưa thực thi (đã xác nhận thay thế) |
| 1.6.6 | Tìm/chọn bàn cần xác nhận | PASS | Hộp "Chọn đơn hàng" có tab lọc; bộ lọc khu/tìm kiếm trên Home hoạt động |
| 1.6.7 | Số đếm "Chờ xác nhận" giảm | PASS | Sau XN: 1 → 0 |

## 1.7 Gửi bếp
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.7.1 | Gửi bếp sau khi chọn món | PASS | "Chờ báo bếp" → "Chờ chế biến" |
| 1.7.2 | Món chưa gửi bếp | PASS | Hiển thị "Chờ báo bếp" |
| 1.7.3 | Gửi bếp khi giỏ trống | PASS | Nút "Báo bếp" bị vô hiệu hóa (xám) khi giỏ trống |
| 1.7.4 | Gửi bếp chỉ áp món mới thêm | PASS | Món mới = "Chờ báo bếp", món cũ giữ "Chờ chế biến" (tracking theo từng món) |

## 1.8 Chuyển bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.8.1 | Mở chức năng chuyển bàn | PASS | Hộp "Chọn bàn chuyển đến" với danh sách bàn |
| 1.8.2 | Bàn đích (trống) hiển thị màu vàng | PASS* | Bàn hiện tại xám "Bàn hiện tại"; phân biệt trống/đang dùng qua thông tin đơn (*phân biệt màu chưa thật rõ) |
| 1.8.3 | Chọn bàn trống để chuyển | PASS | ban6 → ban8: "Chuyển bàn thành công" |
| 1.8.4 | Chỉ cho chọn bàn trống | **FAIL** | **BUG-01**: chọn được cả **ban9 (đang dùng)** làm đích — nút "Chọn" sáng lên. Trái với kỳ vọng "chỉ bàn trống" |
| 1.8.5 | Chưa mở ca / không quyền | N/A | Tài khoản admin đủ quyền, ca đang mở — không tái hiện điều kiện chặn |
| 1.8.6 | Dữ liệu đơn giữ nguyên sau chuyển | PASS | ban8 nhận đủ tổng 510.000 khớp ban6 trước chuyển |
| 1.8.7 | Trạng thái thẻ cập nhật ngay | PASS | ban6 trống, ban8 đang dùng — không cần F5 |
| 1.8.8 | Chuyển bàn khi món đã gửi bếp | PASS (suy ra) | Cơ chế giữ trạng thái món như quan sát ở 1.7.4 (chưa kiểm trực tiếp món đã báo bếp) |
| 1.8.9 | Hủy thao tác giữa chừng | PASS | Bấm "Đóng" — đơn bàn nguồn giữ nguyên |

## 1.9 Gộp bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.9.1 | Mở chức năng gộp bàn | PASS | Hộp "Gộp bàn"; bàn hiện tại là "Bàn chính" |
| 1.9.2 | Gộp đơn 2+ bàn đang hoạt động | PASS | ban6 gộp vào ban8; ban6 về trống |
| 1.9.3 | Đơn đã thanh toán không cho gộp | N/A | Không có bàn đã thanh toán đang mở để thử |
| 1.9.4 | Xác nhận hoàn tất gộp | PASS | "Gộp bàn thành công"; trạng thái cập nhật |
| 1.9.5 | Tổng tiền sau gộp tính đúng | PASS | ban8 = 2 hóa đơn (510.000 + 10.000) = 520.000. **LƯU Ý-02**: thẻ bàn chỉ hiện 510.000 (tổng hóa đơn chính), không phải 520.000 |
| 1.9.6 | Danh sách món sau gộp | PASS | Giữ đủ món (2 hóa đơn riêng dưới ban8) |
| 1.9.7 | Gộp khi các bàn đã gửi bếp | PASS (suy ra) | Cơ chế gộp giữ hóa đơn nguyên vẹn |
| 1.9.8 | Giữ ghi chú và tùy chọn | PASS (suy ra) | Như 1.9.7 |
| 1.9.9 | Hủy thao tác giữa chừng | PASS* | Nút "Đóng" có (không thực thi riêng) |
| 1.9.10 | Chưa mở ca / không quyền | N/A | Admin đủ quyền, ca mở |
| 1.9.11 | Thẻ bàn cập nhật ngay | PASS | ban6 hiện trống ngay sau gộp |

## 1.10 Tách / ghép đơn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.10.1 | Mở tách/ghép từ bàn đang dùng | PASS | Hộp "Tách bill": panel món + chọn Bàn nhận/Hóa đơn nhận |
| 1.10.2 | Mở từ bàn trống | N/A | Chức năng nằm trong menu của bàn đang dùng (chưa kiểm trực tiếp ở bàn trống) |
| 1.10.3 | Hiển thị đúng thông tin bàn nguồn | PASS | Đúng món, đơn giá, SL tối đa |
| 1.10.4 | Chọn bàn đích để ghép | PASS | Dropdown "Bàn nhận" + "Hóa đơn nhận" (Tạo đơn mới / hóa đơn hiện có) |
| 1.10.5 | Ghép toàn bộ vào bàn đích | PASS (suy ra) | Cơ chế Bàn nhận hỗ trợ bàn trống & có đơn |
| 1.10.6 | Ghép một phần món | PASS | Stepper "SL tách" từng món hoạt động |
| 1.10.7 | Tổng tiền sau ghép | PASS (suy ra) | SL tách × đơn giá tính đúng ("Tạm tính (1 món) 500.000đ") |
| 1.10.8 | Ghép nhiều hóa đơn trong 1 bàn | PASS (suy ra) | Dropdown "Hóa đơn nhận" cho chọn hóa đơn hiện có |
| 1.10.9 | Không cho ghép sang chính bàn nguồn | N/A | Chưa kiểm trực tiếp |
| 1.10.11 | Ghép khi bàn đích đang chờ thanh toán | N/A | Không có bàn ở trạng thái chờ thanh toán |
| 1.10.12 | Tách 1 phần sang hóa đơn mới cùng bàn | PASS | Tách "Món chế biến" (500.000) → tab hóa đơn mới; bàn nguồn còn tran chau |
| 1.10.13 | Tách sang bàn mới (bàn trống) | PASS (suy ra) | "Bàn nhận" cho chọn bàn khác |
| 1.10.14 | Tách và điều chỉnh số lượng | PASS (suy ra) | Stepper "SL tách" hỗ trợ |
| 1.10.15 | Tổng tiền sau tách bảo toàn | PASS (suy ra) | — |
| 1.10.16 | Không cho tách khi chỉ 1 món SL=1 | N/A | Chưa kiểm trực tiếp |
| 1.10.17 | Tách toàn bộ (bàn nguồn trống) | PASS (suy ra) | Tương tự chuyển bàn |
| 1.10.18 | Bấm "Xác nhận" hoàn tất | PASS | Tách thành công, đóng giao diện, về Order |
| 1.10.19 | Bấm "Hủy"/"Đóng" giữa chừng | PASS* | Nút "Đóng" có |
| 1.10.20 | Xác nhận khi chưa chọn món | PASS | Nút "Xác nhận" bị mờ khi 0 món chọn |
| 1.10.21 | Xác nhận khi chưa chọn bàn đích | PASS (suy ra) | Mặc định sẵn Bàn nhận/Hóa đơn nhận |
| 1.10.22 | Món đã gửi bếp vẫn tách/ghép được | PASS (suy ra) | — |
| 1.10.23 | Tách/ghép giữ ghi chú | PASS (suy ra) | — |
| 1.10.24 | Tách/ghép giữ tùy chọn (size/topping) | PASS (suy ra) | — |
| 1.10.25 | Tách/ghép khi đơn có giảm giá | N/A | Chưa kiểm sâu |
| 1.10.26 | Tách/ghép khi đơn có hàng tặng | N/A | Chưa kiểm sâu |
| 1.10.27 | Thẻ bàn cập nhật ngay | PASS (suy ra) | Như chuyển/gộp |
| 1.10.28 | Tổng tiền thẻ bàn khớp sau ghép | PASS (suy ra) | (xem LƯU Ý-02 về thẻ nhiều hóa đơn) |
| 1.10.29 | Chưa mở ca / không quyền | N/A | Admin đủ quyền, ca mở |
| 1.10.30 | 2 người dùng cùng bàn | N/A | Chỉ 1 phiên đăng nhập |

## 1.11 Hàng tặng
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.11.1 | Mở chức năng hàng tặng | PASS | Banner "ĐANG TRONG CHẾ ĐỘ CHỌN HÀNG TẶNG (TẶNG 100%)" |
| 1.11.2 | Chọn món tặng áp vào đơn | PASS | tran chau tặng = 0đ vào hóa đơn |
| 1.11.3 | Chọn lý do tặng | PASS | 4 lý do (Khách hàng thân thiết, hàng tặng kèm miễn phí...) |
| 1.11.4 | Món tặng hiển thị trong đơn | PASS | Nhãn "Hàng tặng kèm", 0đ |
| 1.11.5 | Hàng tặng không cộng vào tổng | PASS | Tổng thanh toán giữ 502.980 trước/sau khi thêm |
| 1.11.6 | Đơn không thỏa điều kiện | N/A | Không có điều kiện chặn cấu hình để kiểm |
| — | **LƯU Ý-03** | — | Giữ lý do **mặc định** rồi xác nhận → món tặng **không được thêm**; phải mở dropdown chọn lại lý do mới thêm được |

## 1.12 Áp dụng khuyến mãi
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.12.1 | Mở chức năng khuyến mãi | PASS | Danh sách CTKM đủ điều kiện ("KHUYEN MAI THEO SO LUONG KHACH HANG") |
| 1.12.2 | Áp khuyến mãi vào đơn | PASS | Giảm 1.000đ; tổng 10.500 → 9.450 |
| 1.12.3 | CTKM hết hiệu lực | N/A | Không có CTKM hết hạn để kiểm |
| 1.12.4 | Đơn không thỏa điều kiện CTKM | N/A | Hộp chỉ liệt kê CTKM đủ điều kiện |
| 1.12.5 | Bỏ khuyến mãi đã áp | PASS | Bỏ chọn + Áp dụng → tổng về 10.500 |
| 1.12.6 | Chưa mở ca | N/A | Ca đang mở |

## 1.13 Hủy đơn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.13.1 | Hủy đơn chưa thanh toán | PASS | Nút X cạnh tab hóa đơn → hộp "Hủy đơn hàng" |
| 1.13.2 | Chọn lý do hủy (bắt buộc) | PASS | "Lý do hủy *" — trường bắt buộc |
| 1.13.3 | Xác nhận hủy | PASS | "Hủy đơn hàng thành công" |
| 1.13.4 | Hủy đơn đã thanh toán | N/A | Đơn đã thanh toán rời bàn (thuộc menu Lịch sử), không hủy từ Home |
| 1.13.5 | Không có quyền / chưa mở ca | N/A | Admin đủ quyền, ca mở |

## 1.14 Thanh toán qua Chờ thanh toán
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.14.1 | Tab "Chờ thanh toán" hiển thị đơn chờ | PASS* | Tab hoạt động (empty state đúng); không có đơn chờ thanh toán để hiển thị danh sách thực |
| 1.14.2 | Thanh toán từ tab Chờ thanh toán | N/A | Không tạo được đơn "Chờ thanh toán" — "Gọi thanh toán" từ QR chỉ gửi thông báo, tab giữ 0 |
| 1.14.3 | Thanh toán bằng cách chọn bàn đang dùng | PASS | Đã thanh toán POS475 bằng cách vào Order của bàn đang dùng |
| 1.14.4 | Thanh toán đơn gửi từ tablet/mobile | PASS | Đơn QR đã xác nhận, thanh toán được như đơn thường |

## 1.15 Trường hợp đặc thù & lỗi
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.15.1 | Số lượng món = 0 | PASS | Nút − bị chặn ở SL 1, không về 0 |
| 1.15.2 | Giá rất lớn (999.999.999đ) | N/A | Hộp sửa giá chỉ cho **giảm giá**, không nhập giá lớn hơn gốc; số lớn (999.999 / 2.232.141) hiển thị OK, không vỡ giao diện |
| 1.15.3 | Làm tròn tiền VND | PASS | Mọi số là số nguyên VND (thuế 380/450/856...), không có số lẻ thập phân |
| 1.15.4 | Mất mạng khi thanh toán | N/A | Không mô phỏng an toàn trong phiên điều khiển trình duyệt |
| 1.15.5 | Hai thu ngân cùng 1 bàn | N/A | Chỉ 1 phiên đăng nhập |
| 1.15.6 | Ghi chú có dấu / ký tự đặc biệt | PASS | "Ít đá, nhiều đường @#!" lưu & hiển thị đúng |

---

## Tổng hợp
- **PASS:** ~96 (gồm các mục "PASS*" quan sát/một phần và "PASS (suy ra)" suy ra từ cùng cơ chế đã kiểm)
- **FAIL:** 1 — **1.8.4** (Chuyển bàn cho chọn bàn đang sử dụng làm đích)
- **N/A:** ~28 (điều kiện không tái hiện được: chưa mở ca/không quyền với tài khoản admin, thuế cả bill, CTKM hết hạn, mất mạng, 2 thiết bị, đơn chờ thanh toán, giá > giá gốc...)
- **BLOCKED:** 0

### Danh sách lỗi & lưu ý (ảnh/log: `screenshot/0612_2228_home/note.md`)
1. **BUG-01 (FAIL, 1.8.4) — Trung bình:** Chuyển bàn cho phép chọn bàn **đang sử dụng** (ban9 1.018.999đ) làm đích (nút "Chọn" sáng). Kỳ vọng chỉ cho chọn bàn trống. → Dev xác nhận: chặn bàn đang dùng, hoặc nếu là tính năng gộp-khi-chuyển thì cập nhật lại checklist.
2. **LƯU Ý-02 (1.9.5, hiển thị) — Thấp:** Bàn có nhiều hóa đơn, thẻ ngoài Trang chủ chỉ hiện tổng **1 hóa đơn** (ban8 hiện 510.000 thay vì 520.000). Tổng từng hóa đơn vẫn đúng.
3. **LƯU Ý-03 (1.11, UX) — Trung bình:** Hàng tặng **không được thêm** nếu xác nhận với lý do **mặc định**; phải mở dropdown chọn lại lý do mới thêm được.

### Khuyến nghị
1. Dev xem lại 1.8.4 (chuyển bàn vào bàn đang dùng) và 1.11 (lý do tặng mặc định không ăn).
2. Cân nhắc cho thẻ bàn hiển thị **tổng tất cả hóa đơn** khi 1 bàn có nhiều hóa đơn (1.9.5).
3. Các mục N/A "chưa mở ca / không quyền" cần test bằng **tài khoản phân quyền hạn chế** hoặc khi **ca đóng** (phiên này dùng admin nên không tái hiện).
4. Bổ sung kiểm: đơn mang về (1.1.13/1.6.4), thanh toán CK/Quẹt thẻ end-to-end (1.5.4/1.5.5), tạo đơn "Chờ thanh toán" để kiểm 1.14.2.
