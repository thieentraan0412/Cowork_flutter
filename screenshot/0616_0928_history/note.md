# Ghi chú lỗi & quan sát — Menu HISTORY (phiên 0616_0928)

> Công cụ chụp ảnh **không xuất được file PNG ra đĩa** trong phiên này (giống các phiên trước).
> Vì vậy các lỗi được mô tả bằng văn bản kèm dữ liệu đối chứng để tái hiện.

Môi trường: https://order-flutter.nasys.vn — store `thientester`, user `admin`, vai trò **Thu ngân (Cashier)**, chi nhánh **CN1**, app **1.0.0+54**, Chrome.

Bối cảnh dữ liệu:
- **Hôm nay (16/06/2026): 3 đơn** — 2 đơn Đã hủy (ban2 `PO015062035CN2` 560.000; ban2 `PO015062034CN2` 1.000.000) + 1 đơn Đã thanh toán (ban1 `PO015062033CN2` 1.100.000).
- **Hôm qua (15/06/2026): 20 đơn** (đa số Đã hủy + vài đơn Đã thanh toán).

---

## BUG-01 (NẶNG) — Bộ lọc khoảng ngày (nhiều ngày) trả về RỖNG dù có đơn trong khoảng
**Mức độ:** Cao — sai chức năng cốt lõi của trang Lịch sử.
**Mô tả:** Mọi bộ lọc thời gian dạng **khoảng nhiều ngày** đều trả về "Không tìm thấy đơn hàng nào", kể cả khi khoảng đó CHỨA những ngày có đơn. Chỉ các mốc **một ngày** (Hôm nay, Hôm qua) hoạt động đúng.
**Bằng chứng đối chứng:**
- "Hôm nay" (16/06) → **3 đơn** (đúng).
- "Hôm qua" (15/06) → **20 đơn** (đúng).
- "Tuần này" (15/06–21/06) → **0 đơn** (SAI — khoảng này chứa 15/06 = 20 đơn và 16/06 = 3 đơn ⇒ phải ≥ 23 đơn).
- "Tháng này" (01/06–30/06) → **0 đơn** (SAI — chứa toàn bộ đơn tháng 6).
**Các bước tái hiện:**
1. Vào Lịch sử (mặc định Hôm nay → thấy 3 đơn).
2. Bấm bộ lọc thời gian → chọn "Tuần này" (hoặc "Tháng này") → Áp dụng.
3. Quan sát: danh sách rỗng dù khoảng chứa hôm nay/hôm qua đang có đơn.
**Ảnh hưởng phụ:** không thể dùng khoảng ngày rộng để tra cứu lịch sử ⇒ chặn nhiều nghiệp vụ tra cứu/đối soát.

## FIND-02 — Tùy chọn trạng thái trong bộ lọc KHÔNG khớp checklist
**Trạng thái thực tế trong dropdown "Trạng thái":** `Đang xử lý`, `Hoàn thành`, `Đã hủy`, `Đã trả hàng`, `Chờ thanh toán` (+ mục mặc định "Trạng thái" = tất cả).
**Checklist mong đợi:** Đã thanh toán thành công / Chưa thanh toán / Đã hủy / Đã xử lý trả hàng / Công nợ.
**Đối chiếu:**
- "Đã thanh toán thành công" ⇒ không có; gần nhất là **"Hoàn thành"** (lọc đúng đơn đã thanh toán: Hôm nay → 1 đơn).
- "Chưa thanh toán" ⇒ gần nhất **"Chờ thanh toán"** (Hôm nay → rỗng, không có đơn loại này).
- "Đã hủy" ⇒ khớp, lọc đúng (Hôm nay → 2 đơn).
- "Đã xử lý trả hàng" ⇒ gần nhất **"Đã trả hàng"** (Hôm nay → rỗng).
- **"Công nợ" ⇒ KHÔNG tồn tại** trong dropdown ⇒ testcase 1.2.8 không thực hiện được.
**Khuyến nghị:** cập nhật checklist cho khớp UI, hoặc thống nhất nhãn trạng thái với sản phẩm.

## FIND-03 — Không có tab lọc "Đặt online" trong Lịch sử
Thanh tab chỉ có **3 tab: Tất cả / Tại bàn / Mang về**. Không có tab "Đặt online" (đây là menu riêng trên thanh điều hướng). ⇒ testcase 1.1.4 không thực hiện được theo mô tả.

## FIND-04 — Dropdown "Tất cả bàn" có mục bàn bị TRÙNG; lọc ra kết quả sai
Trong dropdown chọn bàn (tab Tại bàn), các mục **"ban 1" và "ban 2" xuất hiện 2 lần** (kèm "ban kiem tra ten dai" bị mờ/disable).
**Hệ quả:** Chọn **"ban 1"** (mục đầu) → danh sách **rỗng**, mặc dù hôm nay CÓ một đơn nhãn "ban 1" (`PO015062033CN2`). Đơn ban1 đó thuộc về mục "ban 1" còn lại (trùng tên, khác ID).
Để so sánh: chọn **"ban 2"** → đúng **2 đơn** ban2. ⇒ bộ lọc bàn có hoạt động, nhưng **trùng tên bàn gây kết quả gây hiểu nhầm/sai**. Nên rà soát dữ liệu bàn trùng tên.

## FIND-05 (UX) — Các dropdown bộ lọc (Trạng thái / Chọn bàn / Tài khoản) hoạt động chập chờn
- Thường phải **bấm 2 lần** mục mới chọn được (lần 1 chỉ "mở lại" dropdown).
- Danh sách tùy chọn **tự sắp xếp lại / làm mờ** mục đã chọn mỗi lần mở ⇒ vị trí mục thay đổi, dễ bấm nhầm.
- Đôi khi để lại **lớp phủ "ma"** che danh sách, phải bấm ra ngoài/tải lại trang.

## FIND-06 (UX) — Bộ lọc thời gian (calendar) để lại lớp phủ "ma" sau khi Áp dụng
Sau khi bấm "Áp dụng", popup lịch đôi khi không tự đóng (vẫn hiện đè lên danh sách), phải bấm "Hủy"/bấm ra ngoài/tải lại trang.

## FIND-07 (Môi trường) — Phiên đăng nhập hết hạn & kết nối trình duyệt rớt nhiều lần
Trong phiên kiểm thử tự động, kết nối trình duyệt rớt vài lần và xuất hiện thông báo **"Phiên đăng nhập đã hết hạn. Vui lòng đăng nhập lại"**, phải đăng nhập lại nhiều lần. Làm chậm tiến độ (không phải lỗi nghiệp vụ của trang Lịch sử).

---

## Quan sát hữu ích (không phải lỗi)
- **Số tiền trên thẻ đơn (Lịch sử) = "Thực thu"** (đã gồm VAT). VD ban1: thẻ hiện **1.100.000** = Thực thu trong chi tiết (Tổng tiền hàng 1.000.000 + VAT 100.000). (Khác với trang Home, nơi thẻ bàn hiện Tổng tiền hàng chưa thuế.)
- **Màu thẻ:** Đã thanh toán = **xanh lá**; Đã hủy = **đỏ**. (Checklist nhắc "chưa thanh toán = xám" — phiên này không có đơn "chưa thanh toán" để xác nhận màu xám.)
- **Tab "Tại bàn"/"Mang về" mới hiện thêm dropdown "Tất cả bàn" + "Tài khoản"** (tab "Tất cả" sau khi tải mới đôi khi cũng hiện).
- Bộ lọc thời gian có thêm mốc **"Quý này", "Năm nay"** ngoài các mốc checklist liệt kê.
- Modal chi tiết mở qua **menu "..." → "Chi tiết"** (không mở bằng cách bấm thân thẻ); tiêu đề modal là **"Chi tiết hóa đơn"**; nút đóng là **icon X** (không có nút chữ "Đóng").
- Tìm kiếm áp dụng khi **nhấn Enter**.
