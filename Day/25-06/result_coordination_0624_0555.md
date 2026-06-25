# Kết quả kiểm thử — COORDINATION (Điều phối ca)

- Menu: coordination (Điều phối ca) — route `#/pos-shell-route/pos-shift-route`
- Ngày giờ: 24/06 05:55 (UTC)
- Người/agent thực hiện: Claude (Cowork)
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Thu ngân — CN1
- Trình duyệt: Chrome (qua tiện ích điều khiển) — Browser 1
- Thư mục ảnh lỗi: `screenshot/0624_0555_coordination/`

## Ghi chú chung
- Đây là menu **ổn định và hoạt động tốt nhất** trong phiên (ít đơ, đọc số liệu rõ ràng).
- **CA HIỆN TẠI:** SCR00000099CN2 · NV Admin master · Người mở Admin master · Giờ vào ca 08:34 - 24/06/2026 · Tiền mặt đầu ca 0đ · badge **"Đang hoạt động"**. Ca hiện tại **chưa có giao dịch** (4 thẻ = 0, "Không có giao dịch").
- **Đã mở chi tiết ca đã đóng SCR00000098CN2** để kiểm thử số liệu thật.

---

## 1.1 Lịch sử ca

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.1.1 | Hiển thị danh sách các ca | PASS | Thẻ ca có: NV, Người mở, Mã ca, Giờ mở, Giờ đóng, Tiền mặt. VD SCR98 (Admin master, 1.462.986đ), SCR97 (cashier, 1.202.700đ) |
| 1.1.2 | Ca đang mở hiển thị đúng trạng thái | PASS | CA HIỆN TẠI không có giờ đóng, badge "Đang hoạt động" |
| 1.1.5 | Bấm 1 ca để xem chi tiết | PASS | Bấm thẻ SCR98 → panel phải nạp đúng chi tiết ca đó |
| 1.1.6 | Nút "In phiếu" của ca | PASS (một phần) | Ca đã đóng SCR98 hiện nút "In phiếu" + "Chi tiết ca"; chưa kích hoạt in |

## 1.2 Thông tin ca & đóng ca

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.2.1 | Header ca đúng thông tin | PASS | SCR98: "2026-06-18 16:49:04 · Nhân viên: Admin master · **Đã đóng**" |
| 1.2.2 | Hiển thị Tiền mặt đầu ca | PASS | "Tiền mặt đầu ca: 0 đ" |
| 1.2.3 / 1.2.4 | Nút "Đóng ca" / "Đóng và in phiếu" | KHÔNG KIỂM THỬ | Không đóng ca thật (tránh ảnh hưởng vận hành); ca đã đóng SCR98 đúng là KHÔNG có 2 nút này |
| 1.2.5 | Ca đã đóng không cho thao tác lại | PASS | SCR98 (đã đóng) chỉ có "In phiếu"/"Chi tiết ca", KHÔNG có nút đóng ca |

## 1.3 Thẻ tổng hợp (kiểm trên SCR98)

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.3.1 | Thẻ Bán hàng | PASS | Đơn hàng **8**, Công nợ 500.000đ, Tổng tiền **1.947.886đ** |
| 1.3.2 | Thẻ Trả hàng | PASS | TM 0 / CK 0 / Quẹt thẻ 0; Phiếu trả 0; Tổng 0đ |
| 1.3.3 | Thẻ Phiếu thu | PASS | TM **1.517.986đ** · CK **30.450đ** · Quẹt thẻ 0 · QR **9.450đ** · Phiếu thu 10 · Tổng **1.557.886đ** |
| 1.3.4 | Thẻ Phiếu chi | PASS | TM **55.000đ** · CK 0 · Quẹt thẻ 0 · Phiếu chi 4 · Tổng **55.000đ** |
| 1.3.5 | Bấm "..." xem chi tiết phương thức | N/A | UI thực tế **hiển thị sẵn chi tiết phương thức trên thẻ**, KHÔNG có nút "..." (đúng ghi chú UI) |
| 1.3.6 | Tổng phương thức khớp tổng thẻ | PASS | Phiếu thu: 1.517.986 + 30.450 + 0 + 9.450 = **1.557.886** ✓ = Tổng thẻ |

## 1.4 Giao dịch trong ca (SCR98)

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.4.1 | Hiển thị danh sách giao dịch | PASS | Đủ cột: STT · Mã voucher · Loại giao dịch · Số tiền · Thanh toán · Trạng thái. VD POS15062072CN2 · Phiếu bán hàng · 10.500đ · Tiền mặt · Đã thanh toán |
| 1.4.2 | Đếm đúng tổng số giao dịch | PASS | "Tổng cộng: **37** (15 hủy)" hiển thị ở góc phải |
| 1.4.3–1.4.10 | Lọc loại / trạng thái / tìm kiếm | KHÔNG KIỂM THỬ | Có dropdown "Tất cả", ô "Tìm mã, chú thích", checkbox "Hoàn thành"/"Đã hủy" — nhưng mở dropdown chập chờn & ô tìm không nhập được text (Flutter). Quan sát: 2 checkbox đang bật |

## 1.5 Đối soát ca (logic tính) — **kiểm chứng số thật trên SCR98**

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.5.1 | Tổng tiền mặt trong ca đúng công thức | **PASS** | TM Phiếu thu − TM Phiếu chi = **1.517.986 − 55.000 = 1.462.986** ✓ = "Tổng tiền mặt trong ca: 1.462.986 đ" |
| 1.5.2 | Tiền mặt đầu ca KHÔNG cộng vào tổng | PASS | Đầu ca = 0đ; công thức khớp mà không cộng đầu ca |
| 1.5.3 | Chỉ tính giao dịch tiền mặt | **PASS** | CK (30.450đ) và QR (9.450đ) trong Phiếu thu **KHÔNG** cộng vào "Tổng tiền mặt trong ca"; chỉ TM 1.517.986 được dùng |

## 1.9 Hộp "CA HIỆN TẠI"

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.9.1 | Hiển thị đủ thông tin ca đang mở | PASS | Mã ca SCR00000099CN2, NV, Người mở, Giờ vào ca, Tiền mặt đầu ca, badge "Đang hoạt động" |
| 1.9.3 | Badge "Đang hoạt động" | PASS | Màu xanh, thống nhất hộp & panel |
| 1.9.4 | Tiền mặt đầu ca khớp | PASS | 0đ |

## 1.11 Phân biệt ca đang mở vs đã đóng

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.11.2 | Ca đã đóng: chỉ có nút in | PASS | SCR98: "In phiếu" + "Chi tiết ca", KHÔNG có "Đóng ca" |
| 1.11.3 | Chỉ 1 ca đang mở | PASS | Chỉ SCR99 "Đang hoạt động"; SCR98/SCR97 đã đóng (có giờ đóng) |
| 1.11.4 | Ca đã đóng hiển thị giờ đóng | PASS | SCR98 giờ đóng 2026-06-23 15:39:30 |

## 1.7 / 1.8 Bộ lọc Thời gian & Nhân viên

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.7.1 | Giá trị mặc định bộ lọc thời gian | PASS | Mặc định **"17-06-2026 - 24-06-2026"** (~7 ngày gần nhất) |
| 1.8.1 | Dropdown Nhân viên | PASS (một phần) | Hiển thị "Tất cả"; chưa mở chọn NV cụ thể (overlay chập chờn) |
| 1.7.2–1.7.11, 1.8.2–1.8.6 | Các preset/lọc cụ thể | KHÔNG KIỂM THỬ | Mở dropdown lịch/NV chập chờn; chưa đổi được giá trị |

## 1.14 Mã voucher & 1.15 Định dạng tiền

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.14.1 | Tiền tố mã theo loại | PASS | Phiếu bán hàng **POS…**, Phiếu thu **PC…**, Phiếu chi **PT…**, ca **SCR…** |
| 1.14.2 | Hậu tố chi nhánh | PASS | Tất cả mã gắn **…CN2** |
| 1.15.1 | Dấu phân cách nghìn + đ | PASS | "1.947.886 đ", "1.517.986 đ", "1.462.986 đ" |
| 1.15.2 | Giá trị 0 hiển thị "0 đ" | PASS | Thẻ Trả hàng, PT00000000CN2 = "0 đ" (không null) |

## 1.16 Trạng thái rỗng & 1.19 Biên/hiệu năng

| Mục | Nội dung | Trạng thái | Ghi chú |
|-----|----------|-----------|---------|
| 1.16.2 | Ca không có giao dịch | PASS | CA HIỆN TẠI (SCR99): "Không có giao dịch", 4 thẻ = 0 |
| 1.19.2 | Đếm "Tổng cộng (n hủy)" | PASS | SCR98: "Tổng cộng 37 (15 hủy)" |
| 1.19.5 | Đếm tiền mặt kiểm chứng công thức | **PASS** | 1.517.986 − 55.000 = 1.462.986 ✓ |
| 1.17.2 | Mã ca gắn đúng chi nhánh | PASS | SCR…CN2 |

---

## Tổng hợp
- **PASS: ~30** mục (gồm các mục logic quan trọng: công thức tiền mặt ca, tổng phương thức = tổng thẻ, phân biệt ca mở/đóng, định dạng tiền, quy ước mã)
- **FAIL: 0**
- **N/A: 2** — 1.3.5 (UI không còn nút "..." — đã hiển thị sẵn phương thức), một số mục cần đóng ca thật
- **KHÔNG KIỂM THỬ:** đa số bộ lọc cần mở dropdown/nhập text (1.4.3–1.4.10, 1.7.2–1.7.11, 1.8.2–1.8.6, 1.14.3–1.14.6), 1.2.3/1.2.4 (đóng ca thật), 1.6 (modal Chi tiết ca — chưa mở), 1.10 (kích hoạt in), 1.12 (đồng bộ bán hàng — cần thanh toán thật), 1.13 (đối chiếu Thu chi), 1.18 (menu ☰)

## Quan sát tích cực (nổi bật)
- **Logic đối soát tiền mặt CHÍNH XÁC**: Tổng tiền mặt trong ca = TM(Phiếu thu) − TM(Phiếu chi); CK/QR không ảnh hưởng; đầu ca không cộng vào.
- Tổng theo phương thức khớp tổng thẻ (1.557.886 ✓).
- Phân biệt ca mở/đóng đúng (nút & badge); chỉ 1 ca đang hoạt động.
- Quy ước mã (POS/PC/PT/SCR + CN2) và định dạng tiền nhất quán.

> Đây là menu hoạt động tốt nhất; các mục KHÔNG KIỂM THỬ chủ yếu do giới hạn mở overlay/nhập text tự động, không phải lỗi sản phẩm. Khuyến nghị kiểm thử tay các bộ lọc + luồng đồng bộ bán hàng (1.12) và đối chiếu Thu chi (1.13).
