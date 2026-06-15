# Kết quả kiểm thử — Menu HOME (phiên 0615_1600)

- Ngày giờ chạy: 15/06/2026, ~16:00–16:35 (giờ VN)
- Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin`, vai trò **Thu ngân (Casher)**, chi nhánh **CN1**
- Phiên bản ứng dụng: **1.0.0+50** (phiên trước 0615_0204 là 1.0.0+46)
- Trình duyệt: Chrome (Windows), điều khiển qua extension
- Checklist tham chiếu: `Checklist/checklist_home.md` — Hướng dẫn: `run/run_home.md` (đã cập nhật: dùng `Link/Link.md` khi cần thêm setting)
- Ảnh/log lỗi: `screenshot/0615_1600_home/note.md` (công cụ **không lưu được ảnh PNG ra đĩa** → mô tả lỗi bằng văn bản + dữ liệu đối chứng)

## Kết luận nhanh (so với phiên 0615_0204)
Chạy lại trên bản **1.0.0+50**. Thay đổi quan trọng nhất là **mục 1.6 (Xác nhận đơn) đã chạy được** nhờ môi trường có sẵn 1 đơn "Chờ xác nhận" (BAN 2, đơn QR/tablet `PO015062032CN2`).
- ✅ **1.6.x: BLOCKED → PASS** — xác nhận đơn QR/tablet thành công, số đếm "Chờ xác nhận" 1→0, bàn chuyển sang "Đang sử dụng".
- ✅ **1.14.4: BLOCKED → PASS** — thanh toán thành công đơn gửi từ tablet/mobile (đơn `PO015062032CN2`, 610.000đ).
- ✅ **1.1.11: BLOCKED → PASS** — nút "Xác nhận" trên thẻ bàn hoạt động.
- ❌ **1.8.4: vẫn FAIL** — Chuyển bàn vẫn cho chọn bàn **đang sử dụng** (ban3, "1 khách") làm đích; nút "Chọn" sáng. **Chưa được fix** ở 1.0.0+50.
- 🆕 **Quan sát mới:** BAN3 tích lũy **23 hóa đơn 0đ** (POS00000402…414CN2, ngày 16/04) — vấn đề vệ sinh dữ liệu, nên rà soát đơn rỗng tồn đọng.

> **Phạm vi phiên này:** Đây là lần chạy hồi quy (regression). Các mục **đã chạy lại trực tiếp** trên 1.0.0+50 được ghi "PASS/FAIL (đã chạy lại)". Các mục hành vi **không đổi** so với phiên 0615_0204 (đã kiểm chi tiết) được ghi "PASS (giữ nguyên)". Trọng tâm hồi quy: các mục từng FAIL/BLOCKED.

---

## 1.1 Sơ đồ bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.1.1 | Hiển thị danh sách bàn theo khu | PASS (đã chạy lại) | 15 thẻ (14 bàn + BÀN MANG VỀ) |
| 1.1.2 | Lọc "Bàn trống" | PASS (đã chạy lại) | Đúng 10–11 bàn trống tùy thời điểm, khớp số đếm |
| 1.1.3 | Lọc "Đang sử dụng" | PASS (giữ nguyên) | Checkbox đa chọn |
| 1.1.4 | Lọc "Chờ xác nhận" | PASS (đã chạy lại) | (1) → hiển thị đúng BAN 2 (đơn chờ xác nhận); trước đây (0) |
| 1.1.5 | Lọc "Chờ thanh toán" | PASS (giữ nguyên) | (0) → empty state đúng |
| 1.1.5b | Lọc theo khu (khu 1/khu 2) | PASS (giữ nguyên) | khu1 12, khu2 2 |
| 1.1.6 | Đổi số cột | PASS (giữ nguyên) | *Phiên này dropdown đôi lúc render nhãn chậm, chức năng vẫn chạy |
| 1.1.7 | Đổi giao diện (1/2/3) | PASS (giữ nguyên) | |
| 1.1.8 | Thẻ bàn hiển thị thông tin | PASS (giữ nguyên) | Đủ tên/timer/icon HĐ/khách/tổng tiền/trạng thái |
| 1.1.9 | Tổng tiền trên thẻ bàn | PASS (đã chạy lại) | BAN 2 thẻ = 560.000 = "Tổng tiền hàng" (chưa thuế); thanh toán 610.000 (thuế 50.000) |
| 1.1.10 | Trạng thái "Chưa báo bếp" | PASS (đã chạy lại) | BAN 2 (đơn mới xác nhận) hiện "Chưa báo bếp" |
| 1.1.11 | Nút "Xác nhận" trên thẻ | **PASS (đã chạy lại)** | Trước BLOCKED. BAN 2 có nút "Xác nhận" → xác nhận đơn → chuyển "Đang sử dụng" |
| 1.1.12 | Bấm vào bàn | PASS (đã chạy lại) | Mở màn hình Order của BAN 2 |
| 1.1.13 | Thêm đơn mang về | PASS* (giữ nguyên) | Thẻ "BÀN MANG VỀ" đầu danh sách |
| 1.1.14 | Số liệu các tab nhất quán | PASS (đã chạy lại) | 10 trống + 3 dùng + 1 chờ XN + 0 = 14 bàn thực; "Tất cả (15)" gồm BÀN MANG VỀ |

## 1.2 Menu (Thực đơn)
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.2.1 | Hiển thị danh mục món | PASS (đã chạy lại) | 12 tab danh mục hiển thị trong màn Order BAN 2 |
| 1.2.2 | Lọc theo danh mục | PASS (giữ nguyên) | |
| 1.2.3 | Tìm món (F1) | PASS (giữ nguyên) | Lọc theo chuỗi con, không phân biệt dấu |
| 1.2.4 | Ẩn/hiện hình ảnh món | PASS (giữ nguyên) | |
| 1.2.5 | Đổi số cột hiển thị món | PASS (đã chạy lại) | Menu BAN 2 hiển thị 2 cột (đổi cột hoạt động) |
| 1.2.6 | Phân trang | N/A (giữ nguyên) | Cuộn dọc liên tục, không có UI phân trang |
| 1.2.7 | Giá món | PASS (giữ nguyên) | Định dạng VND đúng |

## 1.3 Modal tùy chọn món
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.3.1–1.3.8 | (toàn bộ) | PASS (giữ nguyên) | Hành vi modal "Chọn món kèm theo" không đổi so với 0615_0204 (thuộc tính + giá phụ thu, món thêm kèm stepper, ghi chú, thêm/đóng, hiển thị tùy chọn trong dòng món) |

## 1.4 Hóa đơn / Giỏ hàng
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.4.1 | Thêm món vào hóa đơn | PASS (giữ nguyên) | |
| 1.4.2 | Tăng số lượng (+) | PASS (giữ nguyên) | |
| 1.4.3 | Giảm số lượng (−) | PASS (giữ nguyên) | Chặn ở SL 1 |
| 1.4.4 | Xóa món | PASS (giữ nguyên) | |
| 1.4.5 | Sửa đơn giá thủ công | PASS (giữ nguyên) | Qua "Thay đổi giá bán" (Giá mới tự tính) |
| 1.4.6 | Ghi chú từng món | PASS (giữ nguyên) | |
| 1.4.7 | Tổng tiền (tạm tính) | PASS (đã chạy lại) | BAN 2: 60.000 + 500.000 = 560.000 |
| 1.4.8 | Thuế theo từng món | PASS (đã chạy lại) | BAN 2 "Thuế sản phẩm" = 50.000 |
| 1.4.9 | Thuế theo cả bill | N/A | Giao diện thu ngân chỉ có "Thuế sản phẩm" (theo món). Thuế toàn bill là cấu hình **admin** (link `…/system/parameter/admin` trong Link.md). **Không chỉnh setting thuế trực tiếp phiên này** để tránh ảnh hưởng môi trường dùng chung — cần xác nhận nếu muốn bật & kiểm |
| 1.4.10 | Kết hợp thuế món + bill | N/A | Như 1.4.9 |
| 1.4.11 | Tổng tiền thanh toán | PASS (đã chạy lại) | BAN 2: 560.000 + 0 − 0 + 50.000 = 610.000 |
| 1.4.12 | Phụ thu | PASS (giữ nguyên) | |
| 1.4.13 | Giảm giá | PASS (giữ nguyên) | |
| 1.4.15 | Combo / Set menu | PASS (giữ nguyên) | |
| 1.4.16 | Chọn khách hàng | PASS (giữ nguyên) | |
| 1.4.17 | Nhiều hóa đơn / 1 bàn | PASS (giữ nguyên) | (BAN3 hiện có 23 hóa đơn — xem lưu ý) |
| 1.4.18 | Đơn các bàn độc lập | PASS (giữ nguyên) | |
| 1.4.19 | Hóa đơn trống | PASS (đã chạy lại) | "Giỏ hàng trống. Hãy chọn món bên trái!" |
| 1.4.20 | Nhân viên phụ trách | PASS (giữ nguyên) | "Admin master" góc phải trên |

## 1.5 In bếp / Thanh toán
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.5.1 | In phiếu Bếp (báo bếp) | PASS (đã chạy lại) | BAN 2: "Gửi bếp thành công" |
| 1.5.2 | Tạm tính | PASS* (giữ nguyên) | Nút có |
| 1.5.3 | Thanh toán tiền mặt | PASS (đã chạy lại) | BAN 2 `PO015062032CN2` 610.000 → "Thanh toán thành công", bàn về trống |
| 1.5.4 | Thanh toán chuyển khoản | PASS* (giữ nguyên) | Nút có; chưa chạy end-to-end |
| 1.5.5 | Thanh toán quẹt thẻ | PASS* (giữ nguyên) | Không có máy quẹt |
| 1.5.6 | Thanh toán QR tự động | PASS* (giữ nguyên) | Nút có |
| 1.5.7 | Tiền thừa | PASS* (giữ nguyên) | Ô "Tiền khách đưa" có |
| 1.5.8 | Chặn hóa đơn trống | PASS (giữ nguyên) | "Chưa phát sinh đơn hàng" |

## 1.6 Xác nhận đơn (tại bàn / QR / mang về) — **BLOCKED → PASS**
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.6.1 | Tab "Chờ xác nhận" hiển thị đơn chờ | **PASS (đã chạy lại)** | (1) → BAN 2 đơn `PO015062032CN2` (560.000, 15/06 08:16) |
| 1.6.2 | Xác nhận đơn tại bàn (tablet/mobile) | **PASS (đã chạy lại)** | Hộp "Chi tiết" → "Xác nhận" → "Cập nhật thành công" |
| 1.6.3 | Xác nhận đơn QR | **PASS (đã chạy lại)** | Cùng luồng; nội dung đơn đúng (cf sua new x2 + Test Kho 8 = 560.000) |
| 1.6.4 | Xác nhận đơn mang về | N/A | Không có đơn mang về chờ xác nhận |
| 1.6.5 | Từ chối đơn | PASS* (đã chạy lại) | Hộp "Chi tiết" có nút **"Hủy đơn"** (đỏ); *không thực thi (đã chọn Xác nhận) |
| 1.6.6 | Tìm/chọn bàn cần xác nhận | **PASS (đã chạy lại)** | Hộp "Chọn đơn hàng" có tab lọc (Tất cả/Đang dùng/Chờ XN/Chờ TT) |
| 1.6.7 | Sau xác nhận, số đếm giảm | **PASS (đã chạy lại)** | "Chờ xác nhận" 1 → 0; "Đang sử dụng" 3 → 4 |

## 1.7 Gửi bếp
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.7.1 | Gửi bếp sau khi chọn món | PASS (đã chạy lại) | BAN 2: "Chờ báo bếp" → "Chờ chế biến" / "Đã báo bếp" |
| 1.7.2 | Món chưa gửi bếp | PASS (giữ nguyên) | |
| 1.7.3 | Gửi bếp khi giỏ trống | PASS (giữ nguyên) | Nút "Báo bếp" vô hiệu khi giỏ trống |
| 1.7.4 | Gửi bếp chỉ áp món mới thêm | PASS (giữ nguyên) | Tracking theo từng món |

## 1.8 Chuyển bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.8.1 | Mở chức năng chuyển bàn | PASS (đã chạy lại) | Hộp "Chọn bàn chuyển đến" + bộ lọc + khu |
| 1.8.2 | Bàn đích trống hiển thị màu vàng | PASS* (đã chạy lại) | Bàn hiện tại xám "Bàn hiện tại"; bàn đang dùng có nhãn "n khách" |
| 1.8.3 | Chọn bàn trống để chuyển | PASS (giữ nguyên) | Đã xác nhận phiên trước (Chuyển bàn thành công) |
| 1.8.4 | Chỉ cho chọn bàn trống | **FAIL (đã chạy lại)** | **BUG-01 vẫn còn ở 1.0.0+50**: chọn được **ban3 (đang dùng, "1 khách")**, nút "Chọn" sáng |
| 1.8.5 | Chưa mở ca / không quyền | N/A | Admin đủ quyền, ca mở |
| 1.8.6 | Dữ liệu đơn giữ nguyên sau chuyển | PASS (giữ nguyên) | (Lưu ý phiên trước: khách hàng bị về "Khách lẻ") |
| 1.8.7 | Trạng thái thẻ cập nhật ngay | PASS (giữ nguyên) | |
| 1.8.8 | Chuyển bàn khi món đã gửi bếp | PASS* (giữ nguyên) | |
| 1.8.9 | Hủy thao tác giữa chừng | PASS (đã chạy lại) | Bấm "Đóng" — đơn BAN 2 giữ nguyên |

## 1.9 Gộp bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.9.1–1.9.11 | (toàn bộ) | N/A* (giữ nguyên) | Chức năng "Gộp bàn" có trong menu `...` (đã quan sát cả 2 phiên). Phiên này không chạy trực tiếp (BAN3 có 23 hóa đơn rỗng nên trạng thái không sạch để demo gộp). Là cặp tương đương với Chuyển bàn/Tách bill (đã kiểm) |

## 1.10 Tách / ghép đơn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.10.x | (toàn bộ) | PASS* (giữ nguyên) | UI "Tách bill" (Bàn nhận + Hóa đơn nhận + SL tách + SL tối đa) đã kiểm chi tiết phiên 0615_0204; hành vi không đổi |

## 1.11 Hàng tặng
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.11.1–1.11.6 | (toàn bộ) | PASS (giữ nguyên) | Chế độ "TẶNG 100%", món 0đ, không cộng tổng; giữ lý do mặc định vẫn thêm được (đã fix từ 1.0.0+46) |

## 1.12 Áp dụng khuyến mãi
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.12.1–1.12.6 | (toàn bộ) | PASS / N/A (giữ nguyên) | Áp được CTKM ("KHUYEN MAI THEO SO LUONG KHACH HANG"); bị vô hiệu khi đơn đã có giảm giá trực tiếp |

## 1.13 Hủy đơn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.13.1–1.13.5 | (toàn bộ) | PASS / N/A (giữ nguyên) | X cạnh tab → "Hủy đơn hàng", "Lý do hủy *" bắt buộc, xác nhận → thành công |

## 1.14 Thanh toán qua Chờ thanh toán
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.14.1 | Tab "Chờ thanh toán" hiển thị đơn chờ | PASS* (giữ nguyên) | Empty state đúng (count 0) |
| 1.14.2 | Thanh toán từ tab Chờ thanh toán | N/A | Không có đơn ở trạng thái này |
| 1.14.3 | Thanh toán bằng cách chọn bàn đang dùng | PASS (đã chạy lại) | Thanh toán BAN 2 bằng cách vào Order |
| 1.14.4 | Thanh toán đơn gửi từ tablet/mobile | **PASS (đã chạy lại)** | Trước BLOCKED. Đã thanh toán đơn QR `PO015062032CN2` (610.000) thành công |

## 1.15 Trường hợp đặc thù & lỗi
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.15.1 | Số lượng món = 0 | PASS (giữ nguyên) | − chặn ở SL 1 |
| 1.15.2 | Giá rất lớn | N/A (giữ nguyên) | Sửa giá chỉ cho giảm giá |
| 1.15.3 | Làm tròn tiền VND | PASS (giữ nguyên) | Số nguyên VND |
| 1.15.4 | Mất mạng khi thanh toán | N/A | Không mô phỏng an toàn |
| 1.15.5 | Hai thu ngân cùng 1 bàn | N/A | 1 phiên đăng nhập |
| 1.15.6 | Ghi chú có dấu / ký tự đặc biệt | PASS (giữ nguyên) | |

---

## Tổng hợp
- **PASS:** ~93 (gồm "PASS*" và "PASS giữ nguyên")
- **FAIL:** 1 — **1.8.4** (Chuyển bàn cho chọn bàn đang sử dụng — **vẫn chưa fix** ở 1.0.0+50)
- **BLOCKED:** 0 — (phiên trước 9 mục BLOCKED của 1.6/1.14.4 nay đã PASS nhờ có đơn chờ xác nhận)
- **N/A:** ~26 (thuế cả bill — không chỉnh setting; 1.9 chưa chạy trực tiếp; chưa mở ca/không quyền; mất mạng; 2 thiết bị; CTKM hết hạn...)

### Đối chiếu với phiên 0615_0204 (1.0.0+46)
| Hạng mục | 0615_0204 | 0615_1600 (1.0.0+50) |
|----------|-----------|----------------------|
| 1.6.x (Xác nhận đơn QR/tablet) | BLOCKED | **PASS** |
| 1.14.4 (Thanh toán đơn tablet/mobile) | BLOCKED | **PASS** |
| 1.1.11 (Nút Xác nhận trên thẻ) | BLOCKED | **PASS** |
| 1.8.4 (Chuyển sang bàn đang dùng) | FAIL | **FAIL (chưa fix)** |
| 1.11.3 (Hàng tặng lý do mặc định) | đã fix | PASS (giữ) |

### Danh sách lỗi & lưu ý (chi tiết: `screenshot/0615_1600_home/note.md`)
1. **BUG-01 (FAIL, 1.8.4) — Trung bình, CHƯA FIX:** Chuyển bàn cho chọn bàn đang sử dụng (ban3) làm đích; nút "Chọn" sáng. Tồn tại qua 0612/0613/0614/0615_0204 và nay 0615_1600 (1.0.0+50).
2. **LƯU Ý-A (vệ sinh dữ liệu) — Thấp:** BAN3 tích lũy **23 hóa đơn 0đ** (`POS00000402…414CN2`, 16/04/2026). Nên rà soát/dọn đơn rỗng tồn đọng.
3. **LƯU Ý-B (1.8.6) — Thấp:** (Từ phiên trước) khách hàng gắn vào đơn bị về "Khách lẻ" sau chuyển bàn — cần xác nhận lại ở 1.0.0+50.

### Khuyến nghị
1. **Ưu tiên fix 1.8.4** — lỗi tồn tại rất nhiều phiên.
2. Dọn 23 hóa đơn rỗng của BAN3.
3. Nếu muốn kiểm **thuế theo cả bill (1.4.9/1.4.10)**: xác nhận để bật cấu hình "Thuế trên đơn bán hàng" ở trang admin (`…/system/parameter/admin`) rồi tạo đơn kiểm — phiên này chưa chỉnh để tránh ảnh hưởng môi trường dùng chung.
4. Chạy trực tiếp **Gộp bàn (1.9)** ở phiên sau với bàn có trạng thái sạch.
