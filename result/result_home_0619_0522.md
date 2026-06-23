# Kết quả kiểm thử — HOME

- Menu: home
- Ngày giờ: 19/06 05:22
- Người/agent thực hiện: Claude
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Casher (Thu ngân) — CN1
- Trình duyệt: Chrome
- Ghi chú chung: App nền Flutter web (canvas), một số dropdown chỉ có 1 lựa chọn được cấu hình. Công cụ chụp màn hình của phiên KHÔNG lưu được ảnh ra đĩa, nên các lỗi được mô tả chi tiết bằng chữ kèm số liệu thực tế (thư mục `screenshot/0619_0522_home/`).

## Bảng kết quả

### 1.1 Sơ đồ bàn
| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.1.1 | Hiển thị danh sách bàn theo khu | PASS | Hiện đủ bàn; "Tất cả (15)" |
| 1.1.2 | Lọc "Bàn trống" | PASS | Chỉ hiện bàn trống (9) |
| 1.1.3 | Lọc "Đang sử dụng" | PASS | Đúng 5 bàn, khớp số đếm |
| 1.1.4 | Lọc "Chờ xác nhận" | PASS | (0) — hiện empty state đúng |
| 1.1.5a | Lọc "Chờ thanh toán" | PASS | (1) — chỉ 1 bàn |
| 1.1.5b | Lọc theo khu (khu 1 / khu 2) | PASS | khu 2 → 2 bàn. *Lưu ý: số đếm các tab trạng thái là toàn cục, không đổi theo khu* |
| 1.1.6 | Đổi số cột hiển thị | N/A | Dropdown chỉ có 1 lựa chọn "4 cột" — không đổi được |
| 1.1.7 | Đổi giao diện (1/2/3) | N/A | Dropdown "Giao diện" chỉ có "Giao diện 2"; "Danh sách" cũng chỉ 1 lựa chọn |
| 1.1.8 | Thẻ bàn hiển thị thông tin | PASS | Đủ tên, timer, icon HĐ, icon khách, tổng tiền, nhãn trạng thái |
| 1.1.9 | Tổng tiền trên thẻ bàn | KHÔNG KIỂM THỬ | Quan sát tổng tiền hiển thị hợp lý; chưa đối chiếu chi tiết "gồm/không gồm thuế" |
| 1.1.10 | Trạng thái "Chưa báo bếp" | PASS | BAN4/BAN7 hiện "Chưa báo bếp" khi có món chưa gửi |
| 1.1.11 | Nút "Xác nhận" trên thẻ | N/A | Không có đơn "Chờ xác nhận" (0) |
| 1.1.12 | Bấm vào bàn | PASS | Mở màn hình Order |
| 1.1.13 | Thêm đơn mang về | PASS | "BÀN MANG VỀ" → mở Order chế độ Mang đi |
| 1.1.14 | Số liệu các tab nhất quán | PASS | 9+5+0+1 = 15 = "Tất cả" |

### 1.2 Menu (Thực đơn)
| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.2.1 | Hiển thị danh mục món | PASS | Đủ tab: Tất cả, Bán chạy, Món mới, Nước ngọt... |
| 1.2.2 | Lọc theo danh mục | PASS | Danh sách đổi khi chọn danh mục (một số món test gán nhiều danh mục) |
| 1.2.3 | Tìm món (F1) | PASS | Tìm "trà" ra "Trà A hỷ" — không phân biệt dấu, khớp chuỗi con |
| 1.2.4 | Ẩn/hiện hình ảnh | PASS | Toggle "Hiện ảnh" bật/tắt ảnh đúng |
| 1.2.5 | Đổi số cột hiển thị món | PASS | Có 2/3/4/5 cột; đổi sang 4 cột → bố cục lại đúng |
| 1.2.6 | Phân trang (1/5...) | N/A | Lưới món cuộn liên tục, không có chỉ số phân trang |
| 1.2.7 | Giá món | PASS | Hiển thị đúng định dạng VND |

### 1.3 Modal tùy chọn món
| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.3.1 | Mở modal khi món có tùy chọn | PASS | "comboo 10" → modal "Chọn món kèm theo" |
| 1.3.2 | Chọn thuộc tính (Size...) | PASS | Món "ORDER" có Size S(+0)/M(+10.000)/LL(+20.000) — giá đổi theo |
| 1.3.3 | Chọn món thêm | PASS | Nhóm Lẩu/Nước ngọt/Nước chế biến; ràng buộc tối đa 1 hoạt động (đổi FIFO → bỏ chọn cũ) |
| 1.3.4 | Tăng/giảm số lượng | PASS | + nhân giá ×SL; − không xuống dưới 1 |
| 1.3.5 | Nhập ghi chú | PASS | Ghi chú lưu kèm dòng món |
| 1.3.6 | Bấm "Thêm vào giỏ hàng" | PASS | Món + tùy chọn thêm vào hóa đơn |
| 1.3.7 | Bấm "Đóng" không thêm | KHÔNG KIỂM THỬ | Đã đóng modal bằng nút X ở các bước khác |
| 1.3.8 | Tùy chọn hiển thị trong dòng món | PASS | Dòng hiện FIFO/Nuoc trai cay/test0 + ghi chú |

### 1.4 Hóa đơn / Giỏ hàng
| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.4.1 | Thêm món vào hóa đơn | PASS | Dòng món xuất hiện, "Tổng tiền hàng (n)" tăng |
| 1.4.2 | Tăng số lượng (+) | PASS | Thành tiền = đơn giá × SL (785.010×2 = 1.570.020). *Tổng tiền hàng/thuế cập nhật trễ ~1-2s (async) rồi mới khớp — không phải lỗi nhưng có độ trễ* |
| 1.4.3 | Giảm số lượng (−) | PASS | Giảm đúng |
| 1.4.4 | Xóa món (nút X/thùng rác) | PASS | Xóa dòng, tổng tiền cập nhật |
| 1.4.5 | Sửa đơn giá thủ công | PASS | Modal "Thay đổi giá bán" — giảm 10% → giá mới 499.500, thành tiền cập nhật |
| 1.4.6 | Ghi chú từng món | PASS | Ghi chú lưu & hiển thị theo dòng |
| 1.4.7 | Tổng tiền (tạm tính) | PASS | = Σ(đơn giá×SL), đối chiếu khớp |
| 1.4.8 | Thuế theo từng món | PASS | comboo 10 ~5%; Test Kho 8 = 10% (50.000/500.000) |
| 1.4.9 | Thuế theo cả bill | KHÔNG KIỂM THỬ | Chưa cấu hình/kiểm tra thuế cấp bill |
| 1.4.10 | Kết hợp thuế món + bill | KHÔNG KIỂM THỬ | |
| 1.4.11 | Tổng tiền thanh toán | PASS | = Tổng hàng + Phụ thu − Giảm + Thuế (đối chiếu 815.986đ) |
| 1.4.12 | Phụ thu | PASS | Nhập 50.000 → tổng +50.000 đúng |
| 1.4.13 | Giảm giá (trực tiếp) | **BLOCKED** | "Chọn mức giảm" rỗng (không có mức cấu hình), ô "Nhập giá trị" bị khóa → không áp được giảm giá trực tiếp. (Voucher/Khuyến mãi vẫn có trong modal) |
| 1.4.15 | Combo / Set menu | PASS | "comboo 10" hiện thành phần + giá kèm theo |
| 1.4.16 | Chọn khách hàng | PASS | Modal "Chọn thành viên"; gán "tranvana"/"Trăm thị bé" vào hóa đơn |
| 1.4.17 | Nhiều hóa đơn / 1 bàn | KHÔNG KIỂM THỬ | Có nút "+" tạo HĐ mới nhưng chưa thực thi |
| 1.4.18 | Đơn các bàn độc lập | PASS | Đơn BAN4/BAN7 và các đơn mang về độc lập, không lẫn |
| 1.4.19 | Hóa đơn trống | PASS | "Giỏ hàng trống...", tổng = 0đ |
| 1.4.20 | Nhân viên phụ trách | KHÔNG KIỂM THỬ | Chưa đối chiếu tên nhân viên trên hóa đơn |

### 1.5 In bếp / Thanh toán
| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.5.1 | In phiếu Bếp (báo bếp) | PASS | "Gửi bếp thành công"; dòng món → "Đã báo bếp" |
| 1.5.2 | Tạm tính | PASS | "In tạm tính thành công" |
| 1.5.3 | Thanh toán tiền mặt | PASS | Hoàn tất, bàn về trống |
| 1.5.4 | Thanh toán chuyển khoản | KHÔNG KIỂM THỬ | Nút "Chuyển khoản" có sẵn; chưa hoàn tất bằng phương thức này |
| 1.5.5 | Thanh toán quẹt thẻ | KHÔNG KIỂM THỬ | Nút "Quẹt Thẻ" có sẵn |
| 1.5.6 | Thanh toán QR tự động | KHÔNG KIỂM THỬ | Nút "QR Tự động" có sẵn |
| 1.5.7 | Tiền thừa | PASS | Khách đưa 1.000.000 − 826.486 = tiền thừa 173.514đ (đúng) |
| 1.5.8 | Chặn hóa đơn trống | KHÔNG KIỂM THỬ | Chưa thử thanh toán hóa đơn rỗng |

### 1.6 Xác nhận đơn (tại bàn / QR / mang về)
| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.6.1–1.6.7 | Xác nhận đơn QR/tablet/mang về | N/A | "Chờ xác nhận (0)" — không có đơn chờ từ QR/tablet để xác nhận trong phiên |

### 1.7 Gửi bếp
| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.7.1 | Gửi bếp sau khi chọn món | PASS | Trạng thái chuyển sang "Đã báo bếp" |
| 1.7.2 | Món chưa gửi bếp | PASS | Hiện "Chờ báo bếp" trên dòng món mới |
| 1.7.3 | Gửi bếp khi giỏ trống | KHÔNG KIỂM THỬ | |
| 1.7.4 | Gửi bếp chỉ áp món mới | PASS | Báo bếp lần 2 chỉ gửi món mới (tran chau), món cũ không gửi lại |

### 1.8 Chuyển bàn
| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.8.1 | Mở chức năng chuyển bàn | PASS | Modal "Chọn bàn chuyển đến" — có tab trạng thái + lọc khu |
| 1.8.2 | Bàn đích màu vàng | PARTIAL | Bàn hiện tại bị mờ ("Bàn hiện tại"); các bàn đích đều màu kem, không phân biệt màu vàng/khác rõ rệt |
| 1.8.3 | Chọn bàn trống để chuyển | PASS | Chuyển ban4 → ban7 "Chuyển bàn thành công" |
| 1.8.4 | Chỉ cho chọn bàn trống | KHÔNG KIỂM THỬ | (Đã chuyển vào bàn trống thành công) |
| 1.8.5 | Chưa mở ca / không quyền | N/A | Tài khoản admin đủ quyền, ca đang mở |
| 1.8.6 | Dữ liệu đơn giữ nguyên | PASS | Món, tổng tiền, khách hàng (Trăm thị bé) giữ nguyên ở ban7 |
| 1.8.7 | Trạng thái cập nhật ngay | PASS | Trang chủ cập nhật ngay, không cần F5 |
| 1.8.8 | Chuyển khi món đã gửi bếp | PASS | coca cola "Đã báo bếp" giữ nguyên trạng thái sau chuyển |
| 1.8.9 | Hủy thao tác giữa chừng | KHÔNG KIỂM THỬ | (Đã kiểm "Đóng" tương tự ở Tách bill — không thay đổi) |
| — | *Cảnh báo phụ* | LƯU Ý | Toast "Không tìm thấy cấu hình máy in phiếu chuyển bàn" — thiếu cấu hình máy in (không ảnh hưởng việc chuyển) |

### 1.9 Gộp bàn
| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.9.1–1.9.11 | Gộp bàn | KHÔNG KIỂM THỬ | Mục "Gộp bàn" tồn tại trong menu "..." của bàn dine-in; chưa thực thi gộp để tránh xáo trộn nhiều bàn |

### 1.10 Tách / ghép đơn
| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.10.1 | Mở chức năng tách/ghép | PASS | Giao diện "Tách bill": chọn Bàn nhận + Hóa đơn nhận, bảng món nguồn |
| 1.10.3 | Hiển thị đúng thông tin bàn nguồn | PASS | coca cola (SL tối đa 1), Món chế biến (SL tối đa 2) |
| 1.10.19 | Bấm "Đóng" giữa chừng | PASS | Đóng → đơn giữ nguyên |
| 1.10.x (còn lại) | Thực thi tách/ghép | KHÔNG KIỂM THỬ | Chưa thực thi tách/ghép thực tế |

### 1.11 Hàng tặng
| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.11.1 | Mở chức năng hàng tặng | PASS | Banner "ĐANG TRONG CHẾ ĐỘ CHỌN HÀNG TẶNG (TẶNG 100%)" |
| 1.11.2 | Chọn món tặng áp vào đơn | PASS | "tran chau" thêm với giá 0đ |
| 1.11.3 | Chọn lý do tặng | PASS | Modal "Nhập lý do hàng tặng" (Khách hàng thân thiết) |
| 1.11.4 | Món tặng hiển thị trong đơn | PASS | Badge "Hàng tặng kèm", 0đ |
| 1.11.5 | Hàng tặng không cộng vào tổng | PASS | Tổng thanh toán giữ nguyên 1.010.500đ |
| 1.11.6 | Đơn không thỏa điều kiện | KHÔNG KIỂM THỬ | |

### 1.12 Áp dụng khuyến mãi
| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.12.1 | Mở chức năng khuyến mãi | PASS | Mục "Khuyến mãi" trong menu + phần "Khuyến mãi" trong modal giảm giá |
| 1.12.4 | Đơn không thỏa điều kiện | PASS (quan sát) | Hiển thị "Chưa có khuyến mãi" với đơn hiện tại |
| 1.12.x (còn lại) | Áp / bỏ CTKM | KHÔNG KIỂM THỬ | Không có CTKM đủ điều kiện để áp trong phiên |

### 1.13 Hủy đơn
| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.13.1 | Hủy đơn chưa thanh toán | BLOCKED | Đơn đã có món báo bếp → hệ thống chặn hủy |
| 1.13.2 | Chọn lý do hủy (bắt buộc) | PASS | Trường "Lý do hủy *" bắt buộc, có cảnh báo không thể hoàn tác |
| 1.13.3 | Xác nhận hủy | BLOCKED | Báo lỗi "Exception: Đã có món báo bếp, không thể hủy". *UX: thông điệp lộ chữ "Exception:" thô* |
| 1.13.4–1.13.5 | Hủy đơn đã TT / không quyền | KHÔNG KIỂM THỬ | |

### 1.14 Thanh toán đơn hàng (qua Chờ thanh toán)
| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.14.1 | Tab "Chờ thanh toán" hiển thị đơn chờ | PASS | (1) → đúng bàn chờ thanh toán |
| 1.14.2 | Thanh toán từ tab Chờ thanh toán | PASS | "Thanh toán thành công"; bàn về trống, số đếm giảm (5→4, chờ TT 1→0) |
| 1.14.3 | Thanh toán bằng chọn bàn đang dùng | PASS | Đã thanh toán qua mở bàn trực tiếp |
| 1.14.4 | Thanh toán đơn từ tablet/mobile | N/A | Không có đơn từ thiết bị khách trong phiên |

### 1.15 Trường hợp đặc thù & lỗi
| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.15.1 | Số lượng món = 0 | KHÔNG KIỂM THỬ | |
| 1.15.2 | Giá rất lớn | KHÔNG KIỂM THỬ | Có món 999.999đ trong danh mục; chưa stress-test |
| 1.15.3 | Làm tròn tiền VND | PASS (quan sát) | Thuế/tổng hiển thị số nguyên, không lẻ thập phân |
| 1.15.4 | Mất mạng khi thanh toán | KHÔNG KIỂM THỬ | Không thể ngắt mạng trong phiên |
| 1.15.5 | Hai thu ngân cùng 1 bàn | KHÔNG KIỂM THỬ | Chỉ 1 phiên |
| 1.15.6 | Ghi chú có dấu / ký tự đặc biệt | PARTIAL | Đã nhập ghi chú dạng "ghi chu test - it da" lưu OK; chưa test @#! và đầy đủ tiếng Việt có dấu |

## Tổng hợp
- PASS: 47
- FAIL: 0
- BLOCKED: 3 (1.4.13 Giảm giá trực tiếp; 1.13.1 & 1.13.3 Hủy đơn khi đã báo bếp)
- N/A: 11 (chủ yếu do môi trường: không có đơn Chờ xác nhận/QR/tablet, dropdown 1 lựa chọn, đủ quyền/ca)
- KHÔNG KIỂM THỬ: 22 (các thao tác phá hủy dữ liệu nhiều bàn / cấu hình đặc biệt / cần điều kiện không có sẵn)

## Danh sách lỗi & điểm cần lưu ý
1. **[1.4.13] Giảm giá trực tiếp không dùng được**
   - Tái hiện: Order → menu "..." → Giảm giá → "Giảm giá trực tiếp".
   - Kỳ vọng: chọn mức giảm và nhập % để giảm.
   - Thực tế: dropdown "Chọn mức giảm" rỗng (không có mức cấu hình); ô "Nhập giá trị" bị khóa, không nhập được. → Không áp được giảm giá trực tiếp.
   - Mức độ: cao (chặn nghiệp vụ). Có thể do cấu hình "mức giảm" chưa được thiết lập.

2. **[1.13.1/1.13.3] Hủy đơn báo lỗi kỹ thuật thô**
   - Tái hiện: mở bàn có món "Đã báo bếp" → bấm X cạnh tab hóa đơn → chọn lý do → Xác nhận.
   - Thực tế: chặn hủy với thông điệp "Exception: Đã có món báo bếp, không thể hủy".
   - Nhận xét: chặn hủy khi đã báo bếp là hợp lý về nghiệp vụ, nhưng thông điệp lỗi lộ chữ "Exception:" (thô về UX) → nên đổi sang thông báo thân thiện.

3. **[1.8 / Chuyển bàn] Thiếu cấu hình máy in phiếu chuyển bàn**
   - Khi chuyển bàn thành công vẫn kèm toast "Không tìm thấy cấu hình máy in phiếu chuyển bàn." → cần cấu hình máy in hoặc ẩn cảnh báo nếu không bắt buộc.

4. **[1.4.2] Độ trễ cập nhật tổng tiền/thuế khi đổi số lượng**
   - Khi tăng SL, dòng "Thành tiền" cập nhật ngay nhưng "Tổng tiền hàng" và "Thuế sản phẩm" cập nhật trễ ~1–2 giây (tính lại async). Cuối cùng số liệu khớp đúng — không phải lỗi tính toán, nhưng có thể gây hiểu nhầm trong khoảnh khắc.

5. **[1.1.5 / lọc khu] Số đếm tab trạng thái không theo khu**
   - Khi lọc khu 2, danh sách bàn hiển thị đúng theo khu nhưng số đếm các tab ("Tất cả", "Bàn trống"...) vẫn là tổng toàn cục. Cần xác nhận đây là thiết kế mong muốn.

> Ghi chú ảnh: Công cụ chụp màn hình trình duyệt trong phiên không lưu được ảnh ra đĩa, nên thư mục `screenshot/0619_0522_home/` chỉ chứa README mô tả; các lỗi đã được ghi chi tiết kèm số liệu thực tế ở trên thay cho ảnh.
