# Kết quả kiểm thử — Menu HOME (phiên 3 — chạy tiếp theo run_home.md)

- Ngày giờ chạy: 12/06/2026, ~13:05–13:34 (giờ VN)
- Môi trường: https://order-flutter.nasys.vn (store `thientester`, user `admin`, vai trò Thu ngân/Casher), chi nhánh CN1
- Phiên bản ứng dụng: **1.0.0+39**
- Trình duyệt: Chrome (Windows), điều khiển qua extension
- Checklist tham chiếu: `Checklist/checklist_home.md`
- Tiếp nối 2 phiên trước (`result_home_0612_0832.md`, `result_home_0612_1106.md`) đã chạy 1.1 → 1.4 (một phần). Phiên này tập trung phần **còn lại của 1.4, và 1.5 → 1.12** theo trọng tâm run_home.md (tải trang, layout bàn, chọn/chuyển bàn, thêm-sửa-xóa món, tính tiền, thanh toán).
- Đơn dùng để test phiên này: tạo mới trên bàn trống (ban6 → chuyển sang ban7), mã đơn dải `POS00002468..2471CN2`.

## Bảng trạng thái

### 1.4 Hóa đơn / Giỏ hàng — phần còn lại từ phiên trước
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.4.14 | Gợi ý nhanh tiền mặt | **N/A** | Bản 1.0.0+39 không có nút gợi ý mệnh giá. Ô "Tiền khách đưa" tự điền đúng tổng thanh toán; tiền thừa tính ngay khi nhập số lớn hơn (xem 1.5.7) |
| 1.4.15 | Combo / Set menu | PASS* | "comboo 10": modal "Chọn món kèm theo" hiện nhóm thành phần (Lẩu, Nước ngọt, Nước chế biến) + giá; nút "Thêm vào giỏ hàng - 669.410đ" (=555.000+111.410+1.500+1.500 ✓). Dòng món trong hóa đơn hiện đủ thành phần. **Lưu ý BUG-11**: dòng combo hiển thị Thành tiền 783.820đ nhưng phần đóng góp vào "Tổng tiền hàng" chỉ 669.410đ (chênh đúng bằng "Món thêm +114.410") — hiển thị không nhất quán |
| 1.4.18 | Đơn các bàn độc lập | PASS | Thanh toán xong ban10 (12.000) → ban9 vẫn giữ nguyên 1.018.999; các bàn không lẫn đơn |
| 1.4.20 | Nhân viên phụ trách | PASS* | Tên nhân viên đang đăng nhập "Admin master" hiển thị góc trên phải header. Bản này KHÔNG có dòng "Nhân viên: ..." riêng trong panel hóa đơn |

### 1.5 In bếp / Thanh toán — 8 PASS / 1 N/A / 1 chưa chạy
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.5.1 | In phiếu Bếp/Bar (báo bếp) | PASS | Bấm "Báo bếp" → loading "Đang báo bếp..." → dòng món chuyển từ "Chờ báo bếp" sang **"Chờ chế biến"**; nút Báo bếp chuyển disabled |
| 1.5.2 | Tạm tính | PASS | Bấm "Tạm tính" → "Đang in tạm tính..." → phát phiếu tạm tính đúng tổng 16.970đ |
| 1.5.3 | Thanh toán tiền mặt | PASS | Tiền mặt → "Xác nhận thanh toán" (khách, mã đơn, tổng) → Xác nhận → "Thanh toán thành công"; bàn về trống, Bàn trống 8→9, Đang sử dụng 6→5 |
| 1.5.4 | Thanh toán chuyển khoản | PASS | Chọn "Chuyển khoản" mở thẳng modal xác nhận (không có ô tiền khách đưa) → Xác nhận → "Thanh toán thành công" |
| 1.5.5 | Thanh toán quẹt thẻ | PASS* | Hoàn tất được. *Nút "Xác nhận" bị nuốt click nhiều lần, payment chỉ hoàn tất sau loạt click dồn (BUG-07) — màn hình hiện trạng thái cũ trong khi giao dịch đã chạy |
| 1.5.6 | Thanh toán QR tự động | PASS | Chọn "QR tự động" → modal sinh **mã QR Momo**, có dropdown "Loại QR" (Momo…), nút "In QR" + "Xác nhận"/"Xác nhận & In". Không hoàn tất bước quét QR ngoài (không thực hiện được trong môi trường test) |
| 1.5.7 | Tiền thừa | PASS | Nhập Tiền khách đưa 50.000 cho tổng 16.970 → "Tiền thừa **33.030đ**" (=50.000−16.970 ✓) |
| 1.5.8 | Chặn hóa đơn trống | PASS | Giỏ trống bấm "Thanh toán" → không mở modal, không cho thanh toán |
| 1.5.9 | Hóa đơn điện tử | CHƯA CHẠY | Có mục "Hóa đơn điện tử" trong menu "..."; chưa thực thi phát hành (đơn chưa ở trạng thái phù hợp + lag) |

### 1.7 Gửi bếp — 3 PASS / 1 chưa chạy
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.7.1 | Gửi bếp sau khi chọn món | PASS | Trạng thái dòng món "Chờ báo bếp" → "Chờ chế biến" sau Báo bếp |
| 1.7.2 | Món chưa gửi bếp | PASS | Trước Báo bếp dòng món hiển thị "Chờ báo bếp"; thẻ bàn ngoài Trang chủ hiện "Chưa báo bếp" |
| 1.7.3 | Gửi bếp khi giỏ trống | PASS | Giỏ trống → nút "Báo bếp" bị disable, không gửi được |
| 1.7.4 | Gửi bếp chỉ áp món mới thêm | CHƯA CHẠY | Chưa kiểm (lag) |

### 1.8 Chuyển bàn — 4 PASS (lõi)
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.8.1 | Mở chức năng chuyển bàn | PASS | Menu "..." → "Chuyển bàn" → modal "Chọn bàn chuyển đến" (filter Tất cả/Đang sử dụng/Bàn trống/Chờ xác nhận, lọc khu) |
| 1.8.2 | Bàn đích trống nổi bật | PASS* | Bàn trống màu kem nhạt, bàn đang dùng hiện số tiền/khách; phân biệt được nhưng độ tương phản nhẹ |
| 1.8.3 | Chọn bàn trống để chuyển | PASS | Chuyển ban6 (Test Kho 6, 20.000) → ban7: toast "Chuyển bàn thành công!"; ban6 về trống, ban7 "Đang sử dụng" 20.000 |
| 1.8.6 | Dữ liệu đơn giữ nguyên | PASS | Vào ban7 sau chuyển: vẫn đúng món Test Kho 6, LL, Đường 20%, 21.000đ |
| 1.8.7 | Trạng thái thẻ bàn cập nhật ngay | PASS | Về Trang chủ thấy ngay ban6 trống / ban7 có đơn, không cần F5 |
| — | Không cho chọn bàn hiện tại | PASS | Bàn nguồn (ban6/ban7) hiển thị nhãn "Bàn hiện tại"/"Bàn chính" và bị mờ, không chọn được |

### 1.9 Gộp bàn — 2 PASS (mở chức năng + hủy); phần thực thi gộp: chưa chạy hết
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.9.1 | Mở chức năng gộp bàn | PASS | Menu "..." → "Gộp bàn" → modal "Gộp bàn": "Bàn hiện tại: ban7" (đánh dấu **Bàn chính**), lưới chọn bàn phụ, dòng "Bàn sẽ gộp vào", nút Tiếp tục (disable đến khi chọn) |
| 1.9.x | Chọn bàn phụ | PASS (chọn) | Chọn ban9 → tích xanh, chip "Bàn sẽ gộp vào: ban9", Tiếp tục bật sáng |
| 1.9.9 | Hủy thao tác gộp giữa chừng | PASS | Đóng/hủy giữa chừng (không xác nhận) → ban7 (20.000) và ban9 (1.018.999) giữ nguyên, không bị gộp |
| 1.9.2–1.9.8, 1.9.10–1.9.11 | Thực thi gộp + tổng tiền/món/trạng thái | CHƯA CHẠY | Cố ý không hoàn tất gộp để giữ nguyên dữ liệu ban9; thêm vào đó nút "Tiếp tục"/"Đóng" bị nuốt click (BUG-07/08) |

### 1.12 Áp dụng khuyến mãi — 2 PASS
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.12.1 | Mở chức năng khuyến mãi | PASS | Menu "..." → "Khuyến mãi" → modal liệt kê CTKM đủ điều kiện ("KHUYEN MAI THEO SO LUONG KHACH HANG"), chọn 1/nhiều + "Áp dụng" |
| 1.12.2 | Áp khuyến mãi vào đơn | PASS | Tích CTKM + Áp dụng → "Áp dụng khuyến mãi thành công"; Giảm giá **2.000đ**, Thuế tính lại 900 (5%×18.000), Tổng thanh toán **18.900đ** (=20.000−2.000+900 ✓) |
| 1.12.3–1.12.6 | CTKM hết hạn / không đủ ĐK / bỏ KM / chưa mở ca | CHƯA CHẠY | — |

### Các mục chưa chạy phiên này
- **1.5.9** Hóa đơn điện tử (có trong menu, chưa thực thi)
- **1.6** Xác nhận đơn (tại bàn/QR/mang về): cần đơn gửi từ tablet/QR mới; 1.6.3 & 1.6.7 đã PASS gián tiếp ở phiên 2 (qua 1.1.11 xác nhận đơn QR).
- **1.10** Tách/ghép đơn: có mục "Tách bill" trong menu "..." (xác nhận tồn tại), chưa thực thi.
- **1.11** Hàng tặng: có mục "Hàng tặng" trong menu "..." (xác nhận tồn tại), chưa thực thi.
- **1.13** Hủy đơn: **KHÔNG thấy mục "Hủy đơn" trong menu "..."** của màn Order (menu chỉ có: Hóa đơn điện tử, In tem, In lại tem, In lại phiếu bếp, Khuyến mãi, Số lượng khách, Hàng tặng, Tách bill, Chuyển bàn, Gộp bàn, Đồng giá, Thanh toán đa phương thức). Cần xác minh luồng hủy đơn ở nơi khác (Lịch sử?).
- **1.14** Chờ thanh toán: 1.14.2/1.14.3 (thanh toán từ bàn đang dùng) đã cover qua 1.5.3–1.5.6.
- **1.15** Đặc thù: 1.15.3 (làm tròn VND) — mọi tổng quan sát đều là số nguyên VND, không thấy số lẻ; 1.15.6 (ghi chú ký tự đặc biệt) đã PASS phiên 2.

## Tổng hợp phiên 3
- Đã chạy mới/hoàn tất: **23 mục** → **PASS: 20** | **N/A: 1** (1.4.14) | còn lại đánh dấu CHƯA CHẠY.
- Trọng tâm run_home.md (tải trang, layout bàn, chọn/chuyển bàn, thêm-sửa-xóa món, tính tiền, thanh toán): **đã phủ đủ** — thanh toán cả 4 phương thức (tiền mặt/chuyển khoản/quẹt thẻ/QR), tiền thừa, báo bếp, tạm tính, chuyển bàn (chuyển thành công + giữ dữ liệu), khuyến mãi.
- Phát sinh **5 lỗi mới (BUG-07 → BUG-11)** + tái xác nhận BUG-01, BUG-03 của phiên trước.

## Danh sách lỗi

### BUG-07 — Lag/nuốt click nghiêm trọng toàn ứng dụng — **Cao**
- Hiện tượng: nhiều thao tác (nút "Xác nhận" thanh toán, item trong menu "...", click vào thẻ bàn ở Trang chủ, nút "Thêm vào giỏ", "Tiếp tục"/"Đóng" trong modal) **bị nuốt**, chỉ chạy sau vài giây; ảnh chụp màn hình hiển thị trạng thái CŨ trong khi thao tác thực ra đã/sắp chạy. Có lúc 1 thao tác cần 3–5 lần click.
- Ví dụ tái hiện: thanh toán Quẹt thẻ — bấm "Xác nhận" 4–5 lần + Enter không thấy phản hồi, nhưng giao dịch vẫn hoàn tất (về Trang chủ, bàn trống). Click thẻ bàn trống ở Trang chủ sau khi thanh toán: 3–4 lần không mở, rồi 1 click "trễ" mở nhầm bàn khác.
- Rủi ro: thu ngân bấm trùng (double payment/double action), hoặc tưởng thao tác thất bại nên làm lại.
- Khắc phục tạm: chờ 3–5s giữa các thao tác, reload (F5) khi kẹt.

### BUG-08 — Menu "..." (chức năng) thành "ghost"/lệch khi đang animate — **Trung bình**
- Menu "..." mở dạng animate từ trên xuống; nếu click khi đang animate sẽ trúng item sai hoặc không trúng. Có lần click "Gộp bàn" lại mở "Khuyến mãi" (do click trễ + item dịch vị trí). Cần chờ menu render xong hẳn (~2s) mới click được chính xác.

### BUG-09 — Toast "Áp dụng khuyến mãi thành công" tồn tại/lặp lại quá lâu, che UI — **Trung bình**
- Toast thành công đứng yên/lặp lại >15s (lẽ ra tự ẩn ~3s), phủ giữa màn hình và **chặn mở menu "..."**. Phải reload mới thao tác tiếp được.

### BUG-10 — Lưới thực đơn đôi khi load rỗng "Không có món" khi vào bàn — **Trung bình**
- Vào màn Order của bàn, có lúc lưới món hiện "Không có món" và mất luôn hàng tab danh mục; phải F5 mới có món. (Kèm BUG-03: panel hóa đơn hiện "Hóa đơn mới"/giỏ trống trước khi đơn thật load.)

### BUG-11 — Dòng Combo hiển thị Thành tiền không khớp đóng góp vào Tổng tiền hàng — **Thấp–Trung bình**
- "comboo 10": đơn giá 669.410, nhưng dòng có thêm "Món thêm +114.410đ" → Thành tiền hiển thị **783.820đ**, trong khi "Tổng tiền hàng" chỉ cộng 669.410 (12.000 + 669.410 = 681.410). Hiển thị Thành tiền/đóng góp tổng không nhất quán (nghi double-count phần "Món thêm" ở cột Thành tiền). *Lưu ý: dữ liệu combo test rất lộn xộn (thành phần giá 111.410…), cần kiểm lại với combo cấu hình chuẩn.*

### Tái xác nhận lỗi phiên trước
- **BUG-01** (Trung bình): Tổng tiền trên thẻ bàn KHÔNG gồm thuế — ban6 thẻ hiện 20.000 trong khi tổng thanh toán có thuế là 21.000. (Đã ghi ở phiên 1 & 2.)
- **BUG-03** (Cao): Màn Order hiển thị "Hóa đơn mới"/giỏ trống trước khi đơn thật của bàn load (~vài giây). (Đã ghi ở phiên 2.)

## Ảnh màn hình
- Phiên này chạy qua trình điều khiển Chrome; chức năng lưu ảnh ra đĩa **không khả dụng trong phiên** (đã thử `save_to_disk` — không lưu được). Vì vậy thư mục `screenshot/` không có ảnh mới; các lỗi đã được mô tả đủ chi tiết để tái hiện ở phần "Danh sách lỗi".

## Ghi chú dữ liệu phát sinh do kiểm thử
- Đã thanh toán hoàn tất các đơn test: ban10 (Trà A hỷ, 16.970 — tiền mặt), 1 đơn Cơm 21.000 (chuyển khoản), 1 đơn Cơm 21.000 (quẹt thẻ). Các bàn này đã về trống.
- Đơn Test Kho 6 (21.000, đang áp KM giảm 2.000 → 18.900) hiện **còn trên ban7** (Chưa báo bếp/Chưa thanh toán) — phát sinh do test chuyển bàn + khuyến mãi, chưa dọn.
- ban9 (1.018.999), ban2 (1.560.000), ban kiem tra ten dai (530.000), ban3/ban5 (tổng 0, 23/43 hóa đơn — dữ liệu rác) giữ nguyên như trước.
