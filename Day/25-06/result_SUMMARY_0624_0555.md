# Tổng hợp kiểm thử — Cashier POS (8 menu)

- Ngày giờ: 24/06/2026 05:55 (UTC)
- Người/agent: Claude (Cowork) — Browser 1 (Chrome qua tiện ích điều khiển)
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò **Thu ngân** — CN1 — phiên bản 1.0.0+67
- Phạm vi: chạy toàn bộ 8 tệp trong `run/` (home, history, reserve, online, coordination, cashboot, return, crm)
- Kết quả chi tiết: xem `result_<menu>_0624_0555.md`

---

## Bảng tổng quan theo menu

| Menu | Tình trạng chức năng | PASS | FAIL | Ghi chú nổi bật |
|------|----------------------|------|------|-----------------|
| **home** | Có chức năng | ~36 | 3 | Logic tính tiền đúng (596.000 = hàng+phụ thu−giảm+thuế). FAIL: ô tìm món không nhập được, tổng tiền cập nhật **trễ**, renderer **đơ** |
| **history** | Có chức năng | ~12 | 1 | Thẻ đơn/bộ lọc/đếm đúng. **FAIL: tab "Tại bàn" báo "Đã có lỗi xảy ra"** (retry vẫn lỗi) |
| **reserve** | Có chức năng (rỗng) | 1 | 0 | Lịch theo ngày + empty state đúng; 0 đặt bàn; tạo/sửa/hủy BLOCKED (nhập text bị chặn) |
| **online** | ⚠️ Đang phát triển | 0 | 0 | "Tính năng booking đang phát triển" — toàn bộ N/A |
| **coordination** | Có chức năng (tốt nhất) | ~30 | 0 | **Công thức tiền mặt ca ĐÚNG** (1.517.986 − 55.000 = 1.462.986); phân biệt ca mở/đóng đúng |
| **cashboot** | Có chức năng | ~20 | 2 | **Công thức quỹ ĐÚNG** (đầu kỳ+thu−chi = số dư). **FAIL: mã phiếu "toàn số 0" (PT00000000/PC00000000) + phiếu 0đ** |
| **return** | ⚠️ Đang phát triển | 0 | 0 | "Tính năng returns đang phát triển" — toàn bộ N/A |
| **crm** | ⚠️ Đang phát triển | 0 | 0 | "Tính năng crm đang phát triển" — toàn bộ N/A |

---

## Phát hiện chính (ưu tiên xử lý)

### Lỗi sản phẩm cần xác minh/sửa
1. **[cashboot] Mã phiếu "toàn số 0" + phiếu số tiền 0đ** — tồn tại **PT00000000CN2**, **PC00000000CN2** và các phiếu **0đ** (PT00000000, PT00000036). Lỗi sinh mã & thiếu ràng buộc "số tiền > 0" (BUG-01) **chưa fix**.
2. **[history] Tab "Tại bàn" báo lỗi** — chọn tab "Tại bàn" → "Đã có lỗi xảy ra", "Thử lại" vẫn lỗi, dù có đơn tại bàn (ban 2). "Tất cả"/"Mang về" hoạt động đúng → nghi lỗi riêng bộ lọc "Tại bàn". *(Cần xác minh lại vì app đang bất ổn.)*
3. **[home] Tổng tiền cập nhật bất đồng bộ** — "Thành tiền" dòng đổi ngay nhưng các dòng tổng (Tổng tiền hàng/Phụ thu/Thuế/Tổng thanh toán) **trễ vài giây / chậm 1 nhịp**. Rủi ro hiểu nhầm số tiền khi thao tác nhanh.

### Tính năng chưa triển khai (3 menu)
- **online (Đặt online)**, **return (Trả hàng)**, **crm** đều hiển thị "Tính năng … đang phát triển". Không có gì để kiểm thử ở các menu này.

### Quan sát tích cực (đúng kỳ vọng)
- **Toàn bộ logic tính tiền đều đúng** ở những chỗ kiểm chứng được:
  - Home: Tổng thanh toán = Tổng tiền hàng + Phụ thu − Giảm giá + Thuế (theo % từng món).
  - Coordination: Tổng tiền mặt ca = TM(Phiếu thu) − TM(Phiếu chi); CK/QR không cộng vào tiền mặt.
  - Cashboot: Số dư cuối ca = Tồn đầu kỳ + Tổng thu − Tổng chi.
- Bộ lọc, số đếm, định dạng tiền (VND, dấu chấm nghìn, hậu tố đ), quy ước mã (POS/PC/PT/SCR + CN2) **nhất quán**.
- Phân quyền sửa/xóa: phiếu **tự sinh** chỉ cho xem; phiếu **thủ công** mới cho sửa/xóa.

---

## Giới hạn của phiên kiểm thử (quan trọng)

App là **Flutter web (CanvasKit/canvas)**. Điều khiển tự động gặp 3 giới hạn lớn (đã ghi nhận chi tiết trong từng result, trùng với các phiên trước):

1. **Không nhập được text vào ô input của Flutter** — gõ phím thật / set DOM value / execCommand / dispatch event đều KHÔNG đồng bộ vào controller Flutter. ⇒ **phải nhờ người dùng đăng nhập tay**; mọi case cần nhập liệu (tìm kiếm, thêm/sửa phiếu, tạo đặt bàn, nhập số tiền, lý do…) bị **BLOCKED**.
2. **Click vào widget chập chờn** — nhiều thao tác phải bấm lại 2–3 lần; một số menu "..."/dropdown/overlay không mở được.
3. **Renderer đơ/giật** sau một chuỗi thao tác — chụp màn hình time-out, đôi khi **phải tải lại app** (đã reload 1 lần giữa phiên) + chọn lại vai trò Thu ngân.

⇒ Vì vậy nhiều case (đặc biệt các luồng **thanh toán, chuyển/gộp/tách-ghép bàn, hàng tặng, khuyến mãi, hủy đơn, thêm/sửa phiếu, tạo đặt bàn**) được ghi **KHÔNG KIỂM THỬ / BLOCKED**, **không phải vì lỗi sản phẩm** mà do giới hạn công cụ tự động + nguyên tắc tránh phá dữ liệu thật. **Khuyến nghị kiểm thử tay trên thiết bị thật** cho các luồng này.

---

## Khuyến nghị ưu tiên
1. Xử lý lỗi sinh mã phiếu "toàn số 0" và ràng buộc "số tiền > 0" (cashboot).
2. Xác minh lại lỗi tab "Tại bàn" (history) trên thiết bị thật.
3. Kiểm tra hiệu năng: tổng tiền cập nhật trễ + renderer đơ (home/order).
4. Hoàn thiện 3 tính năng đang phát triển (online, return, crm).
5. Kiểm thử tay các luồng nghiệp vụ quan trọng mà tự động không chạm tới được.
