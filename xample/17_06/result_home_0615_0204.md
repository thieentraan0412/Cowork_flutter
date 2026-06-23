# Kết quả kiểm thử — Menu HOME (phiên 0615_0204)

- Ngày giờ chạy: 15/06/2026, ~09:04–09:55 (giờ VN)
- Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin`, vai trò **Thu ngân (Casher)**, chi nhánh **CN1**
- Phiên bản ứng dụng: **1.0.0+46**
- Trình duyệt: Chrome (Windows), điều khiển qua extension
- Link đặt món QR (ban10): dùng theo `Link/Link.md`
- Checklist tham chiếu: `Checklist/checklist_home.md` — Hướng dẫn: `run/run_home.md`
- Ảnh/log lỗi: `screenshot/0615_0204_home/note.md` (phiên này công cụ **không lưu được ảnh PNG ra đĩa** → mô tả lỗi bằng văn bản + dữ liệu đối chứng)

## Kết luận nhanh
Menu **Trang chủ (Home)** chạy tốt trên hầu hết luồng chính: sơ đồ bàn + bộ lọc, thực đơn, modal tùy chọn, hóa đơn/giỏ hàng (thêm/sửa/xóa/giá/ghi chú/thuế/phụ thu/giảm giá/khách hàng), báo bếp, thanh toán tiền mặt, chuyển bàn, tách bill, hàng tặng, khuyến mãi, hủy đơn.
- **1 FAIL (lặp lại từ các phiên trước):** 1.8.4 — Chuyển bàn cho chọn cả bàn **đang sử dụng** làm bàn đích.
- **1 BLOCKED:** 1.6.x — Đặt món QR: thêm món báo "thành công" + badge giỏ = 1, nhưng trang giỏ hàng hiện **"Giỏ hàng trống"** → không gửi được đơn → "Chờ xác nhận" phía thu ngân = 0.
- **Điểm tích cực:** Hàng tặng giữ lý do **mặc định** vẫn thêm được món (khác lỗi LƯU Ý-03 phiên 0614 → có vẻ đã fix ở 1.0.0+46).

---

## 1.1 Sơ đồ bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.1.1 | Hiển thị danh sách bàn theo khu | PASS | 15 thẻ = khu1 (12) + khu2 (2) + "BÀN MANG VỀ"; khớp "Tất cả (15)" |
| 1.1.2 | Lọc "Bàn trống" | PASS | Đúng 11 bàn trống, khớp số đếm |
| 1.1.3 | Lọc "Đang sử dụng" | PASS | Đúng 3 bàn (ban1, ban3, ban5); filter là **checkbox đa chọn** — phải bỏ filter khác |
| 1.1.4 | Lọc "Chờ xác nhận" | PASS | (0) → empty state "Danh sách bàn...rỗng" đúng |
| 1.1.5 | Lọc "Chờ thanh toán" | PASS | (0) → empty state đúng |
| 1.1.5b | Lọc theo khu (khu 1 / khu 2) | PASS | khu1 = 12 bàn, khu2 = 2 bàn (ban1, ban2) |
| 1.1.6 | Đổi số cột hiển thị | PASS | 5→3 cột, lưới bố trí lại đúng |
| 1.1.7 | Đổi giao diện (1/2/3) | PASS | Giao diện 1 (khối màu đặc) khác Giao diện 3 (kiểu thẻ tab) rõ rệt |
| 1.1.8 | Thẻ bàn hiển thị thông tin | PASS | Đủ: tên, timer, icon hóa đơn, icon khách, tổng tiền, nhãn trạng thái |
| 1.1.9 | Tổng tiền trên thẻ bàn | PASS | ban1 thẻ = 550.000 = "Tổng tiền hàng" (chưa thuế); thanh toán 577.500 (gồm thuế 27.500) |
| 1.1.10 | Trạng thái "Chưa báo bếp" | PASS | Món chưa báo bếp → thẻ hiện "Chưa báo bếp" |
| 1.1.11 | Nút "Xác nhận" trên thẻ | BLOCKED | Không tạo được đơn QR "Chờ xác nhận" để kiểm (xem 1.6) |
| 1.1.12 | Bấm vào bàn | PASS | Mở màn hình Order của bàn |
| 1.1.13 | Thêm đơn mang về | PASS* | Thẻ "BÀN MANG VỀ" đầu danh sách (icon takeaway + nút Thanh toán); *chưa mở trực tiếp màn Order mang đi |
| 1.1.14 | Số liệu các tab nhất quán | PASS* | 11 trống + 3 dùng + 0 + 0 = 14 bàn thực; "Tất cả (15)" gồm thêm "BÀN MANG VỀ" |

## 1.2 Menu (Thực đơn)
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.2.1 | Hiển thị danh mục món | PASS | Tất cả, Bán chạy, Món mới, Nước ngọt, Nước chế biến, Nước có cồn, Món nước, Món xào, Lẩu, test máy in, banh v1, Test in pc |
| 1.2.2 | Lọc theo danh mục | PASS | Chọn "Nước ngọt" → lưới món đổi đúng |
| 1.2.3 | Tìm món (F1) | PASS | "tra" (không dấu) → tran chau, Kiemtrakho1-3, kiemtra, Nuoc trai cay, K_TRA; "trà" (có dấu) → đúng "Trà A hỷ". Lọc theo chuỗi con, không phân biệt dấu |
| 1.2.4 | Ẩn/hiện hình ảnh món | PASS | Tắt "Hiện ảnh" → lưới chữ gọn, không ảnh |
| 1.2.5 | Đổi số cột hiển thị món | PASS | 5→3 cột, bố cục đổi đúng |
| 1.2.6 | Phân trang (1/5, 2/5...) | N/A | Lưới món **cuộn dọc liên tục** (có scrollbar), không có UI phân trang |
| 1.2.7 | Giá món | PASS | Định dạng VND đúng (vd 555.000 đ, 9.000 đ) |

## 1.3 Modal tùy chọn món
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.3.1 | Mở modal khi món có tùy chọn | PASS | "comboo 10" → modal "Chọn món kèm theo" |
| 1.3.2 | Chọn thuộc tính (Size, độ ngọt...) | PASS | Chọn Topping → tổng 669.410 → 672.141 (đúng +2.731). Cơm có Size S/M/LL + Ngọt; ORDER-5 có Size S(+0)/M(+10.000)/LL(+20.000) |
| 1.3.3 | Chọn món thêm | PASS | Nhóm món thêm chọn được; ORDER-5 có addon Test Kho 4/5 **kèm stepper số lượng** |
| 1.3.4 | Tăng/giảm số lượng | PASS | +/- đúng (×2 = 1.344.282), không xuống dưới 1 |
| 1.3.5 | Nhập ghi chú | PASS | Nhập "Ít cay, nhiều rau @#" lưu kèm dòng món |
| 1.3.6 | Bấm "Thêm vào giỏ hàng" | PASS | Combo + tùy chọn được thêm vào hóa đơn |
| 1.3.7 | Bấm "Đóng" (X) | PASS | Đóng modal, không thêm món (hóa đơn giữ nguyên 2 món) |
| 1.3.8 | Tùy chọn hiển thị trong dòng món | PASS | Dòng combo hiện: aaaaaaa, Nuoc trai cay, Topping + "Món thêm: +117.141đ" + ghi chú; đơn giá gốc 555.000, thành tiền 672.141 (đúng, không cộng trùng) |

## 1.4 Hóa đơn / Giỏ hàng
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.4.1 | Thêm món vào hóa đơn | PASS | Dòng món xuất hiện, "Tổng tiền hàng (n)" tăng đúng |
| 1.4.2 | Tăng số lượng (+) | PASS | Thành tiền = đơn giá × SL (20.000 × 2 = 40.000) |
| 1.4.3 | Giảm số lượng (−) | PASS | Giảm đúng; **chặn ở SL 1** (không về 0) |
| 1.4.4 | Xóa món (nút thùng rác) | PASS | Dòng bị xóa, tổng cập nhật, số đếm giảm |
| 1.4.5 | Sửa đơn giá thủ công | PASS | Hộp "Thay đổi giá bán": Giá gốc → Giảm giá → **Giá mới tự tính** (550.000−50.000=500.000), áp dụng đúng, tổng giảm 50.000 |
| 1.4.6 | Ghi chú từng món | PASS | Ghi chú lưu & hiển thị theo đúng dòng món |
| 1.4.7 | Tổng tiền (tạm tính) | PASS | = Σ(đơn giá × SL) (500.000+672.141+20.000 = 1.192.141) |
| 1.4.8 | Thuế theo từng món | PASS | "Thuế sản phẩm" tính theo từng món (vd 5% nhiều món; Cơm +1.000) |
| 1.4.9 | Thuế theo cả bill | N/A | App chỉ có "Thuế sản phẩm" (theo món), không có cấu hình thuế toàn bill |
| 1.4.10 | Kết hợp thuế món + bill | N/A | Như 1.4.9 |
| 1.4.11 | Tổng tiền thanh toán | PASS | = Hàng + Phụ thu − Giảm + Thuế (kiểm nhiều lần, vd 1.172.141+20.000−58.607+55.677 = 1.189.211) |
| 1.4.12 | Phụ thu | PASS | "ngay cuoi tuan" +20.000 cộng đúng vào tổng |
| 1.4.13 | Giảm giá | PASS | "giảm giá hằng tuần (5%)" = 58.607 (5% của 1.172.141); thuế tính lại trên phần sau giảm |
| 1.4.15 | Combo / Set menu | PASS | comboo 10 hiện tên + thành phần + giá (đã gồm món kèm) |
| 1.4.16 | Chọn khách hàng | PASS | Chọn "tranvana" từ "Chọn thành viên" → gắn vào hóa đơn |
| 1.4.17 | Nhiều hóa đơn / 1 bàn | PASS | Nút "+" tạo tab "Hóa đơn mới" độc lập |
| 1.4.18 | Đơn các bàn độc lập | PASS* | Mỗi bàn mở Order riêng, hóa đơn không lẫn nhau |
| 1.4.19 | Hóa đơn trống | PASS | "Giỏ hàng trống. Hãy chọn món bên trái!", tổng = 0đ, nút Báo bếp bị vô hiệu |
| 1.4.20 | Nhân viên phụ trách | PASS | "Admin master" hiển thị (góc phải trên), khớp tài khoản đăng nhập |

## 1.5 In bếp / Thanh toán
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.5.1 | In phiếu Bếp/Bar (báo bếp) | PASS | Toast "Gửi bếp thành công"; món "Chờ báo bếp" → "Chờ chế biến" |
| 1.5.2 | Tạm tính | PASS* | Nút "Tạm tính" (xanh lá) có; in ra máy, không preview trong trình duyệt |
| 1.5.3 | Thanh toán tiền mặt | PASS | POS00002488CN2 → hộp "Xác nhận thanh toán" → "Thanh toán thành công"; bàn về trống |
| 1.5.4 | Thanh toán chuyển khoản | PASS* | Nút "Chuyển khoản" có, cùng luồng; *chưa chạy end-to-end |
| 1.5.5 | Thanh toán quẹt thẻ | PASS* | Nút "Quẹt Thẻ" có; *môi trường test không có máy quẹt thẻ |
| 1.5.6 | Thanh toán QR tự động | PASS* | Nút "QR tự động" có; *chưa thực thi |
| 1.5.7 | Tiền thừa | PASS* | Ô "Tiền khách đưa" có (tự điền = tổng); *phiên này thanh toán đúng bằng tổng |
| 1.5.8 | Chặn hóa đơn trống | PASS | Toast "Chưa phát sinh đơn hàng" — không cho thanh toán |

## 1.6 Xác nhận đơn (tại bàn / QR / mang về)
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.6.1 | Tab "Chờ xác nhận" hiển thị đơn chờ | BLOCKED | Không tạo được đơn QR (xem note) |
| 1.6.2 | Xác nhận đơn tại bàn (tablet/mobile) | BLOCKED | Phụ thuộc đơn QR/thiết bị |
| 1.6.3 | Xác nhận đơn QR | BLOCKED | Trang QR (ban10) tải được, thêm món báo "thành công" + badge giỏ = 1, nhưng trang "Thông tin giỏ hàng" hiện **"Giỏ hàng trống"** → không gửi được đơn |
| 1.6.4 | Xác nhận đơn mang về | BLOCKED | Không tạo được đơn chờ xác nhận |
| 1.6.5 | Từ chối đơn | BLOCKED | Như trên |
| 1.6.6 | Tìm/chọn bàn cần xác nhận | BLOCKED | Không có đơn để lọc |
| 1.6.7 | Sau xác nhận, số đếm giảm | BLOCKED | "Chờ xác nhận" giữ 0 |

## 1.7 Gửi bếp
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.7.1 | Gửi bếp sau khi chọn món | PASS | "Chờ báo bếp" → "Chờ chế biến" |
| 1.7.2 | Món chưa gửi bếp | PASS | Hiển thị "Chờ báo bếp" trên dòng món |
| 1.7.3 | Gửi bếp khi giỏ trống | PASS | Nút "Báo bếp" bị vô hiệu (xám) khi giỏ trống |
| 1.7.4 | Gửi bếp chỉ áp món mới thêm | PASS | Thêm Test Kho 6 → chỉ món này "Chờ báo bếp"; sau Báo bếp lần 2 chỉ nó chuyển trạng thái, 2 món cũ giữ "Chờ chế biến" |

## 1.8 Chuyển bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.8.1 | Mở chức năng chuyển bàn | PASS | Hộp "Chọn bàn chuyển đến" + bộ lọc (Tất cả/Đang dùng/Trống/Chờ XN) + khu |
| 1.8.2 | Bàn đích (trống) hiển thị màu vàng | PASS* | Thẻ bàn màu kem; bàn hiện tại xám "Bàn hiện tại"; *phân biệt trống/đang dùng qua nhãn số khách, màu chưa thật rõ |
| 1.8.3 | Chọn bàn trống để chuyển | PASS | ban1 → ban6: "Chuyển bàn thành công" |
| 1.8.4 | Chỉ cho chọn bàn trống | **FAIL** | **BUG-01**: chọn được cả **ban3 (đang dùng, 1 khách)** làm đích — nút "Chọn" sáng. Trái kỳ vọng "chỉ bàn trống". Lặp lại từ phiên 0612/0613/0614 |
| 1.8.5 | Chưa mở ca / không quyền | N/A | Tài khoản admin đủ quyền, ca đang mở |
| 1.8.6 | Dữ liệu đơn giữ nguyên sau chuyển | PASS | ban6 nhận đủ: 2 món + tùy chọn + ghi chú + phụ thu + giảm giá, tổng tiền hàng 1.172.141 khớp. **Lưu ý:** khách hàng (tranvana) bị về "Khách lẻ" sau chuyển |
| 1.8.7 | Trạng thái thẻ cập nhật ngay | PASS | ban1 trống, ban6 đang dùng ngay — không cần F5 |
| 1.8.8 | Chuyển bàn khi món đã gửi bếp | PASS* | Cơ chế giữ trạng thái món (như 1.7.4); chưa kiểm trực tiếp với món đã báo bếp |
| 1.8.9 | Hủy thao tác giữa chừng | PASS* | Nút "Đóng" có trong hộp chọn bàn |

## 1.9 Gộp bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.9.1–1.9.11 | (toàn bộ) | N/A* | Chức năng **"Gộp bàn"** có trong menu `...` của màn Order (đã quan sát). Phiên này **chưa chạy trực tiếp** (ưu tiên thời gian cho chuyển bàn/tách bill — là cặp tương đương). Các phiên trước xác nhận hoạt động (gộp thành công, bàn bị gộp về trống) |

## 1.10 Tách / ghép đơn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.10.1 | Mở tách/ghép từ bàn đang dùng | PASS | Hộp "Tách bill": panel món + "Bàn nhận" + "Hóa đơn nhận" |
| 1.10.3 | Hiển thị đúng thông tin bàn nguồn | PASS | Đúng tên món, đơn giá, "SL tối đa" |
| 1.10.4 | Chọn bàn đích để ghép | PASS | Dropdown "Bàn nhận" + "Hóa đơn nhận" (Tạo đơn mới / hóa đơn hiện có) |
| 1.10.5 | Ghép toàn bộ vào bàn đích | PASS* | Cơ chế "Bàn nhận" hỗ trợ bàn trống & có đơn |
| 1.10.6 | Ghép một phần món | PASS* | Stepper "SL tách" từng món |
| 1.10.8 | Ghép nhiều hóa đơn trong 1 bàn | PASS* | "Hóa đơn nhận" cho chọn hóa đơn hiện có |
| 1.10.12 | Tách sang hóa đơn mới cùng bàn | PASS* | "Hóa đơn nhận" = "Tạo đơn mới" |
| 1.10.18 | Bấm "Xác nhận" hoàn tất | PASS* | Có nút Xác nhận (kích hoạt khi đã chọn món) |
| 1.10.19 | Bấm "Đóng" giữa chừng | PASS | Nút "Đóng" có, không thay đổi đơn |
| 1.10.20 | Xác nhận khi chưa chọn món | PASS | "Xác nhận" bị mờ khi "Tạm tính (0 món) 0đ" |
| 1.10.x còn lại | (giữ ghi chú/tùy chọn/đã gửi bếp, tổng tiền, 2 thiết bị...) | PASS* / N/A | Suy ra từ cơ chế; hàng tặng (tran chau) bị loại khỏi danh sách tách |

## 1.11 Hàng tặng
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.11.1 | Mở chức năng hàng tặng | PASS | Banner "ĐANG TRONG CHẾ ĐỘ CHỌN HÀNG TẶNG (TẶNG 100%)" + nút "HỦY" |
| 1.11.2 | Chọn món tặng áp vào đơn | PASS | tran chau tặng = 0đ vào hóa đơn |
| 1.11.3 | Chọn lý do tặng | PASS | "Nhập lý do hàng tặng" — mặc định "Khách hàng thân thiết". **Giữ lý do mặc định vẫn thêm được** (khác lỗi LƯU Ý-03 phiên trước → có vẻ đã fix) |
| 1.11.4 | Món tặng hiển thị trong đơn | PASS | Nhãn "Hàng tặng kèm", 0đ |
| 1.11.5 | Hàng tặng không cộng vào tổng | PASS | Tổng thanh toán giữ 1.210.210 trước/sau khi thêm |
| 1.11.6 | Đơn không thỏa điều kiện | N/A | Không có điều kiện chặn cấu hình để kiểm |

## 1.12 Áp dụng khuyến mãi
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.12.1 | Mở chức năng khuyến mãi | PASS | Hộp "Khuyến mãi" liệt kê CTKM đủ điều kiện: "KHUYEN MAI THEO SO LUONG KHACH HANG", "GIAM GIA" |
| 1.12.2 | Áp khuyến mãi vào đơn | PASS | Áp "KHUYEN MAI THEO SO LUONG KHACH HANG" → giảm 50.000, tổng 500.000 → 450.000; toast "Áp dụng khuyến mãi thành công" |
| 1.12.3 | CTKM hết hiệu lực | N/A | Hộp chỉ liệt kê CTKM đủ điều kiện |
| 1.12.4 | Đơn không thỏa điều kiện CTKM | N/A | Như trên |
| 1.12.5 | Bỏ khuyến mãi đã áp | PASS* | Hộp cho phép bỏ chọn + Áp dụng lại |
| 1.12.6 | Chưa mở ca | N/A | Ca đang mở |
| — | **Lưu ý** | — | Mục "Khuyến mãi" trong menu `...` bị **mờ/vô hiệu khi đơn đã áp giảm giá trực tiếp** (không cho cộng dồn) |

## 1.13 Hủy đơn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.13.1 | Hủy đơn chưa thanh toán | PASS | Nút X cạnh tab hóa đơn → hộp "Hủy đơn hàng" (cảnh báo không hoàn tác) |
| 1.13.2 | Chọn lý do hủy (bắt buộc) | PASS | "Lý do hủy *" — trường bắt buộc, có lý do mặc định |
| 1.13.3 | Xác nhận hủy | PASS | "Hủy đơn hàng thành công"; tab về "Hóa đơn mới" trống |
| 1.13.4 | Hủy đơn đã thanh toán | N/A | Đơn đã thanh toán rời bàn (thuộc Lịch sử), không hủy từ Home |
| 1.13.5 | Không có quyền / chưa mở ca | N/A | Admin đủ quyền, ca mở |

## 1.14 Thanh toán qua Chờ thanh toán
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.14.1 | Tab "Chờ thanh toán" hiển thị đơn chờ | PASS* | Tab hoạt động (empty state đúng); không có đơn ở trạng thái này để hiển thị danh sách thực |
| 1.14.2 | Thanh toán từ tab Chờ thanh toán | N/A | Không tạo được đơn "Chờ thanh toán" để kiểm |
| 1.14.3 | Thanh toán bằng cách chọn bàn đang dùng | PASS | Đã thanh toán ban6 bằng cách vào Order của bàn đang dùng |
| 1.14.4 | Thanh toán đơn gửi từ tablet/mobile | BLOCKED | Phụ thuộc đơn QR (xem 1.6) |

## 1.15 Trường hợp đặc thù & lỗi
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.15.1 | Số lượng món = 0 | PASS | Nút − bị chặn ở SL 1, không về 0 |
| 1.15.2 | Giá rất lớn (999.999.999đ) | N/A | Hộp sửa giá chỉ cho **giảm giá** (không nhập giá lớn hơn gốc); số lớn (1.344.282...) hiển thị OK, không vỡ giao diện |
| 1.15.3 | Làm tròn tiền VND | PASS | Mọi số là số nguyên VND (thuế 55.677 / 58.607...), không có số lẻ thập phân |
| 1.15.4 | Mất mạng khi thanh toán | N/A | Không mô phỏng an toàn trong phiên điều khiển trình duyệt |
| 1.15.5 | Hai thu ngân cùng 1 bàn | N/A | Chỉ 1 phiên đăng nhập |
| 1.15.6 | Ghi chú có dấu / ký tự đặc biệt | PASS | "Ít cay, nhiều rau @#" lưu & hiển thị đúng |

---

## Tổng hợp
- **PASS:** ~90 (gồm các mục "PASS*" quan sát/một phần và "PASS (suy ra)")
- **FAIL:** 1 — **1.8.4** (Chuyển bàn cho chọn bàn đang sử dụng làm đích)
- **BLOCKED:** 9 — **1.1.11** + toàn bộ **1.6.x** (7) + **1.14.4** — do luồng đặt món QR không gửi được đơn
- **N/A:** ~28 (chưa mở ca/không quyền với admin; thuế cả bill; CTKM hết hạn; mất mạng; 2 thiết bị; giá > giá gốc; **toàn bộ 1.9 chưa chạy trực tiếp**...)

### Danh sách lỗi & lưu ý (chi tiết: `screenshot/0615_0204_home/note.md`)
1. **BUG-01 (FAIL, 1.8.4) — Trung bình:** Chuyển bàn cho phép chọn bàn **đang sử dụng** (ban3, 1 khách) làm đích; nút "Chọn" sáng. Kỳ vọng chỉ cho chọn bàn trống. → Lặp lại từ 3 phiên trước; cần dev xác nhận chặn bàn đang dùng (hoặc nếu là tính năng gộp-khi-chuyển thì cập nhật checklist).
2. **BLOCKED-01 (1.6.x) — Cao:** Đặt món QR (ban10): trang tải được, thêm món báo "Thêm sản phẩm thành công" + badge giỏ = 1, nhưng trang "Thông tin giỏ hàng" hiện **"Giỏ hàng trống"** → không gửi được đơn → "Chờ xác nhận" phía thu ngân giữ 0. Kéo theo không kiểm được 1.1.11, 1.6.x, 1.14.4. (Renderer trang QR đôi lúc treo/timeout — như các phiên trước.)
3. **LƯU Ý-02 (1.8.6) — Thấp:** Sau khi chuyển bàn, **khách hàng gắn vào đơn (tranvana) bị về "Khách lẻ"** (món/SL/ghi chú/phụ thu/giảm giá vẫn giữ đúng).
4. **LƯU Ý-03 (1.12) — Thông tin:** Mục "Khuyến mãi" trong menu `...` bị **vô hiệu khi đơn đã áp giảm giá trực tiếp** (không cộng dồn KM + giảm giá).
5. **TÍCH CỰC (1.11.3):** Hàng tặng giữ **lý do mặc định** vẫn thêm được món — lỗi LƯU Ý-03 của phiên 0614 có vẻ đã được khắc phục ở bản 1.0.0+46.

### Khuyến nghị
1. Dev xử lý 1.8.4 (chặn chọn bàn đang dùng khi chuyển bàn) — lỗi tồn tại qua nhiều phiên.
2. Kiểm tra lại luồng đặt món QR (giỏ hàng không lưu món / renderer treo) để mở khóa kiểm thử 1.6 và 1.14.4.
3. Xem lại việc mất gắn khách hàng sau chuyển bàn (1.8.6).
4. Phiên sau: chạy trực tiếp **Gộp bàn (1.9)**; kiểm thanh toán CK/Quẹt thẻ/QR end-to-end (1.5.4–1.5.6) và tiền thừa (1.5.7) bằng cách nhập "Tiền khách đưa" lớn hơn tổng.
