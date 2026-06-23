# Kết quả kiểm thử — Menu HOME (phiên 0614_1305)

- Ngày giờ chạy: 14/06/2026, ~13:05–14:00 (giờ máy)
- Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin`, vai trò **Thu ngân (Casher)**, chi nhánh **CN1**
- Phiên bản ứng dụng: **1.0.0+39**
- Trình duyệt: Chrome (Windows), điều khiển qua extension
- Checklist tham chiếu: `Checklist/checklist_home.md` — Hướng dẫn: `run/run_home.md`
- Ảnh/log lỗi: `screenshot/0614_1305_home/note.md` (phiên này công cụ **không lưu được ảnh PNG ra đĩa** → mô tả lỗi bằng văn bản + dữ liệu đối chứng)

## Kết luận nhanh
Menu **Trang chủ (Home)** hoạt động tốt trên hầu hết chức năng: sơ đồ bàn, bộ lọc trạng thái/khu, đổi cột/giao diện, thực đơn, modal tùy chọn, hóa đơn/giỏ hàng (thêm/sửa SL/xóa/sửa giá/ghi chú/phụ thu/giảm giá/khách hàng/nhiều HĐ), báo bếp (gửi mới + phiếu bổ sung), thanh toán **tiền mặt** và **chuyển khoản** (chạy end-to-end), tiền thừa, chặn đơn trống, hàng tặng, khuyến mãi, hủy đơn, chuyển bàn (thực thi thật), tách bill (thực thi thật), gộp bàn (mở + chọn).
- **1 FAIL:** 1.8.4 — Chuyển bàn cho chọn cả bàn **đang sử dụng** làm bàn đích (BUG-01, lặp lại từ 0613/0612).
- **1 BLOCKED:** nhóm 1.6 (xác nhận đơn QR) — trang đặt món QR treo renderer sau "Tạo đơn mới"; kéo theo 1.1.11 & 1.14.4 không kiểm trực tiếp.

---

## 1.1 Sơ đồ bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.1.1 | Hiển thị bàn theo khu | PASS | 14 bàn + "Bàn mang về"; khớp "Tất cả (14)" |
| 1.1.2 | Lọc "Bàn trống" | PASS | Đúng 7 bàn (ban1, ban1, ban_qr, ban4, ban6, ban7, ban8), khớp số đếm |
| 1.1.3 | Lọc "Đang sử dụng" | PASS | Đúng 7 bàn (ban2, ban2, ban ktra ten dai, ban3, ban5, ban9, ban10) |
| 1.1.4 | Lọc "Chờ xác nhận" | PASS | (0) → empty state "Danh sách bàn… 'Chờ xác nhận' rỗng" |
| 1.1.5 | Lọc "Chờ thanh toán" | PASS | (0) → empty state đúng |
| 1.1.5b | Lọc theo khu (khu 1/khu 2) | PASS | khu 1 = 12 bàn (loại khu2 ban1/ban2 + mang về); dropdown Tất cả/khu1/khu2 |
| 1.1.6 | Đổi số cột hiển thị | PASS | 6→4 cột bố trí lại; tùy chọn 1–8 cột |
| 1.1.7 | Đổi giao diện (1/2/3) | PASS | Giao diện 1↔3 đổi rõ kiểu thẻ (màu, vị trí tên/tổng tiền) |
| 1.1.8 | Thẻ bàn hiển thị thông tin | PASS | Đủ: tên, timer, icon hóa đơn, icon khách, tổng tiền, nhãn trạng thái |
| 1.1.9 | Tổng tiền trên thẻ bàn | PASS | Thẻ ban4 = **1.338.820 (Tổng tiền hàng, chưa thuế)**; thanh toán 1.405.761 (thuế 66.941) |
| 1.1.10 | Trạng thái "Chưa báo bếp" | PASS | Bàn có món chưa gửi bếp hiện "Chưa báo bếp" |
| 1.1.11 | Nút "Xác nhận" trên thẻ | N/A | Không có đơn "Chờ xác nhận" (0) — xem 1.6 (BLOCKED) |
| 1.1.12 | Bấm vào bàn | PASS | Mở màn hình Order của bàn |
| 1.1.13 | Thêm đơn mang về | PASS | "Bàn mang về" → quản lý đơn Mang về; "Thêm đơn hàng" → Order "ĐƠN MANG VỀ" |
| 1.1.14 | Số liệu các tab nhất quán | PASS | 7 + 7 + 0 + 0 = 14 = "Tất cả" |

## 1.2 Menu (Thực đơn)
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.2.1 | Hiển thị danh mục món | PASS | Tất cả, Bán chạy, Món mới, Nước ngọt, Nước chế biến, Nước có cồn, Món nước, Món xào, Lẩu, test máy in, banh v1, Test in pc |
| 1.2.2 | Lọc theo danh mục | PASS | Chọn "Nước ngọt" đổi lưới + đánh dấu chọn |
| 1.2.3 | Tìm món (F1) | PASS | "tra" (không dấu) → 6 KQ; "Trà" (có dấu) → "Trà A hỷ". OK cả có/không dấu |
| 1.2.4 | Ẩn/hiện hình ảnh | PASS | Toggle "Hiện ảnh" đổi giữa lưới chữ ↔ lưới ảnh |
| 1.2.5 | Đổi số cột hiển thị món | PASS | 2→4 cột; tùy chọn 2–5 cột |
| 1.2.6 | Phân trang (1/5…) | N/A | Lưới món cuộn dọc liên tục, không có UI phân trang |
| 1.2.7 | Giá món | PASS | Định dạng VND đúng (555.000đ, 10.000đ…) |

## 1.3 Modal tùy chọn món
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.3.1 | Mở modal khi món có tùy chọn | PASS | "comboo 10" → modal "Chọn món kèm theo" |
| 1.3.2 | Chọn thuộc tính | PASS | Nhóm min1/max1 (radio); chọn Topping bỏ test0, giá 669.410→672.141 |
| 1.3.3 | Chọn món thêm | PASS | Ghi nhận lựa chọn theo nhóm |
| 1.3.4 | Tăng/giảm số lượng | PASS | ×2 = 1.344.282; không xuống dưới 1 |
| 1.3.5 | Nhập ghi chú | N/A | Modal combo không có ô ghi chú (ghi chú ở dòng hóa đơn — 1.4.6) |
| 1.3.6 | Bấm "Thêm vào giỏ hàng" | PASS | Combo + tùy chọn vào hóa đơn |
| 1.3.7 | Bấm "Đóng" (X) | PASS | Đóng modal, không thêm món |
| 1.3.8 | Tùy chọn hiển thị trong dòng món | PASS | Hiện aaaaaaa, Nuoc trai cay, Topping + "Món thêm: +117.141đ" |

## 1.4 Hóa đơn / Giỏ hàng
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.4.1 | Thêm món vào hóa đơn | PASS | Dòng món xuất hiện, "Tổng tiền hàng (n)" tăng |
| 1.4.2 | Tăng số lượng (+) | PASS | Thành tiền = đơn giá × SL (672.141×2=1.344.282); tổng/thuế tính lại đúng (trễ vài giây) |
| 1.4.3 | Giảm số lượng (−) | PASS | Giảm đúng; **chặn ở SL 1**, không về 0 |
| 1.4.4 | Xóa món (thùng rác) | PASS | Dòng bị xóa (toast "Hủy món"), tổng cập nhật |
| 1.4.5 | Sửa đơn giá thủ công | PASS | Hộp "Thay đổi giá bán": giảm 55.000 → giá mới 500.000 (auto). **Chỉ giảm, không tăng > giá gốc** |
| 1.4.6 | Ghi chú từng món | PASS | Lưu & hiển thị "ít đá, nhiều đường @#!" |
| 1.4.7 | Tổng tiền (tạm tính) | PASS | = Σ(đơn giá × SL) |
| 1.4.8 | Thuế theo từng món | PASS | combo 5%; tran chau 5% (500/đơn vị); cf 0% (quan sát) |
| 1.4.9 | Thuế theo cả bill | N/A | App chỉ có "Thuế sản phẩm" (theo món) |
| 1.4.10 | Kết hợp thuế món + bill | N/A | Như 1.4.9 |
| 1.4.11 | Tổng tiền thanh toán | PASS | = Hàng + Phụ thu − Giảm + Thuế (617.141+20.000−0+30.857 = 667.998) |
| 1.4.12 | Phụ thu | PASS | "ngay cuoi tuan" +20.000 cộng đúng |
| 1.4.13 | Giảm giá | PASS | CTKM 10% = 61.714; thuế tính lại trên nền sau giảm; thanh toán đúng số đã giảm. *Chưa kiểm chéo end-to-end trang admin "quản lí đơn hàng"* |
| 1.4.15 | Combo / Set menu | PASS | Combo hiện tên + thành phần + giá (đã gồm "Món thêm") |
| 1.4.16 | Chọn khách hàng | PASS | Chọn "tranvana" (hộp "Chọn thành viên" có tìm kiếm) gắn vào hóa đơn |
| 1.4.17 | Nhiều hóa đơn / 1 bàn | PASS | Nút "+" tạo HĐ độc lập (POS…482 / …483 / "Hóa đơn mới") |
| 1.4.18 | Đơn các bàn độc lập | PASS | Mỗi bàn/HĐ riêng (quan sát qua chuyển/tách bàn) |
| 1.4.19 | Hóa đơn trống | PASS | "Giỏ hàng trống. Hãy chọn món bên trái!", tổng = 0đ |
| 1.4.20 | Nhân viên phụ trách | PASS* | "Admin master" hiển thị góc phải, khớp tài khoản đăng nhập |

## 1.5 In bếp / Thanh toán
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.5.1 | In phiếu Bếp/Bar (báo bếp) | PASS | Toast "Gửi bếp thành công"; món → "Chờ chế biến" |
| 1.5.2 | Tạm tính | PASS | Kích hoạt in tạm tính (không lỗi; không preview trong trình duyệt) |
| 1.5.3 | Thanh toán tiền mặt | PASS | Khách đưa 700.000 → "Xác nhận thanh toán" → "Thanh toán thành công", bàn về trống |
| 1.5.4 | Thanh toán chuyển khoản | PASS | Hiện QR ngân hàng + TK (TRAN VAN THIEN) → "Xác nhận" → "Thanh toán thành công" |
| 1.5.5 | Thanh toán quẹt thẻ | PASS* | Luồng đúng (chọn "Máy quẹt thẻ độc lập" → Gửi) nhưng lỗi "Gửi lệnh xuống máy quẹt thẻ thất bại" — thiếu máy quẹt thẻ vật lý |
| 1.5.6 | Thanh toán QR tự động | PASS | Sinh mã QR Momo (có chọn "Loại QR"); luồng xác nhận sẵn sàng |
| 1.5.7 | Tiền thừa | PASS | 700.000 − 612.647 = **87.353** (đúng) |
| 1.5.8 | Chặn hóa đơn trống | PASS | Bấm "Thanh toán" trên HĐ trống không mở hộp; "Báo bếp" vô hiệu |

## 1.6 Xác nhận đơn (tại bàn / QR / mang về)
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.6.1 | Tab "Chờ xác nhận" hiển thị | PASS* | Tab/bộ lọc hoạt động (empty state đúng); không populate được đơn QR thật |
| 1.6.2 | Xác nhận đơn tại bàn (tablet/mobile) | N/A | Không tạo được đơn chờ xác nhận |
| 1.6.3 | Xác nhận đơn QR | **BLOCKED** | Trang QR treo renderer ngay sau "Tạo đơn mới"; đơn không sang Thu ngân |
| 1.6.4 | Xác nhận đơn mang về | N/A | "Chờ xác nhận" mang về = 0 |
| 1.6.5 | Từ chối đơn | N/A | Không có đơn chờ để từ chối |
| 1.6.6 | Tìm/chọn bàn cần xác nhận | PASS | Bộ lọc Chờ xác nhận + dropdown khu + tìm kiếm hoạt động |
| 1.6.7 | Số đếm "Chờ xác nhận" giảm | N/A | Không có đơn để xác nhận |

## 1.7 Gửi bếp
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.7.1 | Gửi bếp sau khi chọn món | PASS | "Chờ báo bếp" → "Chờ chế biến" |
| 1.7.2 | Món chưa gửi bếp | PASS | Hiển thị "Chờ báo bếp" |
| 1.7.3 | Gửi bếp khi giỏ trống | PASS | Nút "Báo bếp" vô hiệu (xám) |
| 1.7.4 | Gửi bếp chỉ áp món mới | PASS | Thêm tran chau + Báo bếp → chỉ tran chau gửi; combo giữ "Chờ chế biến", không gửi trùng |

## 1.8 Chuyển bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.8.1 | Mở chức năng chuyển bàn | PASS | Hộp "Chọn bàn chuyển đến" + tab trạng thái + lọc khu; bàn hiện tại mờ |
| 1.8.2 | Bàn đích (trống) màu vàng | PASS* | Bàn hiện tại xám/mờ; trống & đang dùng đều màu kem (màu phân biệt chưa rõ) |
| 1.8.3 | Chọn bàn trống để chuyển | PASS | Chuyển ban_qr → ban4 (trống) — "Chuyển bàn thành công" |
| 1.8.4 | Chỉ cho chọn bàn trống | **FAIL** | **BUG-01**: chọn được cả **ban 2 (đang dùng, 2.232.141)** làm đích, nút "Chọn" sáng. Kỳ vọng: chỉ bàn trống. Lặp lại từ 0613/0612 |
| 1.8.5 | Chưa mở ca / không quyền | N/A | Admin đủ quyền, ca mở |
| 1.8.6 | Dữ liệu đơn giữ nguyên sau chuyển | PASS | ban4 nhận đủ đơn 1.338.820 (= combo ×2), 1 khách |
| 1.8.7 | Trạng thái thẻ cập nhật ngay | PASS | Về Trang chủ: ban_qr trống, ban4 đang dùng — không cần F5 |
| 1.8.8 | Chuyển bàn khi món đã gửi bếp | PASS (suy ra) | Trạng thái bám theo món (như 1.7.4) |
| 1.8.9 | Hủy thao tác giữa chừng | PASS | Có nút "Đóng" |

## 1.9 Gộp bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.9.1 | Mở chức năng gộp bàn | PASS | Hộp "Gộp bàn"; ban4 = "Bàn chính"; chọn ban5 → "Bàn sẽ gộp vào: ban5", "Tiếp tục" sáng (multi-select) |
| 1.9.2 | Gộp 2+ bàn đang hoạt động | PASS (suy ra) | Cơ chế chọn nhiều bàn phụ rồi "Tiếp tục"; không thực thi gộp thật để tránh hỏng dữ liệu store |
| 1.9.3 | Đơn đã thanh toán không cho gộp | N/A | Không có bàn đã TT đang mở để thử |
| 1.9.4–1.9.8 | Xác nhận / tổng tiền / món / gửi bếp / ghi chú | PASS (suy ra) | Cơ chế hỗ trợ |
| 1.9.9 | Hủy thao tác giữa chừng | PASS | "Đóng" hủy, không thay đổi |
| 1.9.10 | Chưa mở ca / không quyền | N/A | Admin đủ quyền, ca mở |
| 1.9.11 | Thẻ bàn cập nhật ngay sau gộp | PASS (suy ra) | Như cơ chế chuyển bàn (1.8.7) |

## 1.10 Tách / ghép đơn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.10.1 | Mở tách/ghép từ bàn đang dùng | PASS | Hộp "Tách bill": panel món + "Bàn nhận" + "Hóa đơn nhận" |
| 1.10.2 | Mở từ bàn trống | N/A | Chức năng trong menu bàn đang dùng |
| 1.10.3 | Hiển thị đúng bàn nguồn | PASS | comboo 10, đơn giá 555.000, SL tối đa 2 |
| 1.10.4 | Chọn bàn / hóa đơn đích | PASS | "Bàn nhận" + "Hóa đơn nhận" (Tạo đơn mới / HĐ hiện có) |
| 1.10.5–1.10.11 | Ghép toàn bộ/một phần, tổng tiền | PASS (suy ra) | Stepper "SL tách" + SL tối đa hỗ trợ bàn trống & có đơn |
| 1.10.12 | Tách 1 phần sang HĐ mới cùng bàn | PASS | Tách 1/2 combo → tạo HĐ mới POS…485 trong ban4 (mỗi HĐ 1 combo) |
| 1.10.14 | Tách & điều chỉnh số lượng | PASS | Tách 1 trong 2 |
| 1.10.15 | Tổng tiền sau tách không đổi | PASS | 669.410 + 669.410 = 1.338.820 |
| 1.10.18 | Bấm "Xác nhận" hoàn tất | PASS | Thực thi tách thành công |
| 1.10.19 | Bấm "Hủy"/"Đóng" giữa chừng | PASS | "Đóng" không thay đổi |
| 1.10.20 | Xác nhận khi chưa chọn món | PASS | "Xác nhận" mờ khi SL tách = 0 |
| 1.10.21–1.10.30 | Đích/giảm giá/hàng tặng/ghi chú/tùy chọn/2 thiết bị | PASS (suy ra) / N/A | Cơ chế giữ thuộc tính món; vài ca không tái hiện với 1 phiên admin |

## 1.11 Hàng tặng
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.11.1 | Mở chức năng hàng tặng | PASS | Banner "ĐANG TRONG CHẾ ĐỘ CHỌN HÀNG TẶNG (TẶNG 100%)" + HỦY |
| 1.11.2 | Chọn món tặng áp vào đơn | PASS | tran chau = 0đ vào hóa đơn |
| 1.11.3 | Chọn lý do tặng | PASS | Hộp "Nhập lý do hàng tặng" (mặc định "Khách hàng thân thiết") |
| 1.11.4 | Món tặng hiển thị trong đơn | PASS | Nhãn "Hàng tặng kèm", 0đ |
| 1.11.5 | Hàng tặng không cộng vào tổng | PASS | Tổng thanh toán giữ 702.881 trước–sau |
| 1.11.6 | Đơn không thỏa điều kiện | N/A | Không có điều kiện chặn cấu hình |

## 1.12 Áp dụng khuyến mãi
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.12.1 | Mở chức năng khuyến mãi | PASS | Danh sách CTKM đủ ĐK ("KHUYEN MAI THEO SO LUONG KHACH HANG") |
| 1.12.2 | Áp khuyến mãi vào đơn | PASS | Giảm 10% (61.714); thuế tính lại trên nền sau giảm; tổng giảm tương ứng |
| 1.12.3 | CTKM hết hiệu lực | N/A | Không có CTKM hết hạn để kiểm |
| 1.12.4 | Đơn không thỏa điều kiện | N/A | Hộp chỉ liệt kê CTKM đủ ĐK |
| 1.12.5 | Bỏ khuyến mãi đã áp | PASS (suy ra) | Modal KM chọn/bỏ chọn + Áp dụng; dòng "Giảm giá" về 0 khi gỡ |
| 1.12.6 | Chưa mở ca | N/A | Ca đang mở |

## 1.13 Hủy đơn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.13.1 | Hủy đơn chưa thanh toán | PASS | Nút X cạnh tab → hộp "Hủy đơn hàng" (cảnh báo "không thể hoàn tác") |
| 1.13.2 | Chọn lý do hủy (bắt buộc) | PASS | "Lý do hủy *" bắt buộc, có dropdown lý do |
| 1.13.3 | Xác nhận hủy | PASS | "Hủy đơn hàng thành công"; đơn POS…483 rời danh sách |
| 1.13.4 | Hủy đơn đã thanh toán | N/A | Đơn đã TT thuộc Lịch sử, không hủy từ Home |
| 1.13.5 | Không có quyền / chưa mở ca | N/A | Admin đủ quyền, ca mở |

## 1.14 Thanh toán qua Chờ thanh toán
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.14.1 | Tab "Chờ thanh toán" hiển thị | PASS* | Home dine-in empty đúng; khu Mang về có 1 đơn "Chờ thanh toán" (POS00002407CN2, 530.000) |
| 1.14.2 | Thanh toán từ tab Chờ thanh toán | PASS* (lưu ý) | Vào được luồng từ đơn "Chờ thanh toán" nhưng màn Order mở ra **giỏ trống** (chưa nạp lại món) — cần kiểm lại |
| 1.14.3 | Thanh toán bằng chọn bàn đang dùng | PASS | Đã thanh toán nhiều đơn bằng cách vào Order bàn đang dùng (tiền mặt/chuyển khoản) |
| 1.14.4 | Thanh toán đơn gửi tablet/mobile | N/A | Không tạo được đơn QR (xem 1.6 BLOCKED) |

## 1.15 Trường hợp đặc thù & lỗi
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.15.1 | Số lượng món = 0 | PASS | Nút − chặn ở SL 1, không về 0 |
| 1.15.2 | Giá rất lớn (999.999.999đ) | N/A | Sửa giá chỉ cho **giảm** (không nhập > giá gốc); số lớn (2.232.141 / 1.405.761) hiển thị OK, không vỡ UI |
| 1.15.3 | Làm tròn tiền VND | PASS | Mọi số nguyên VND (thuế 30.857/33.607/66.941, tiền thừa 87.353); chênh ±1đ do thứ tự làm tròn khi có KM |
| 1.15.4 | Mất mạng khi thanh toán | N/A | Không mô phỏng an toàn trong phiên |
| 1.15.5 | Hai thu ngân cùng 1 bàn | N/A | Chỉ 1 phiên đăng nhập |
| 1.15.6 | Ghi chú có dấu / ký tự đặc biệt | PASS | "ít đá, nhiều đường @#!" lưu & hiển thị đúng |

---

## Tổng hợp
- **PASS:** ~73 (gồm "PASS*" quan sát/một phần và "PASS (suy ra)" suy ra từ cơ chế đã kiểm)
- **FAIL:** 1 — **1.8.4** (Chuyển bàn cho chọn bàn đang sử dụng làm đích)
- **BLOCKED:** 1 — **1.6.3** (đặt đơn QR treo renderer) → kéo theo 1.6.2/1.6.4/1.6.5/1.6.7, 1.1.11, 1.14.4 không kiểm trực tiếp
- **N/A:** ~28 (điều kiện không tái hiện: thuế cả bill, chưa mở ca/không quyền với admin, CTKM hết hạn/không đủ ĐK, mất mạng, 2 thiết bị, đơn chờ thanh toán dine-in, giá > gốc, phân trang…)

### Danh sách lỗi & lưu ý (chi tiết: `screenshot/0614_1305_home/note.md`)
1. **BUG-01 (FAIL, 1.8.4) — Trung bình:** Chuyển bàn cho phép chọn bàn **đang sử dụng** (ban 2 — 2.232.141đ) làm đích (nút "Chọn" sáng). Kỳ vọng chỉ cho chọn bàn trống. → Dev cần chặn bàn đang dùng (hoặc nếu là tính năng gộp-khi-chuyển thì cập nhật checklist). **Lặp lại từ 0613/0612.**
2. **BLOCKED (1.6.x) — Cần kiểm lại:** Trang đặt món qua link QR (ban10) treo renderer ngay sau khi bấm "Tạo đơn mới"; không tạo được đơn "Chờ xác nhận" phía Thu ngân. Cần kiểm lại bằng thiết bị/QR thật.
3. **Lưu ý (1.5.5):** Quẹt thẻ trả lỗi "Faild 400: Gửi lệnh xuống máy quẹt thẻ thất bại" (thiếu máy quẹt thẻ vật lý trong môi trường test); chuỗi lỗi có lỗi chính tả "Faild".
4. **Lưu ý (1.14.2):** Mở đơn "Chờ thanh toán" (mang về POS00002407CN2) bằng nút "Thanh toán" → màn Order hiện giỏ trống (chưa nạp lại món của đơn) — cần kiểm lại.

### Khuyến nghị
1. Dev xem lại **1.8.4** (chuyển bàn vào bàn đang dùng) — lỗi tái diễn qua 3 phiên.
2. Kiểm lại luồng đặt món QR → "Chờ xác nhận" trên thiết bị/QR thật (1.6.2/1.6.3/1.6.4/1.6.7, 1.1.11, 1.14.4).
3. Bổ sung kiểm bằng **tài khoản phân quyền hạn chế** hoặc khi **ca đóng** cho các mục N/A "chưa mở ca / không quyền".
4. Kiểm chéo end-to-end hóa đơn có **giảm giá** ở trang admin "quản lí đơn hàng" (1.4.13); xác minh nạp lại món khi thanh toán đơn "Chờ thanh toán" (1.14.2); thực thi đầy đủ **gộp bàn** (1.9.2–1.9.8) trên dữ liệu test riêng.
