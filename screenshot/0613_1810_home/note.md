# Ảnh/log lỗi — Menu HOME (phiên 0613_1810)

> Lưu ý: Công cụ điều khiển trình duyệt trong phiên này **không lưu được ảnh ra đĩa** (chức năng save screenshot bị vô hiệu).
> Vì vậy các mục FAIL/N-A/BLOCKED được ghi nhận bằng **mô tả văn bản + dữ liệu đối chứng** thay cho ảnh chụp.
> Mọi quan sát dưới đây đều lấy trực tiếp từ ứng dụng (https://order-flutter.nasys.vn — store `thientester`, vai trò Thu ngân, chi nhánh CN1, phiên bản 1.0.0+39).

---

## BUG-01 (FAIL) — 1.8.4 Chuyển bàn cho chọn bàn ĐANG SỬ DỤNG làm bàn đích
- **Bước tái hiện:**
  1. Vào màn hình Order của bàn đang dùng ("ban kiem tra ten dai").
  2. Mở menu `...` → **Chuyển bàn** → hộp "Chọn bàn chuyển đến".
  3. Bấm vào thẻ **"ban 2" (đang sử dụng, 2.232.141đ, 1 khách)**.
- **Kết quả thực tế:** Thẻ "ban 2" (đang dùng) **được chọn** (viền xanh đậm) và nút **"Chọn" sáng/kích hoạt** → cho phép chuyển vào bàn đang sử dụng.
- **Kỳ vọng:** Hệ thống chỉ cho chọn **bàn trống**; bàn đang dùng phải bị mờ/không cho chọn.
- **Mức độ:** Trung bình. Trùng với BUG-01 các phiên trước (12/06).
- **Đối chứng:** Hộp "Chọn bàn chuyển đến" có các tab Tất cả(14)/Đang sử dụng(8)/Bàn trống(6)/Chờ xác nhận(0); bàn hiện tại bị mờ ("Bàn hiện tại") nhưng các bàn "đang sử dụng" khác vẫn chọn được.

---

## BLOCKED — 1.6.x Xác nhận đơn QR (không tạo được đơn QR chờ xác nhận trong phiên)
- **Bước đã thực hiện:** Mở link đặt món QR (`table1.klkim.com/v2/order/qr?...&table=ab4393...` = bàn **ban10**) ở tab riêng → thêm **Comboo 10 (669.410đ)** vào giỏ → mở giỏ → bấm **"Đặt món"** → bấm **"Xác nhận"** trong hộp xác nhận.
- **Kết quả thực tế:**
  - Trang QR **bị treo renderer** (mọi lệnh screenshot timeout 30s); phải thao tác bằng DOM (find/click theo ref).
  - Sau khi bấm Đặt món → Xác nhận, **giỏ hàng không clear**, vẫn hiển thị "Đặt món - 669.410đ".
  - Phía Thu ngân (Trang chủ): **"Chờ xác nhận" vẫn = 0**, ban10 vẫn 679.410đ (không phát sinh đơn mới); badge "Đặt online" giữ nguyên = 3.
  - Menu "Đặt online" của Thu ngân hiển thị "Tính năng booking đang phát triển" (không phải nơi chứa đơn QR).
- **Ảnh hưởng các mục:** 1.6.2, 1.6.3, 1.6.4, 1.6.5, 1.6.7, 1.1.11 (nút Xác nhận trên thẻ), 1.14.4 — không kiểm trực tiếp được vì không có đơn "Chờ xác nhận" thực tế.
- **Ghi chú:** Có thể do trang QR bị treo (JS không gửi được đơn) trong phiên điều khiển trình duyệt, hơn là lỗi sản phẩm khi dùng thật. Cần kiểm lại bằng thiết bị/QR thật.

---

## Tổng các mục N/A (không tái hiện được điều kiện)
- **1.4.9 / 1.4.10 Thuế cả bill / kết hợp:** App chỉ có dòng "Thuế sản phẩm" (thuế theo từng món); không có cấu hình thuế toàn bill để kiểm.
- **1.4.14 Gợi ý nhanh tiền mặt:** Không thấy nút gợi ý mệnh giá; ô "Tiền khách đưa" tự điền = tổng.
- **1.5.4 / 1.5.5 / 1.5.6 (CK / Quẹt thẻ / QR tự động):** Nút có đủ, cùng luồng "Xác nhận thanh toán"; chưa chạy end-to-end giao dịch thật.
- **1.8.5 / 1.9.10 / 1.10.29 / 1.12.6 / 1.13.5 Chưa mở ca / không quyền:** Dùng tài khoản admin (đủ quyền, ca đang mở) → không tái hiện được trạng thái bị chặn.
- **1.12.3 / 1.12.4 CTKM hết hạn / không đủ điều kiện:** Hộp khuyến mãi chỉ liệt kê CTKM **đủ điều kiện** ("Đơn hàng đủ điều kiện...") → không thấy CTKM hết hạn/không đủ ĐK.
- **1.13.4 Hủy đơn đã thanh toán:** Đơn đã thanh toán rời bàn (thuộc menu Lịch sử) → không hủy từ Home.
- **1.15.2 Giá rất lớn (999.999.999đ):** Hộp sửa giá chỉ cho **giảm giá** (Giá mới = Giá gốc − Giảm), không nhập giá lớn hơn gốc.
- **1.15.4 Mất mạng khi thanh toán:** Không mô phỏng an toàn trong phiên điều khiển trình duyệt.
- **1.15.5 Hai thu ngân cùng 1 bàn:** Chỉ 1 phiên đăng nhập.
- **1.2.6 Phân trang:** Lưới món dùng cuộn dọc liên tục, không có UI phân trang "1/5".
- **1.14.2 Thanh toán từ Chờ thanh toán (dine-in):** Tab "Chờ thanh toán" của Home = 0 (không có đơn dine-in chờ thanh toán). (Khu Mang về có 1 đơn "Chờ thanh toán" POS00002407CN2 530.000đ.)
