# Ghi chú lỗi — phiên 0626_1102 (Menu HOME)

> Công cụ chụp ảnh của trình duyệt trong phiên này KHÔNG ghi được ảnh ra đĩa,
> nên các lỗi được mô tả bằng văn bản + ID ảnh chụp nội bộ để đối chiếu.

## Lỗi #1 — [1.20.2] Renderer Flutter bị treo (đơ overlay) sau nhiều thao tác liên tiếp
- Hiện tượng A (thanh công cụ Trang chủ): sau khi click nhanh nhiều lần vào các dropdown
  "Số cột / Chế độ xem / Giao diện", các dropdown KHÔNG mở ra nữa (kể cả dropdown khu vốn mở được trước đó).
- Hiện tượng B (màn Order, modal "Hóa đơn điện tử"): sau một loạt thao tác mở/đóng modal
  (Khuyến mãi → Hàng tặng → Đồng giá → HĐĐT), nút **X đóng modal KHÔNG phản hồi**;
  bấm Escape và bấm nền mờ (backdrop) đều KHÔNG đóng được modal. Con trỏ hover vẫn sáng nút X
  (hover hoạt động) nhưng click không ăn → renderer đóng băng phần overlay.
- Cách tái hiện: thực hiện liên tục ~15–20 thao tác click vào dropdown/modal trong màn Trang chủ hoặc Order
  mà không tải lại trang.
- Khắc phục: **tải lại trang (F5) về URL gốc** → app phục hồi, giữ đăng nhập + vai trò + dữ liệu đơn.
- Ảnh nội bộ liên quan: ss_8839hdejb (modal HĐĐT kẹt không đóng), ss_2270dpxnz (dropdown khu không mở).
- Ảnh hưởng: thu ngân thao tác nhanh/nhiều có thể phải F5 giữa chừng; dễ gây gián đoạn khi đông khách.

## Lỗi #2 — [1.4.24 / 1.20.1] Tổng tiền cập nhật bất đồng bộ (trễ ~4–7s)
- Khi bấm +/- số lượng, cột "Thành tiền" của dòng đổi NGAY, nhưng "Tổng tiền hàng" / "Tổng tiền thanh toán"
  ở phần tổng bị TRỄ ~4–7 giây mới khớp (ví dụ: dòng đã 51.000đ nhưng tổng vẫn hiện 34.000đ/35.700đ
  một lúc rồi mới nhảy lên 51.000đ/53.550đ).
- Kết quả cuối ĐÚNG, nhưng độ trễ gây hiểu nhầm số tiền tại thời điểm thao tác.
- Ảnh nội bộ liên quan: ss_828807gp1 (tổng còn 34.000 khi dòng đã 51.000).
