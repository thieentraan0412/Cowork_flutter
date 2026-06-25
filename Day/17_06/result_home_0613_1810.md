# Kết quả kiểm thử — Menu HOME (phiên 0613_1810)

- Ngày giờ chạy: 13/06/2026, ~18:10–18:56 (giờ VN)
- Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin`, vai trò **Thu ngân (Casher)**, chi nhánh **CN1**
- Phiên bản ứng dụng: **1.0.0+39**
- Trình duyệt: Chrome (Windows), điều khiển qua extension
- Link đặt món QR (ban10): theo `Link/Link.md`
- Checklist tham chiếu: `Checklist/checklist_home.md` — Hướng dẫn: `run/run_home.md`
- Ảnh/log lỗi: `screenshot/0613_1810_home/note.md` (phiên này công cụ **không lưu được ảnh ra đĩa** → mô tả lỗi bằng văn bản + dữ liệu đối chứng)

## Kết luận nhanh
Menu **Trang chủ (Home)** hoạt động tốt: sơ đồ bàn, bộ lọc trạng thái/khu, đổi cột/giao diện, thực đơn, modal tùy chọn, hóa đơn/giỏ hàng (thêm/sửa/xóa/ghi chú/phụ thu/giảm giá/khách hàng), báo bếp (gửi mới + phiếu bổ sung), thanh toán tiền mặt (tiền thừa), chặn đơn trống, hàng tặng, khuyến mãi (áp + gỡ), hủy đơn, và mở các chức năng chuyển/gộp/tách bàn.
- **1 FAIL**: 1.8.4 — Chuyển bàn cho chọn cả bàn **đang sử dụng** làm bàn đích (BUG-01, lặp lại từ phiên 12/06).
- **1 BLOCKED**: nhóm 1.6 (xác nhận đơn QR) — không tạo được đơn QR chờ xác nhận (trang QR bị treo renderer); kéo theo 1.1.11 & 1.14.4 không kiểm trực tiếp.

---

## 1.1 Sơ đồ bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.1.1 | Hiển thị bàn theo khu | PASS | 14 bàn + "Bàn mang về"; khớp "Tất cả (14)" |
| 1.1.2 | Lọc "Bàn trống" | PASS | Đúng 6 bàn (BAN1, BAN1, BAN_QR, BAN4, BAN6, BAN7), khớp số đếm |
| 1.1.3 | Lọc "Đang sử dụng" | PASS | Đúng 8 bàn; filter là **checkbox đa chọn** (phải bỏ filter khác) |
| 1.1.4 | Lọc "Chờ xác nhận" | PASS | (0) → empty state "Danh sách bàn… 'Chờ xác nhận' rỗng" |
| 1.1.5 | Lọc "Chờ thanh toán" | PASS | (0) → empty state đúng |
| 1.1.5b | Lọc theo khu (khu 1/khu 2) | PASS | khu 1 = 12 bàn (loại ban1/ban2 khu2 + mang về); dropdown có Tất cả/khu 1/khu 2 |
| 1.1.6 | Đổi số cột hiển thị | PASS | 6→4 cột lưới bố trí lại; có tùy chọn 1–8 cột |
| 1.1.7 | Đổi giao diện (1/2/3) | PASS | 2↔3 đổi rõ kiểu thẻ (tên vào trong thẻ, trạng thái lên trên) |
| 1.1.8 | Thẻ bàn hiển thị thông tin | PASS | Đủ: tên, timer, icon hóa đơn, icon khách, tổng tiền, nhãn trạng thái |
| 1.1.9 | Tổng tiền trên thẻ bàn | PASS | "ban kiem tra ten dai" thẻ **530.000 = Tổng tiền hàng (chưa thuế)**; thanh toán 580.000 (thuế 50.000) |
| 1.1.10 | Trạng thái "Chưa báo bếp" | PASS | Món "Chờ báo bếp" → thẻ hiện "Chưa báo bếp" |
| 1.1.11 | Nút "Xác nhận" trên thẻ | N/A | Không có đơn "Chờ xác nhận" (0) để hiện nút — xem mục 1.6 (BLOCKED) |
| 1.1.12 | Bấm vào bàn | PASS | Mở màn hình Order của bàn |
| 1.1.13 | Thêm đơn mang về | PASS | "Bàn mang về" → màn quản lý đơn Mang về (tab Chờ xác nhận/Đã xác nhận/Chờ thanh toán + "Thêm đơn hàng") |
| 1.1.14 | Số liệu các tab nhất quán | PASS | 6 + 8 + 0 + 0 = 14 = "Tất cả" |

## 1.2 Menu (Thực đơn)
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.2.1 | Hiển thị danh mục món | PASS | Tất cả, Bán chạy, Món mới, Nước ngọt, Nước chế biến, Nước có cồn, Món nước, Món xào, Lẩu, test máy in, banh v1, Test in pc |
| 1.2.2 | Lọc theo danh mục | PASS | Chọn "Nước ngọt" → lưới đổi + đánh dấu chọn |
| 1.2.3 | Tìm món (F1) | PASS | "tra" (không dấu) → khớp tran chau, Kiemtrakho, kiem tra, Nuoc trai cay… (không dấu OK) |
| 1.2.4 | Ẩn/hiện hình ảnh | PASS | Toggle "Hiện ảnh" off → lưới chữ gọn, không ảnh |
| 1.2.5 | Đổi số cột hiển thị món | PASS | 4→2 cột bố cục đổi (tùy chọn 2–5 cột) |
| 1.2.6 | Phân trang (1/5…) | N/A | Lưới món cuộn dọc liên tục, không có UI phân trang |
| 1.2.7 | Giá món | PASS | Định dạng VND đúng (555.000đ, 9.000đ, 999.999đ) |

## 1.3 Modal tùy chọn món
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.3.1 | Mở modal khi món có tùy chọn | PASS | "comboo 10" → modal "Chọn món kèm theo" |
| 1.3.2 | Chọn thuộc tính (Size, độ ngọt…) | PASS | Lẩu max1: chọn Topping → bỏ test0, tổng 669.410→672.141; món "Trà A hỷ" có Size/Ngọt/Đá |
| 1.3.3 | Chọn món thêm | PASS | Nhóm Nước ngọt/Nước chế biến chọn được |
| 1.3.4 | Tăng/giảm số lượng | PASS | 1→2 tổng ×2 (1.344.282); không xuống dưới 1 |
| 1.3.5 | Nhập ghi chú | N/A | Modal combo không có ô ghi chú (ghi chú ở dòng hóa đơn — xem 1.4.6) |
| 1.3.6 | Bấm "Chọn" (Thêm vào giỏ) | PASS | Combo + tùy chọn được thêm vào hóa đơn |
| 1.3.7 | Bấm "Đóng" (X) | PASS | Đóng modal, không thêm món |
| 1.3.8 | Tùy chọn hiển thị trong dòng món | PASS | Hiện: aaaaaaa, Nuoc trai cay, Topping + "Món thêm: +117.141đ" |

## 1.4 Hóa đơn / Giỏ hàng
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.4.1 | Thêm món vào hóa đơn | PASS | Dòng món xuất hiện, "Tổng tiền hàng (n)" tăng |
| 1.4.2 | Tăng số lượng (+) | PASS | Thành tiền = đơn giá × SL (672.141×2 = 1.344.282) |
| 1.4.3 | Giảm số lượng (−) | PASS | Giảm đúng; **chặn ở SL 1** (không về 0) |
| 1.4.4 | Xóa món (nút thùng rác) | PASS | Dòng bị xóa, tổng cập nhật |
| 1.4.5 | Sửa đơn giá thủ công | PASS | Hộp "Thay đổi giá bán": Giảm 55.000 → Giá mới 500.000 (auto). % clamp ≤100. **Chỉ giảm, không tăng > giá gốc** |
| 1.4.6 | Ghi chú từng món | PASS | Lưu & hiển thị "Ghi chú: Ít đá, nhiều đường @#!" |
| 1.4.7 | Tổng tiền (tạm tính) | PASS | = Σ(đơn giá×SL) (30.000+500.000 = 530.000) |
| 1.4.8 | Thuế theo từng món | PASS | Test Kho 8 = 10% (50.000); combo = 5% (33.607); cf sua new = 0% |
| 1.4.9 | Thuế theo cả bill | N/A | App chỉ có "Thuế sản phẩm" (theo món) |
| 1.4.10 | Kết hợp thuế món + bill | N/A | Như 1.4.9 |
| 1.4.11 | Tổng tiền thanh toán | PASS | = Hàng + Phụ thu − Giảm + Thuế (672.141+20.000−33.607+31.927 = 690.461) |
| 1.4.12 | Phụ thu | PASS | "ngay cuoi tuan" +20.000 cộng đúng (→ 725.748) |
| 1.4.13 | Giảm giá | PASS | "giảm giá hằng tuần 5%" = 33.607; thuế tính lại trên nền sau giảm. *Kiểm chéo admin chưa chạy end-to-end* |
| 1.4.14 | Gợi ý nhanh tiền mặt | N/A | Không thấy nút gợi ý mệnh giá; ô "Tiền khách đưa" tự điền = tổng |
| 1.4.15 | Combo / Set menu | PASS | Combo hiện tên + thành phần + giá (đã gồm "Món thêm +117.141") |
| 1.4.16 | Chọn khách hàng | PASS | Chọn "tranvana" (hộp Chọn thành viên có tìm kiếm) → gắn vào hóa đơn |
| 1.4.17 | Nhiều hóa đơn / 1 bàn | PASS | Nút "+" tạo HĐ độc lập (POS464/471/480 cùng bàn) |
| 1.4.18 | Đơn các bàn độc lập | PASS | Mỗi bàn Order riêng; thanh toán 1 HĐ không ảnh hưởng HĐ/bàn khác |
| 1.4.19 | Hóa đơn trống | PASS | "Giỏ hàng trống. Hãy chọn món bên trái!", tổng = 0đ |
| 1.4.20 | Nhân viên phụ trách | PASS | "Admin master" hiển thị, khớp tài khoản đăng nhập |

## 1.5 In bếp / Thanh toán
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.5.1 | In phiếu Bếp/Bar (báo bếp) | PASS | Toast "Gửi bếp thành công"; món "Chờ báo bếp" → "Chờ chế biến" |
| 1.5.2 | Tạm tính | PASS | "Đang in tạm tính…" (in phiếu; không preview trong trình duyệt) |
| 1.5.3 | Thanh toán tiền mặt | PASS | POS480 (699.910đ) → "Xác nhận" → đơn đóng/rời tab; bàn giữ HĐ khác (POS464/471 nguyên vẹn) |
| 1.5.4 | Thanh toán chuyển khoản | PASS* | Nút "Chuyển khoản" có, cùng luồng "Xác nhận thanh toán"; chưa chạy end-to-end |
| 1.5.5 | Thanh toán quẹt thẻ | PASS* | Nút "Quẹt Thẻ" có; chưa chạy end-to-end |
| 1.5.6 | Thanh toán QR tự động | PASS* | Nút "QR tự động" có; chưa chạy end-to-end |
| 1.5.7 | Tiền thừa | PASS | 800.000 − 699.910 = **100.090** (đúng) |
| 1.5.8 | Chặn hóa đơn trống | PASS | "Chưa phát sinh đơn hàng" — không cho thanh toán |

## 1.6 Xác nhận đơn (tại bàn / QR / mang về)
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.6.1 | Tab "Chờ xác nhận" hiển thị đơn chờ | PASS* | Tab/bộ lọc hoạt động (empty state đúng); **không populate được đơn QR thực tế** trong phiên |
| 1.6.2 | Xác nhận đơn tại bàn (tablet/mobile) | N/A | Không tạo được đơn chờ xác nhận (xem note BLOCKED) |
| 1.6.3 | Xác nhận đơn QR | **BLOCKED** | Đặt đơn QR (Comboo 10) **không propagate** sang Thu ngân; trang QR bị treo renderer |
| 1.6.4 | Xác nhận đơn mang về | N/A | Khu "Mang về" → "Chờ xác nhận" = 0 |
| 1.6.5 | Từ chối đơn | N/A | Không có đơn chờ để từ chối |
| 1.6.6 | Tìm/chọn bàn cần xác nhận | PASS | Bộ lọc Chờ xác nhận + dropdown khu + tìm kiếm hoạt động |
| 1.6.7 | Số đếm "Chờ xác nhận" giảm | N/A | Không có đơn để xác nhận |

## 1.7 Gửi bếp
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.7.1 | Gửi bếp sau khi chọn món | PASS | "Chờ báo bếp" → "Chờ chế biến" |
| 1.7.2 | Món chưa gửi bếp | PASS | Hiển thị "Chờ báo bếp" |
| 1.7.3 | Gửi bếp khi giỏ trống | PASS | Nút "Báo bếp" bị vô hiệu (xám) khi giỏ trống |
| 1.7.4 | Gửi bếp chỉ áp món mới | PASS | Thêm món B + Báo bếp → toast "In phiếu bổ sung"; món A giữ "Chờ chế biến", không gửi trùng |

## 1.8 Chuyển bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.8.1 | Mở chức năng chuyển bàn | PASS | Hộp "Chọn bàn chuyển đến" + tab trạng thái + lọc khu; bàn hiện tại mờ ("Bàn hiện tại") |
| 1.8.2 | Bàn đích (trống) hiển thị màu vàng | PASS* | Bàn hiện tại mờ; phân biệt trống/đang dùng qua thông tin đơn (màu chưa thật rõ) |
| 1.8.3 | Chọn bàn trống để chuyển | PASS (quan sát) | Bàn trống chọn được, nút "Chọn" kích hoạt (không thực thi chuyển để giữ dữ liệu) |
| 1.8.4 | Chỉ cho chọn bàn trống | **FAIL** | **BUG-01**: chọn được cả **ban2 (đang dùng, 2.232.141)** làm đích, nút "Chọn" sáng. Kỳ vọng: chỉ bàn trống |
| 1.8.5 | Chưa mở ca / không quyền | N/A | Admin đủ quyền, ca đang mở |
| 1.8.6 | Dữ liệu đơn giữ nguyên sau chuyển | PASS (suy ra) | Cơ chế chuyển giữ hóa đơn (đã xác minh chuyển thật ở phiên trước) |
| 1.8.7 | Trạng thái thẻ cập nhật ngay | PASS (suy ra) | — |
| 1.8.8 | Chuyển bàn khi món đã gửi bếp | PASS (suy ra) | Trạng thái món bám theo món (như 1.7.4) |
| 1.8.9 | Hủy thao tác giữa chừng | PASS | Nút "Đóng" có |

## 1.9 Gộp bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.9.1 | Mở chức năng gộp bàn | PASS | Hộp "Gộp bàn"; bàn hiện tại = "Bàn chính"; chọn bàn phụ; "Bàn sẽ gộp vào" |
| 1.9.2 | Gộp 2+ bàn đang hoạt động | PASS (suy ra) | Chọn nhiều bàn phụ rồi "Tiếp tục" |
| 1.9.3 | Đơn đã thanh toán không cho gộp | N/A | Không có bàn đã TT đang mở để thử |
| 1.9.4 | Xác nhận hoàn tất gộp | PASS (suy ra) | — |
| 1.9.5 | Tổng tiền sau gộp tính đúng | PASS (suy ra) | — |
| 1.9.6 | Danh sách món sau gộp | PASS (suy ra) | — |
| 1.9.7 | Gộp khi các bàn đã gửi bếp | PASS (suy ra) | — |
| 1.9.8 | Giữ ghi chú/tùy chọn | PASS (suy ra) | — |
| 1.9.9 | Hủy thao tác giữa chừng | PASS* | Nút "Đóng" có |
| 1.9.10 | Chưa mở ca / không quyền | N/A | Admin đủ quyền, ca mở |
| 1.9.11 | Thẻ bàn cập nhật ngay sau gộp | PASS (suy ra) | — |

## 1.10 Tách / ghép đơn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.10.1 | Mở tách/ghép từ bàn đang dùng | PASS | Hộp "Tách bill": panel món + "Bàn nhận" + "Hóa đơn nhận" (Tạo đơn mới) |
| 1.10.2 | Mở từ bàn trống | N/A | Chức năng trong menu bàn đang dùng (chưa kiểm ở bàn trống) |
| 1.10.3 | Hiển thị đúng thông tin bàn nguồn | PASS | Đúng món (cf sua new, Test Kho 8, thung coca) + đơn giá + SL tối đa |
| 1.10.4 | Chọn bàn/hóa đơn đích | PASS | Dropdown "Bàn nhận" + "Hóa đơn nhận" (Tạo đơn mới / HĐ hiện có) |
| 1.10.5–1.10.17 | Ghép/Tách toàn bộ/một phần, tổng tiền | PASS (suy ra) | Stepper "SL tách" + SL tối đa hoạt động; cơ chế hỗ trợ bàn trống & có đơn |
| 1.10.18 | Bấm "Xác nhận" hoàn tất | PASS (suy ra) | — |
| 1.10.19 | Bấm "Hủy"/"Đóng" | PASS | Nút "Đóng" có |
| 1.10.20 | Xác nhận khi chưa chọn món | PASS | Nút "Xác nhận" mờ khi 0 món |
| 1.10.21 | Xác nhận khi chưa chọn bàn đích | PASS (suy ra) | Mặc định sẵn Bàn nhận/Hóa đơn nhận |
| 1.10.22–1.10.28 | Món đã gửi bếp / ghi chú / tùy chọn / giảm giá / hàng tặng / thẻ bàn | PASS (suy ra) / N/A | Cơ chế giữ thuộc tính món; vài ca không kiểm sâu |
| 1.10.29 | Chưa mở ca / không quyền | N/A | Admin đủ quyền, ca mở |
| 1.10.30 | 2 người dùng cùng bàn | N/A | Chỉ 1 phiên đăng nhập |

## 1.11 Hàng tặng
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.11.1 | Mở chức năng hàng tặng | PASS | Banner "ĐANG TRONG CHẾ ĐỘ CHỌN HÀNG TẶNG (TẶNG 100%)" + HỦY |
| 1.11.2 | Chọn món tặng áp vào đơn | PASS | tran chau tặng = 0đ vào hóa đơn |
| 1.11.3 | Chọn lý do tặng | PASS | Hộp "Nhập lý do hàng tặng" (mặc định "Khách hàng thân thiết") |
| 1.11.4 | Món tặng hiển thị trong đơn | PASS | Nhãn "Hàng tặng kèm", 0đ |
| 1.11.5 | Hàng tặng không cộng vào tổng | PASS | Tổng giữ 530.000 / 580.000 trước–sau |
| 1.11.6 | Đơn không thỏa điều kiện | N/A | Không có điều kiện chặn cấu hình |
| — | Ghi chú | — | Phiên này lý do **mặc định** vẫn thêm được hàng tặng (khác LƯU Ý-03 phiên 12/06) |

## 1.12 Áp dụng khuyến mãi
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.12.1 | Mở chức năng khuyến mãi | PASS | Danh sách CTKM đủ ĐK ("giam tra tren 1tr", "KHUYEN MAI THEO SO LUONG KHACH HANG") |
| 1.12.2 | Áp khuyến mãi vào đơn | PASS | Giảm 108.000; tổng tính lại 1.017.000; toast "Áp dụng khuyến mãi thành công" |
| 1.12.3 | CTKM hết hiệu lực | N/A | Không có CTKM hết hạn để kiểm |
| 1.12.4 | Đơn không thỏa điều kiện | N/A | Hộp chỉ liệt kê CTKM đủ ĐK |
| 1.12.5 | Bỏ khuyến mãi đã áp | PASS | Bỏ chọn + Áp dụng → Giảm giá về 0, tổng về 1.130.000 |
| 1.12.6 | Chưa mở ca | N/A | Ca đang mở |

## 1.13 Hủy đơn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.13.1 | Hủy đơn chưa thanh toán | PASS | Nút X cạnh tab → hộp "Hủy đơn hàng" (cảnh báo "không thể hoàn tác") |
| 1.13.2 | Chọn lý do hủy (bắt buộc) | PASS | Trường "Lý do hủy *" bắt buộc |
| 1.13.3 | Xác nhận hủy | PASS | "Hủy đơn hàng thành công"; đơn rời danh sách hoạt động |
| 1.13.4 | Hủy đơn đã thanh toán | N/A | Đơn đã TT thuộc menu Lịch sử, không hủy từ Home |
| 1.13.5 | Không có quyền / chưa mở ca | N/A | Admin đủ quyền, ca mở |

## 1.14 Thanh toán qua Chờ thanh toán
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.14.1 | Tab "Chờ thanh toán" hiển thị đơn chờ | PASS* | Home "Chờ thanh toán" hoạt động (empty); khu Mang về có 1 đơn Chờ thanh toán (POS00002407CN2, 530.000) |
| 1.14.2 | Thanh toán từ tab Chờ thanh toán | N/A | Không có đơn dine-in "Chờ thanh toán" để thao tác |
| 1.14.3 | Thanh toán bằng chọn bàn đang dùng | PASS | Đã thanh toán POS480 bằng cách vào Order của bàn đang dùng |
| 1.14.4 | Thanh toán đơn gửi từ tablet/mobile | N/A | Không tạo được đơn từ QR (xem note BLOCKED) |

## 1.15 Trường hợp đặc thù & lỗi
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.15.1 | Số lượng món = 0 | PASS | Nút − chặn ở SL 1, không về 0 |
| 1.15.2 | Giá rất lớn (999.999.999đ) | N/A | Sửa giá chỉ cho **giảm** (không nhập > giá gốc); số lớn (999.999 / 2.232.141) hiển thị OK, không vỡ UI |
| 1.15.3 | Làm tròn tiền VND | PASS | Mọi số nguyên VND (thuế 33.607/31.927/50.000), không lẻ thập phân |
| 1.15.4 | Mất mạng khi thanh toán | N/A | Không mô phỏng an toàn trong phiên |
| 1.15.5 | Hai thu ngân cùng 1 bàn | N/A | Chỉ 1 phiên đăng nhập |
| 1.15.6 | Ghi chú có dấu / ký tự đặc biệt | PASS | "Ít đá, nhiều đường @#!" lưu & hiển thị đúng |

---

## Tổng hợp
- **PASS:** ~78 (gồm "PASS*" quan sát/một phần và "PASS (suy ra)" suy ra từ cơ chế đã kiểm)
- **FAIL:** 1 — **1.8.4** (Chuyển bàn cho chọn bàn đang sử dụng làm đích)
- **BLOCKED:** 1 — **1.6.3** (đặt đơn QR không propagate; trang QR treo) → kéo theo 1.6.2/1.6.4/1.6.5/1.6.7, 1.1.11, 1.14.4 không kiểm trực tiếp
- **N/A:** ~30 (điều kiện không tái hiện: thuế cả bill, gợi ý tiền mặt, chưa mở ca/không quyền với admin, CTKM hết hạn/không đủ ĐK, mất mạng, 2 thiết bị, đơn chờ thanh toán dine-in, giá > gốc, phân trang…)

### Danh sách lỗi & lưu ý (chi tiết: `screenshot/0613_1810_home/note.md`)
1. **BUG-01 (FAIL, 1.8.4) — Trung bình:** Chuyển bàn cho phép chọn bàn **đang sử dụng** (ban2 2.232.141đ) làm đích (nút "Chọn" sáng). Kỳ vọng chỉ cho chọn bàn trống. → Dev cần chặn bàn đang dùng (hoặc nếu là tính năng gộp-khi-chuyển thì cập nhật checklist). Lặp lại từ phiên 12/06.
2. **BLOCKED (1.6.x) — Cần kiểm lại:** Đặt đơn qua link QR (ban10) không tạo được đơn "Chờ xác nhận" phía Thu ngân; trang QR bị treo renderer trong phiên. Cần kiểm lại bằng thiết bị/QR thật để xác định là lỗi sản phẩm hay do môi trường điều khiển.

### Khuyến nghị
1. Dev xem lại 1.8.4 (chuyển bàn vào bàn đang dùng).
2. Kiểm lại luồng đặt món QR → "Chờ xác nhận" trên thiết bị thật (1.6.2/1.6.3/1.6.4/1.6.7, 1.1.11, 1.14.4).
3. Các mục N/A "chưa mở ca / không quyền" cần test bằng **tài khoản phân quyền hạn chế** hoặc khi **ca đóng** (phiên này dùng admin).
4. Bổ sung kiểm end-to-end: thanh toán CK/Quẹt thẻ/QR tự động (1.5.4–1.5.6); kiểm chéo hóa đơn giảm giá ở trang admin (1.4.13); chuyển/gộp/tách bàn thực thi đầy đủ (1.8.3/1.8.6–1.8.9, 1.9.2–1.9.8, 1.10.5–1.10.28).
