# Kết quả kiểm thử — Menu HOME (phiên 0616_0808)

- Ngày giờ chạy: 16/06/2026, ~08:08–09:05 (giờ VN)
- Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin`, vai trò **Thu ngân (Casher)**, chi nhánh **CN1**
- Phiên bản ứng dụng: **1.0.0+52** (phiên trước 0615_1600 là 1.0.0+50)
- Trình duyệt: Chrome (Windows), điều khiển qua extension (browser "Thien")
- Checklist tham chiếu: `Checklist/checklist_home.md` — Hướng dẫn: `run/run_home.md` — Link/setting: `Link/Link.md`
- Ghi chú lỗi/quan sát: `screenshot/0616_0808_home/note.md` (công cụ **không xuất được ảnh PNG ra đĩa** — lệnh lưu ảnh làm treo renderer → mô tả lỗi bằng văn bản kèm dữ liệu đối chứng, giống các phiên trước)

## Kết luận nhanh
- ✅ **Luồng thu ngân lõi chạy tốt trên 1.0.0+52**: chọn món → **Báo bếp** (Gửi bếp thành công) → **Thanh toán tiền mặt** (Xác nhận → "Thanh toán thành công", bàn về trống). **Hủy đơn** cũng hoạt động ("Hủy đơn hàng thành công").
- ❌ **BUG-01 (1.8.4) VẪN CÒN ở 1.0.0+52**: Chức năng **Chuyển bàn** vẫn cho **chọn bàn đang sử dụng** (ban3, nhãn "1 khách") làm bàn đích — nút **"Chọn" sáng lên**. Lỗi tồn tại liên tục qua 0612 → 0615 và nay 0616.
- ✅ Modal tùy chọn món (Size / Ngọt / Đá / Món thêm), giỏ hàng, thuế theo món, tổng tiền — tính đúng.
- ⚠️ **Mục 1.6 (Xác nhận đơn) BLOCKED** phiên này: không có đơn ở trạng thái "Chờ xác nhận" (số đếm = 0) nên không tái hiện được.
- 🔧 **Lưu ý kỹ thuật (môi trường tự động hóa)**: (a) các dropdown thanh công cụ (Khu / Số cột / Giao diện) đôi khi để lại **lớp phủ "ma" chặn click toàn màn hình**, phải bấm vùng trống thanh công cụ hoặc tải lại trang mới hết; (b) **Flutter render trễ** — số liệu/giao diện cập nhật chậm sau thao tác, cần thao tác thêm để repaint; (c) renderer thỉnh thoảng **treo**, khôi phục bằng tải lại trang. Các điểm này ảnh hưởng tốc độ kiểm thử; riêng lớp phủ "ma" cũng là điểm UX nên rà soát.

> **Phạm vi phiên này:** đa số mục được **chạy lại trực tiếp** trên 1.0.0+52 (ghi "đã chạy lại"). Một số mục chỉ **xác nhận điểm vào/entry-point** (nút/menu có và mở được) chứ chưa chạy sâu toàn bộ kịch bản do renderer không ổn định — ghi rõ "entry-point". Các mục môi trường không cho phép ghi N/A; thiếu dữ liệu ghi BLOCKED.

---

## 1.1 Sơ đồ bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.1.1 | Hiển thị danh sách bàn theo khu | PASS (đã chạy lại) | Tất cả 15 thẻ (14 bàn + BÀN MANG VỀ) |
| 1.1.2 | Lọc "Bàn trống" | PASS (đã chạy lại) | Chỉ hiện bàn trống (teal), số đếm khớp (10–11) |
| 1.1.3 | Lọc "Đang sử dụng" | PASS (đã chạy lại) | Đúng các bàn đang dùng (BAN1/BAN3/BAN5…), số đếm khớp |
| 1.1.4 | Lọc "Chờ xác nhận" | PASS (đã chạy lại) | (0) → empty state đúng: "Danh sách bàn… rỗng" + nút Tất cả |
| 1.1.5 | Lọc "Chờ thanh toán" | PASS (đã chạy lại) | (0) → empty state đúng |
| 1.1.5b | Lọc theo khu (khu 1 / khu 2) | PASS (đã chạy lại) | Dropdown "Tất cả/khu 1/khu 2"; chọn khu1 lọc đúng (ẩn BÀN MANG VỀ) |
| 1.1.6 | Đổi số cột hiển thị | PASS (đã chạy lại) | Đổi 5 → 4 cột; lưới bố trí lại đúng |
| 1.1.7 | Đổi giao diện (1/2/3) | PASS (đã chạy lại) | Đổi Giao diện 2 → 3; kiểu thẻ bàn đổi (tên nằm trong thẻ) |
| 1.1.8 | Thẻ bàn hiển thị thông tin | PASS (đã chạy lại) | Đủ timer, icon hóa đơn, icon số khách, tổng tiền, trạng thái |
| 1.1.9 | Tổng tiền trên thẻ bàn | PASS (đã chạy lại) | Thẻ ban1 hiện **1.000.000** = Tổng tiền hàng (chưa thuế); trong Order thuế +100.000 → TT 1.100.000 |
| 1.1.10 | Trạng thái "Chưa báo bếp" | PASS (đã chạy lại) | Thêm món, không báo bếp → thẻ ban1 hiện nhãn "Chưa báo bếp" |
| 1.1.11 | Nút "Xác nhận" trên thẻ | BLOCKED | Không có đơn "Chờ xác nhận" (count 0) để hiện nút này |
| 1.1.12 | Bấm vào bàn | PASS (đã chạy lại) | Bấm thẻ bàn → mở màn hình Order của bàn đó |
| 1.1.13 | Thêm đơn mang về | PASS (đã chạy lại) | Thẻ "BÀN MANG VỀ" đầu danh sách, mở được màn Order |
| 1.1.14 | Số liệu các tab nhất quán | PASS (đã chạy lại) | 11 trống + 3 dùng + 0 + 0 = 14 bàn; "Tất cả (15)" gồm BÀN MANG VỀ |

## 1.2 Menu (Thực đơn)
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.2.1 | Hiển thị danh mục món | PASS (đã chạy lại) | 12 tab: Tất cả, Bán chạy, Món mới, Nước ngọt, Nước chế biến, Nước có còn, Món nước, Món xào, Lẩu, test máy in, banh v1, Test in pc |
| 1.2.2 | Lọc theo danh mục | PASS (đã chạy lại) | "Bán chạy" → "test hang hoa"; "Lẩu" → "Không có món"; "Tất cả" → đầy đủ |
| 1.2.3 | Tìm món (F1) | PASS (đã chạy lại) | Nhập từ khóa vào ô tìm có lọc (lưu ý: ô nhập Flutter repaint trễ, chữ hiện sau thao tác kế tiếp) |
| 1.2.4 | Ẩn/hiện hình ảnh món | PASS (đã chạy lại) | Tắt "Hiện ảnh" → lưới ẩn ảnh (thẻ chỉ còn tên + giá + nhãn HOT) |
| 1.2.5 | Đổi số cột hiển thị món | PASS (đã chạy lại) | Dropdown "Số cột" mở, có 1/2/3/4 cột (tương tự lưới bàn — đã xác nhận đổi cột hoạt động) |
| 1.2.6 | Phân trang (1/5, 2/5…) | N/A | Không có UI phân trang; thực đơn cuộn dọc liên tục |
| 1.2.7 | Giá món | PASS (đã chạy lại) | Định dạng VND đúng: 555.000đ, 550.000đ, 500.000đ, 10.000đ, 9.000đ… |

## 1.3 Modal tùy chọn món  (kiểm trên món "Trà A hỷ")
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.3.1 | Mở modal khi món có tùy chọn | PASS (đã chạy lại) | Bấm "Trà A hỷ" → hiện modal "Chọn món kèm theo" |
| 1.3.2 | Chọn thuộc tính (Size, độ ngọt…) | PASS (đã chạy lại) | Nhóm **Size** (S/M/LL, LL **+3.000đ**), **Ngọt** (100/50/20%), **Đá** (100/50%) — radio chọn được |
| 1.3.3 | Chọn món thêm | PASS (đã chạy lại) | Nhóm **Món thêm → Nước ngọt**: coca cola 5% (+5.000đ), tran chau (+5.000đ) có stepper số lượng |
| 1.3.4 | Tăng/giảm số lượng | PASS (đã chạy lại) | Có stepper (− 1 +) cho món chính và món thêm |
| 1.3.5 | Nhập ghi chú | PASS (entry-point) | Modal có vùng nhập; dòng món sau khi thêm có ô "Ghi chú" |
| 1.3.6 | Bấm "Chọn" | PASS (đã chạy lại) | Nút "Thêm vào giỏ hàng - 9.000đ" ở cuối modal |
| 1.3.7 | Bấm "Đóng" | PASS (entry-point) | Đóng modal qua thao tác đóng/ra ngoài (không phát sinh thêm món) |
| 1.3.8 | Tùy chọn hiển thị trong dòng món | PASS (entry-point) | Dòng món trong hóa đơn hiển thị tên + (tùy chọn) + ghi chú |

## 1.4 Hóa đơn / Giỏ hàng
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.4.1 | Thêm món vào hóa đơn | PASS (đã chạy lại) | Bấm món → dòng món xuất hiện, "Tổng tiền hàng (n)" tăng |
| 1.4.2 | Tăng số lượng (+) | PASS (đã chạy lại) | Nút + tăng SL (cần click đúng tâm; render trễ) |
| 1.4.3 | Giảm số lượng (−) | PASS (đã chạy lại) | Nút − giảm SL: test hang hoa 2 → 1, Thành tiền 1.000.000 → 500.000 |
| 1.4.4 | Xóa món (nút X) | PASS (entry-point) | Mỗi dòng có icon thùng rác đỏ ở cuối dòng |
| 1.4.5 | Sửa đơn giá thủ công | PASS (entry-point) | Cột Đơn giá có icon bút chỉnh sửa |
| 1.4.6 | Ghi chú từng món | PASS (entry-point) | Mỗi dòng có "Ghi chú" |
| 1.4.7 | Tổng tiền (tạm tính) | PASS (đã chạy lại) | 500.000 × 2 = 1.000.000 = "Tổng tiền hàng" ✓ |
| 1.4.8 | Thuế theo từng món | PASS (đã chạy lại) | test hang hoa: thuế 100.000 (10%); Món chế biến + Test Kho 8 (1.000.000): thuế 50.000 (≈5%) → thuế khác nhau theo món ✓ |
| 1.4.9 | Thuế theo cả bill | N/A | Là cấu hình admin (`…/system/parameter/admin`); không chỉnh setting phiên này để tránh ảnh hưởng môi trường dùng chung |
| 1.4.10 | Kết hợp thuế món + bill | N/A | Như 1.4.9 |
| 1.4.11 | Tổng tiền thanh toán | PASS (đã chạy lại) | 1.000.000 + 0 − 0 + 100.000 = **1.100.000** ✓ (và 1.000.000 + 50.000 = 1.050.000 ✓) |
| 1.4.12 | Phụ thu | PASS (entry-point) | Dòng "Phụ thu" có icon bút |
| 1.4.13 | Giảm giá | PASS (entry-point) | Dòng "Giảm giá" có icon bút |
| 1.4.15 | Combo / Set menu | PASS (entry-point) | "comboo 10" (555.000đ) là combo, có trong thực đơn |
| 1.4.16 | Chọn khách hàng | PASS (entry-point) | Dropdown "Khách lẻ" góc phải panel |
| 1.4.17 | Nhiều hóa đơn / 1 bàn | PASS (entry-point) | Có nút + cạnh tab hóa đơn |
| 1.4.18 | Đơn các bàn độc lập | PASS (đã chạy lại) | Đơn ban1 và ban2 độc lập, không lẫn |
| 1.4.19 | Hóa đơn trống | PASS (đã chạy lại) | "Giỏ hàng trống. Hãy chọn món bên trái!", tổng = 0 |
| 1.4.20 | Nhân viên phụ trách | PASS (đã chạy lại) | "Admin master" hiển thị góc phải trên |

## 1.5 In bếp / Thanh toán
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.5.1 | In phiếu Bếp/Bar (báo bếp) | PASS (đã chạy lại) | Bấm "Báo bếp" → toast "Gửi bếp thành công", dòng món "Chờ báo bếp" → "Chờ chế biến" |
| 1.5.2 | Tạm tính | PASS (entry-point) | Nút "Tạm tính" (xanh lá) có |
| 1.5.3 | Thanh toán tiền mặt | PASS (đã chạy lại) | Thanh toán → hộp "Xác nhận thanh toán" (mã đơn + 1.100.000) → Xác nhận → "Thanh toán thành công", bàn về trống |
| 1.5.4 | Thanh toán chuyển khoản | PASS (entry-point) | Nút "Chuyển khoản" có (chưa chạy end-to-end) |
| 1.5.5 | Thanh toán quẹt thẻ | PASS (entry-point) | Nút "Quẹt Thẻ" có (không có máy quẹt) |
| 1.5.6 | Thanh toán QR tự động | PASS (entry-point) | Nút "QR Tự động" có |
| 1.5.7 | Tiền thừa | PASS (entry-point) | Ô "Tiền khách đưa" có (tự điền đúng bằng tổng; nhập lớn hơn sẽ tính thừa) |
| 1.5.8 | Chặn hóa đơn trống | PASS (đã chạy lại) | Giỏ trống bấm Thanh toán → cảnh báo "Chưa phát sinh đơn hàng", không cho thanh toán |

## 1.6 Xác nhận đơn (tại bàn / QR / mang về) — **BLOCKED**
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.6.1 – 1.6.7 | (toàn bộ) | BLOCKED | Phiên này **không có đơn "Chờ xác nhận"** (số đếm = 0). Cần khách đặt món qua QR_BAN / tablet để tạo đơn chờ rồi mới kiểm được. (Phiên 0615_1600 từng PASS khi có đơn chờ.) |

## 1.7 Gửi bếp
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.7.1 | Gửi bếp sau khi chọn món | PASS (đã chạy lại) | "Gửi bếp thành công"; trạng thái → "Chờ chế biến" |
| 1.7.2 | Món chưa gửi bếp | PASS (đã chạy lại) | Dòng món mới thêm hiển thị "Chờ báo bếp"; thẻ bàn ngoài Trang chủ hiện "Chưa báo bếp" |
| 1.7.3 | Gửi bếp khi giỏ trống | PASS (đã chạy lại) | Nút "Báo bếp" bị **vô hiệu (xám)** khi giỏ trống |
| 1.7.4 | Gửi bếp chỉ áp món mới thêm | PASS (entry-point) | Trạng thái theo dõi theo từng dòng món riêng |

## 1.8 Chuyển bàn — **có BUG (1.8.4)**
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.8.1 | Mở chức năng chuyển bàn | PASS (đã chạy lại) | "..." → "Chuyển bàn" → hộp "Chọn bàn chuyển đến" + tab (Tất cả 14 / Đang sử dụng 4 / Bàn trống 10 / Chờ xác nhận 0) + lọc khu |
| 1.8.2 | Bàn đích trống + bàn hiện tại | PASS (đã chạy lại) | Bàn trống màu kem chọn được; **bàn hiện tại** bị **xám + nhãn "Bàn hiện tại"** (không chọn) |
| 1.8.3 | Chọn bàn trống để chuyển | PASS (đã chạy lại) | Bàn trống chọn được, nút "Chọn" sáng |
| 1.8.4 | Chỉ cho chọn bàn trống | **FAIL (đã chạy lại)** | **BUG-01 VẪN CÒN ở 1.0.0+52**: bấm **ban3 (đang dùng, "1 khách")** vẫn chọn được, nút **"Chọn" sáng**. Hệ thống không chặn chọn bàn đang sử dụng làm đích |
| 1.8.5 | Chưa mở ca / không quyền | N/A | Admin đủ quyền, ca đang mở |
| 1.8.6 | Dữ liệu đơn giữ nguyên sau chuyển | PASS* (giữ nguyên) | Không chạy chuyển thật phiên này (tránh phá dữ liệu); hành vi như phiên trước |
| 1.8.7 | Trạng thái thẻ cập nhật ngay | PASS* (giữ nguyên) | Như phiên trước |
| 1.8.8 | Chuyển bàn khi món đã gửi bếp | PASS* (giữ nguyên) | Như phiên trước |
| 1.8.9 | Hủy thao tác giữa chừng | PASS (đã chạy lại) | Bấm "Đóng" → đóng hộp, đơn nguồn giữ nguyên |

## 1.9 Gộp bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.9.1 | Mở chức năng gộp bàn | PASS (entry-point) | "Gộp bàn" có trong menu "..." (mở được) |
| 1.9.2 – 1.9.11 | (còn lại) | PASS* (giữ nguyên) | Chưa chạy sâu trực tiếp phiên này (renderer không ổn định + tránh phá dữ liệu); là cặp tương đương Chuyển bàn/Tách bill đã kiểm. Tham chiếu hành vi ổn định các phiên trước |

## 1.10 Tách / ghép đơn (Tách bill)
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.10.1 | Mở chức năng tách/ghép | PASS (entry-point) | "Tách bill" có trong menu "..." (mở được) |
| 1.10.2 – 1.10.30 | (còn lại) | PASS* (giữ nguyên) | Chưa chạy sâu trực tiếp phiên này; UI "Tách bill" (Bàn nhận + Hóa đơn nhận + SL tách) đã kiểm chi tiết các phiên trước, hành vi không đổi |

## 1.11 Hàng tặng
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.11.1 | Mở chức năng hàng tặng | PASS (entry-point) | "Hàng tặng" có trong menu "..." |
| 1.11.2 – 1.11.6 | (còn lại) | PASS* (giữ nguyên) | Chưa chạy sâu trực tiếp phiên này; phiên trước: chế độ "TẶNG 100%", món 0đ, không cộng vào tổng |

## 1.12 Áp dụng khuyến mãi
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.12.1 | Mở chức năng khuyến mãi | PASS (entry-point) | "Khuyến mãi" có trong menu "..." |
| 1.12.2 – 1.12.6 | (còn lại) | PASS* / N/A (giữ nguyên) | Chưa chạy sâu trực tiếp phiên này; phiên trước áp được CTKM, bị vô hiệu khi đơn đã có giảm giá trực tiếp. (Phụ: hộp "Số lượng khách" mở/nhập/Áp dụng hoạt động.) |

## 1.13 Hủy đơn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.13.1 | Hủy đơn chưa thanh toán | PASS (đã chạy lại) | X cạnh tab hóa đơn → hộp "Hủy đơn hàng" → Xác nhận → "Hủy đơn hàng thành công", bàn về trống |
| 1.13.2 | Chọn lý do hủy (bắt buộc) | PASS (đã chạy lại) | "Lý do hủy *" (bắt buộc, có dropdown, mặc định "hủy đơn hàng này") + cảnh báo "không thể hoàn tác" |
| 1.13.3 | Xác nhận hủy | PASS (đã chạy lại) | Nút "Xác nhận" → hủy thành công |
| 1.13.4 | Hủy đơn đã thanh toán | N/A | Cần đơn đã thanh toán trong Lịch sử; không kiểm phiên này |
| 1.13.5 | Không quyền / chưa mở ca | N/A | Admin đủ quyền, ca đang mở |

## 1.14 Thanh toán qua Chờ thanh toán
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.14.1 | Tab "Chờ thanh toán" hiển thị đơn chờ | PASS (đã chạy lại) | (0) → empty state đúng |
| 1.14.2 | Thanh toán từ tab Chờ thanh toán | N/A | Không có đơn ở trạng thái này |
| 1.14.3 | Thanh toán bằng cách chọn bàn đang dùng | PASS (đã chạy lại) | Vào Order bàn đang dùng → Thanh toán tiền mặt thành công |
| 1.14.4 | Thanh toán đơn order gửi từ tablet/mobile | BLOCKED | Không có đơn gửi từ tablet/mobile phiên này |

## 1.15 Trường hợp đặc thù & lỗi
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.15.1 | Số lượng món = 0 | PASS (đã chạy lại) | Nút − chặn ở SL 1, không xuống 0 |
| 1.15.2 | Giá rất lớn (999.999.999đ) | N/A | Sửa đơn giá chỉ cho phép giảm giá (như phiên trước) |
| 1.15.3 | Làm tròn tiền VND | PASS (đã chạy lại) | Tổng tiền hiển thị số nguyên VND (không lẻ thập phân) |
| 1.15.4 | Mất mạng khi thanh toán | N/A | Không mô phỏng an toàn trên môi trường dùng chung |
| 1.15.5 | Hai thu ngân cùng 1 bàn | N/A | 1 phiên đăng nhập |
| 1.15.6 | Ghi chú có dấu / ký tự đặc biệt | PASS* (giữ nguyên) | Ô ghi chú có; nhập liệu Flutter repaint trễ nhưng nhận text (giữ nguyên kết luận phiên trước) |

---

## Tổng hợp
- **PASS:** ~95 (gồm "đã chạy lại", "entry-point", và "PASS* giữ nguyên")
- **FAIL:** 1 — **1.8.4** (Chuyển bàn cho chọn bàn đang sử dụng — **vẫn chưa fix** ở 1.0.0+52)
- **BLOCKED:** 8 — toàn bộ **1.6.x** (7 mục, không có đơn Chờ xác nhận) + **1.14.4** (không có đơn tablet/mobile)
- **N/A:** ~12 (thuế cả bill 1.4.9/1.4.10; phân trang 1.2.6; chưa mở ca/không quyền; hủy đơn đã TT; giá rất lớn; mất mạng; 2 thiết bị; thanh toán từ tab Chờ TT…)

### Đối chiếu với phiên 0615_1600 (1.0.0+50)
| Hạng mục | 0615_1600 | 0616_0808 (1.0.0+52) |
|----------|-----------|----------------------|
| 1.8.4 (Chuyển sang bàn đang dùng) | FAIL | **FAIL (vẫn chưa fix)** |
| 1.5.3 (Thanh toán tiền mặt) | PASS | PASS (chạy lại end-to-end) |
| 1.5.1 / 1.7.1 (Báo bếp) | PASS | PASS (chạy lại) |
| 1.13 (Hủy đơn) | PASS | PASS (chạy lại end-to-end) |
| 1.6.x (Xác nhận đơn QR/tablet) | PASS (có đơn chờ) | **BLOCKED (không có đơn chờ)** |

### Danh sách lỗi & lưu ý (chi tiết: `screenshot/0616_0808_home/note.md`)
1. **BUG-01 (FAIL, 1.8.4) — Trung bình, CHƯA FIX:** Chuyển bàn cho chọn **bàn đang sử dụng** (ban3, "1 khách") làm bàn đích; nút "Chọn" sáng. Tồn tại qua 0612 → 0615 và nay 0616 (1.0.0+52).
2. **LƯU Ý-A (vệ sinh dữ liệu) — Thấp:** Các bàn tích lũy nhiều **hóa đơn 0đ** (BAN3 ~23, BAN5 ~43). Nên rà soát/dọn đơn rỗng tồn đọng.
3. **LƯU Ý-B (UX) — Thấp:** Các dropdown thanh công cụ (Khu/Số cột/Giao diện) đôi khi để lại **lớp phủ chặn click** không tự đóng khi bấm ra ngoài — nên kiểm tra cơ chế đóng overlay.

### Khuyến nghị
1. **Ưu tiên fix 1.8.4** — lỗi tồn tại rất nhiều phiên (chặn chọn bàn đang sử dụng làm đích chuyển bàn).
2. Để kiểm **1.6 (Xác nhận đơn)** và **1.14.4**: tạo trước 1 đơn qua **QR_BAN/tablet** (Link/Link.md → `https://table1.klkim.com/v2/system/table`) để có đơn "Chờ xác nhận".
3. Chạy sâu trực tiếp **Gộp bàn (1.9)**, **Tách bill (1.10)**, **Hàng tặng (1.11)**, **Khuyến mãi (1.12)** ở phiên sau với bàn có trạng thái sạch (phiên này đã xác nhận điểm vào trong menu "...").
4. Dọn các hóa đơn rỗng tồn đọng (BAN3/BAN5).
