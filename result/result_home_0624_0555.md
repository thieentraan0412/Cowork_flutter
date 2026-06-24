# Kết quả kiểm thử — HOME

- Menu: home
- Ngày giờ: 24/06 05:55 (UTC)
- Người/agent thực hiện: Claude (Cowork)
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Thu ngân (Casher) — CN1 — ca đang hoạt động
- Trình duyệt: Chrome (qua tiện ích điều khiển) — Browser 1
- Thư mục ảnh lỗi: `screenshot/0624_0555_home/`

## Ghi chú chung về môi trường kiểm thử
- App nền **Flutter web (CanvasKit/canvas)**. Hai giới hạn tự động hóa quan trọng (đã kiểm chứng lại trong phiên này):
  1. **Không nhập được chữ vào ô input của Flutter**: gõ phím thật (CDP), set value qua DOM, `execCommand('insertText')`, dispatch `InputEvent`, đều KHÔNG đồng bộ vào controller của Flutter → **không đăng nhập tự động được** (đã nhờ người dùng đăng nhập tay) và **ô tìm món (1.2.3) không nhập được**.
  2. **Click vào widget Flutter chập chờn**: nhiều khi phải bấm lại 2–3 lần mới ăn (VD nút +/- số lượng); renderer **đơ/giật** sau một chuỗi thao tác → **chụp màn hình time-out**, phải đợi/thử lại (biểu hiện mục 1.20.2). Trong phiên đã gặp time-out screenshot ~3 lần.
- Các thao tác *click ổn định hơn hẳn so với màn login*: chọn vai trò, lọc trạng thái, mở bàn, thêm món vào giỏ, +/- số lượng, xóa món, mở/đóng modal tùy chọn — **đều thực hiện được** (dù đôi lúc phải lặp lại).
- Số liệu Trang chủ khi vào: **Tất cả (15)**, Bàn trống (7), Đang sử dụng (7), Chờ xác nhận (0), Chờ thanh toán (0). Khu hiển thị: **khu 1**.

---

## 1.1 Sơ đồ bàn

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.1.1 | Hiển thị danh sách bàn theo khu | PASS | Hiện đủ bàn (BAN1..BAN10, BAN_QR, BAN KIEM TRA TEN DAI...) + thẻ "BÀN MANG VỀ"; "Tất cả (15)" |
| 1.1.2 | Lọc "Bàn trống" | PASS | Bật riêng → chỉ hiện bàn trống (màu teal): BAN KIEM TRA TEN DAI, BAN_QR, BAN4, BAN8, BAN10 (khu 1). Số đếm toàn cục (7) |
| 1.1.3 | Lọc "Đang sử dụng" | PASS | Bật → chỉ hiện bàn đang dùng (vàng): BAN1, BAN2, BAN3, BAN5, BAN6, BAN7, BAN9. Số đếm (7) |
| 1.1.4 | Lọc "Chờ xác nhận" | N/A | Số đếm (0) — không có đơn để đối chiếu |
| 1.1.5a | Lọc "Chờ thanh toán" | N/A | Số đếm (0) |
| 1.1.5b | Lọc theo khu (khu 1 / khu 2) | PASS (một phần) | Dropdown "khu 1" hiển thị trên thanh công cụ; chưa đổi sang khu 2 trong phiên (mở dropdown chập chờn) |
| 1.1.6 | Đổi số cột hiển thị | PASS (một phần) | Dropdown "5 cột" hiển thị; chưa đổi được giá trị (dropdown khó mở bằng click tự động) |
| 1.1.7 | Đổi giao diện (1/2/3) | PASS (một phần) | Nút "Giao diện 1" hiển thị; chưa đổi được |
| 1.1.8 | Thẻ bàn hiển thị thông tin | PASS | Đủ: tên bàn, timer, icon hóa đơn + số, icon khách + số, tổng tiền, màu trạng thái. VD BAN1: 96:48, 1 HĐ, 1 khách, 540.000; BAN7: 1 HĐ, 1 khách, 1.010.000 |
| 1.1.9 | Tổng tiền trên thẻ bàn | PASS | Thẻ BAN1 = 540.000 = "Tổng tiền hàng" trong Order (chưa gồm thuế/phụ thu) |
| 1.1.14 | Số liệu các tab nhất quán | PASS | 7 (trống) + 7 (đang dùng) + 0 + 0 = **14**; "Tất cả" = **15**. Chênh +1 = thẻ "BÀN MANG VỀ" |
| 1.1.16 | Bộ lọc trạng thái cộng dồn (đa lựa chọn) | PASS | Bật đồng thời "Bàn trống" + "Đang sử dụng" → hiện **hợp (union)** cả 2 nhóm; là toggle cộng dồn, KHÔNG phải radio |
| 1.1.18 | Thẻ "Bàn mang về" tính vào "Tất cả" | PASS | "Tất cả" (15) lớn hơn tổng các tab (14) đúng 1 đơn vị |
| 1.1.10–1.1.13, 1.1.15, 1.1.17 | Các mục còn lại | KHÔNG KIỂM THỬ | Phụ thuộc dropdown/đơn chờ xác nhận hoặc thao tác mở overlay chưa ổn định |

## 1.2 Menu (Thực đơn)

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.2.1 | Hiển thị danh mục món | PASS | Đủ tab: Tất cả, Bán chạy, Món mới, Nước ngọt, Nước chế biến, Nước có cồn, Món nước, Món xào, Lẩu, test máy in, banh v1, Test in pc |
| 1.2.3 | Tìm món (F1) | **FAIL (giới hạn công cụ)** | Gõ "tra" vào ô tìm món → **không nhập được**, lưới món KHÔNG lọc. Do Flutter không nhận text từ điều khiển tự động (xem ghi chú chung). Cần kiểm thử tay |
| 1.2.4 | Ẩn/hiện hình ảnh món | PASS (một phần) | Toggle "Hiện ảnh" hiển thị (đang tắt → lưới chỉ tên + giá) |
| 1.2.5 | Đổi số cột hiển thị món | PASS (một phần) | Dropdown "4 cột" hiển thị |
| 1.2.7 | Giá món | PASS | Đúng định dạng VND: 555.000đ, 550.000đ, 500.000đ, 10.000đ, 9.000đ, 999.999đ, 30.000đ, 20.000đ |

## 1.3 Modal tùy chọn món

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.3.1 | Mở modal khi món có tùy chọn | PASS | Bấm "Trà A hỷ" → modal **"Chọn món kèm theo"** (Size, Ngọt, Đá, số lượng, nút thêm) |
| 1.3.2 | Chọn thuộc tính (Size, Ngọt, Đá) | PASS | Size **S/M/LL** (LL = **+3.000đ**), Ngọt (Đường 100/50/20%), Đá (100/50%). Chọn **LL** → nút "Thêm vào giỏ hàng" đổi **9.000đ → 12.000đ** (thuộc tính có phụ thu áp đúng) |
| 1.3.4 | Tăng/giảm số lượng trong modal | PASS (một phần) | Có nút +/- cạnh tên món + ô số lượng |
| 1.3.7 | Bấm "Đóng" (không chọn gì) | PASS | Đóng modal (Esc) → KHÔNG thêm món; đơn BAN1 giữ nguyên 2 món / 540.000 |

## 1.4 Hóa đơn / Giỏ hàng (kiểm trên BAN1)

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.4.1 | Thêm món vào hóa đơn | PASS | Bấm "tran chau" → dòng xuất hiện (10.000đ); số đếm "Tổng tiền hàng (2)" → **(3)** |
| 1.4.2 | Tăng số lượng (+) | PASS | tran chau SL 1→2; Thành tiền **10.000 → 20.000** (= đơn giá × SL). *Cần bấm lặp lại do click chập chờn* |
| 1.4.3 | Giảm số lượng (−) | PASS | tran chau SL 2→1; Thành tiền 20.000 → 10.000. Khi SL = 1, bấm "−" **không xuống 0** (chặn đúng) |
| 1.4.4 | Xóa món (thùng rác) | PASS | Bấm icon thùng rác đỏ → xóa "tran chau"; số đếm (3) → **(2)**, đơn trở về trạng thái gốc |
| 1.4.6 | Ghi chú từng món | PASS | Dòng "Cơm" hiển thị "Ghi chú: ít cay @#1" + link "Chỉnh sửa" |
| 1.4.7 | Tổng tiền (tạm tính) | PASS | 500.000 (Test điều chuyển) + 40.000 (Cơm ×2) = **540.000** = "Tổng tiền hàng" |
| 1.4.8 | Thuế theo từng món | PASS | "Thuế sản phẩm" = **2.000** = 5% × 40.000 (Cơm). Khi thêm tran chau (10.000) thuế tăng +500 = 5% → app tính thuế theo % từng món |
| 1.4.11 | Tổng tiền thanh toán | PASS | **596.000** = 540.000 (hàng) + 54.000 (phụ thu) − 0 (giảm) + 2.000 (thuế) |
| 1.4.12 | Phụ thu | PASS | Phụ thu "[ngay cuoi tuan]" = **54.000** = 10% của 540.000 |
| 1.4.20 | Nhân viên phụ trách | PASS | "Admin master" hiển thị góc phải app |
| 1.4.21 | Chọn khách qua "Chọn thành viên" | PASS (một phần) | Dropdown **"Chọn thành viên"** hiển thị (đúng nhãn thực tế, không phải "Khách lẻ"); chưa mở danh sách |
| 1.4.24 | Tổng tiền cập nhật bất đồng bộ | **FAIL (xác nhận lỗi)** | "Thành tiền" của dòng đổi **ngay**, nhưng "Tổng tiền hàng / Phụ thu / Thuế / Tổng thanh toán" **trễ vài giây / luôn chậm 1 nhịp** so với dòng. Tái hiện nhiều lần (thêm món, +/-). Xem 1.20.1 |
| 1.4.5, 1.4.13, 1.4.15–1.4.19, 1.4.22, 1.4.23 | Sửa giá/giảm giá/combo/nhiều HĐ/khách hàng/modal sửa giá | KHÔNG KIỂM THỬ | Phụ thuộc nhập tay (không gõ được) hoặc mở overlay; chưa hoàn tất trong phiên |

## 1.5 In bếp / Thanh toán

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.5.1 | Báo bếp | PASS (một phần) | Nút "Báo bếp" (cam) hiển thị; món mới có nhãn "Chờ báo bếp". Không bấm gửi để tránh thao tác thật trên đơn đang mở |
| 1.5.2 | Tạm tính | PASS (một phần) | Nút "Tạm tính" (xanh lá) hiển thị |
| 1.5.3–1.5.6 | Tiền mặt / Chuyển khoản / Quẹt Thẻ / QR Tự động | PASS (một phần) | Đủ 4 nút phương thức thanh toán hiển thị trong panel; **không hoàn tất thanh toán** để không đóng đơn thật của BAN1 |
| 1.5.7 | Tiền thừa | KHÔNG KIỂM THỬ | Có ô "Tiền khách đưa"; cần nhập số (không gõ được tự động) |
| 1.5.8 | Chặn hóa đơn trống | KHÔNG KIỂM THỬ | — |

## 1.6 Xác nhận đơn (tại bàn / QR / mang về)

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.6.1–1.6.7 | Toàn bộ luồng xác nhận đơn | N/A / BLOCKED | Tab "Chờ xác nhận" = (0); cần đơn gửi từ tablet/mobile/QR (phụ thuộc thiết bị ngoài) |

## 1.7 Gửi bếp

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.7.2 | Món chưa gửi bếp | PASS | Món trong đơn hiển thị nhãn **"Chờ báo bếp"** đúng |
| 1.7.1, 1.7.3, 1.7.4 | Gửi bếp / giỏ trống / chỉ món mới | KHÔNG KIỂM THỬ | Không bấm "Báo bếp" trên đơn thật để tránh thay đổi trạng thái |

## 1.8–1.13 Chuyển/Gộp/Tách-ghép bàn, Hàng tặng, Khuyến mãi, Hủy đơn

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.8–1.13 | Các chức năng trong menu "..." của hóa đơn | KHÔNG KIỂM THỬ | Nút "..." (menu chức năng) có tồn tại trong panel hóa đơn. Các luồng chuyển/gộp/tách-ghép/hàng tặng/khuyến mãi/hủy đơn **thay đổi dữ liệu thật** và phụ thuộc mở overlay (chập chờn). Khuyến nghị kiểm thử tay |

## 1.20 Hiệu năng & ổn định (Flutter web)

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.20.1 | Tổng tiền cập nhật tức thì | **FAIL** | Tổng tiền (Tổng tiền hàng/Phụ thu/Thuế/Tổng thanh toán) cập nhật **trễ vài giây / chậm 1 nhịp** so với cột "Thành tiền" của dòng. Tái hiện ổn định khi thêm/+/- món |
| 1.20.2 | App không treo khi thao tác liên tục | **FAIL** | Renderer **đơ/giật** sau một chuỗi thao tác: chụp màn hình **time-out** (gặp ~3 lần trong phiên), phải đợi/thử lại |
| 1.20.3 | Khôi phục dữ liệu sau thao tác | PASS | Sau khi thêm/xóa "tran chau", đơn BAN1 trở về đúng trạng thái gốc (Test điều chuyển + Cơm = 540.000 / 596.000) |

---

## Tổng hợp

- **PASS (gồm "PASS một phần" có bằng chứng):** 1.1.1, 1.1.2, 1.1.3, 1.1.5b, 1.1.6, 1.1.7, 1.1.8, 1.1.9, 1.1.14, 1.1.16, 1.1.18, 1.2.1, 1.2.4, 1.2.5, 1.2.7, 1.3.1, 1.3.2, 1.3.4, 1.3.7, 1.4.1, 1.4.2, 1.4.3, 1.4.4, 1.4.6, 1.4.7, 1.4.8, 1.4.11, 1.4.12, 1.4.20, 1.4.21, 1.5.1, 1.5.2, 1.5.3–1.5.6, 1.7.2, 1.20.3  → **~36 mục PASS**
- **FAIL: 3** — **1.2.3** (ô tìm món không nhập được — giới hạn nhập liệu Flutter), **1.4.24 / 1.20.1** (tổng tiền cập nhật trễ bất đồng bộ), **1.20.2** (renderer đơ/giật, screenshot time-out)
- **N/A: 4** — 1.1.4, 1.1.5a (tab = 0), 1.6.x (không có đơn chờ xác nhận)
- **BLOCKED:** 1.6.2–1.6.7 (phụ thuộc tablet/mobile/QR ngoài)
- **KHÔNG KIỂM THỬ:** phần lớn 1.4 nâng cao (sửa giá/giảm giá/combo/nhiều HĐ), 1.5.7–1.5.8, 1.7.1/1.7.3/1.7.4, 1.8–1.13 (chuyển/gộp/tách-ghép/hàng tặng/khuyến mãi/hủy đơn) — do (1) không nhập được chữ, (2) tránh thao tác phá dữ liệu thật, (3) overlay/menu "..." mở chập chờn

## Danh sách lỗi chính
1. **[1.2.3] Ô tìm món không nhận text qua điều khiển tự động** — gõ "tra" không lọc lưới món. *Lưu ý:* đây phần lớn là **giới hạn công cụ tự động trên Flutter web** (không khẳng định lỗi sản phẩm); cần kiểm thử tay để kết luận.
2. **[1.4.24 / 1.20.1] Tổng tiền cập nhật bất đồng bộ** — cột "Thành tiền" của dòng đổi ngay, nhưng các dòng tổng (Tổng tiền hàng / Phụ thu / Thuế / Tổng thanh toán) trễ vài giây / chậm 1 nhịp. Dễ gây hiểu nhầm số tiền khi thao tác nhanh → nên kiểm tra để đảm bảo không sai số lúc thanh toán.
3. **[1.20.2] Renderer đơ/giật** — sau chuỗi thao tác, app ngừng phản hồi, chụp màn hình time-out, phải đợi/thử lại. Nên kiểm tra hiệu năng trên thiết bị thật (một phần có thể do môi trường điều khiển tự động).

## Quan sát tích cực (đúng kỳ vọng)
- Logic tính tiền chính xác: **Tổng thanh toán = Tổng tiền hàng + Phụ thu(10%) − Giảm giá + Thuế(theo % từng món)** = 596.000 ✓
- Thuế theo từng món đúng %; thêm/xóa món, +/- số lượng cập nhật Thành tiền dòng đúng ngay.
- Bộ lọc trạng thái cộng dồn (union) hoạt động đúng; số đếm tab khớp; "Bàn mang về" lệch +1 đúng quy ước.
- Modal tùy chọn món áp phụ thu thuộc tính đúng (LL +3.000 → 12.000).

> Khuyến nghị: các mục KHÔNG KIỂM THỬ (nhập liệu, thanh toán, chuyển/gộp/tách-ghép bàn, hàng tặng, khuyến mãi, hủy đơn) nên **kiểm thử tay trên thiết bị thật** vì điều khiển tự động không nhập được chữ và mở overlay không ổn định trên Flutter web canvas. Hai mục FAIL hiệu năng (1.20.1, 1.20.2) nên ưu tiên xác minh lại.
