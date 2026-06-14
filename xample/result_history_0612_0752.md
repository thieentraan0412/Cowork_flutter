# Kết quả kiểm thử — Menu HISTORY (Lịch sử đơn hàng)

- Ngày giờ chạy: 12/06/2026, ~07:45–07:52 (giờ VN)
- Môi trường: https://order-flutter.nasys.vn (store `thientester`, user `admin`, vai trò **Thu ngân/Casher**), chi nhánh **CN1**
- Phiên bản ứng dụng: **1.0.0+39**
- Trình duyệt: Chrome (Windows), điều khiển qua extension (Browser 3)
- Checklist tham chiếu: `Checklist/checklist_history.md` (mục **1.1 Bộ lọc loại đơn**)
- Bối cảnh dữ liệu: "Hôm nay" có **9 đơn**, tất cả đều là đơn **Tại bàn**; không có đơn Mang về / Đặt online trong ngày.

## Bảng trạng thái — 1.1 Bộ lọc loại đơn

| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.1.1 | Lọc tab "Tất cả" | **PASS** | Tab "Tất cả" mặc định active (viền cam). Hiển thị **Tổng: 9 đơn** gồm đủ loại trạng thái: Chưa thanh toán (ban2, ban10, ban kiem tra ten dai), Đã hủy (ban7, ban1), Đã thanh toán (ban6, ban6, ban10). Không lọc theo loại — đúng kỳ vọng. |
| 1.1.2 | Lọc tab "Tại bàn" | **PASS** | Bấm tab "Tại bàn" (active cam). Vẫn **Tổng: 9 đơn**, tất cả đều là đơn tại bàn (đúng, vì toàn bộ đơn hôm nay là đơn tại bàn). Không lẫn đơn loại khác. |
| 1.1.3 | Lọc tab "Mang về" | **PASS** | Bấm tab "Mang về". Danh sách rỗng, hiện icon + dòng **"Không tìm thấy đơn hàng nào"**. Đúng kỳ vọng (hôm nay không có đơn mang về → danh sách rỗng). |
| 1.1.4 | Lọc tab "Đặt online" | **FAIL / N-A** | **Không tồn tại tab "Đặt online"** trên thanh lọc của trang Lịch sử. Thanh lọc chỉ có 3 tab: **Tất cả / Tại bàn / Mang về**. Đơn đặt online được quản lý ở menu riêng "Đặt online" trên thanh điều hướng trên cùng, không phải bằng tab lọc trong Lịch sử. → Testcase theo checklist không thực hiện được vì UI không có tab này. |
| 1.1.5 | Dropdown "Chọn bàn" | **PASS\*** | Dropdown trên thanh lọc tên là **"Tất cả bàn"** (không phải "Chọn bàn"). Mở ra danh sách bàn: Tất cả bàn, ban 1, ban 2, ban kiem tra ten dai, ban_qr, ban3…ban10. Chọn **ban7** → danh sách lọc còn **Tổng: 2 đơn**. Bộ lọc CÓ hoạt động (giảm từ 9 → 2). **\*Bất thường:** kết quả gồm thẻ **ban7** (POS00002472CN2, Đã hủy) **và** thẻ **"ban kiem tra ten dai"** (POS00002471CN2, Chưa thanh toán) — tức xuất hiện thêm 1 đơn thuộc bàn khác khi đang lọc ban7. Khả năng do lịch sử **gộp bàn** (ban7 từng gộp vào "ban kiem tra ten dai"); cần xác nhận với sản phẩm liệu đây là hành vi mong muốn hay rò rỉ bộ lọc. |

## Tổng hợp
- PASS: 3 (1.1.1, 1.1.2, 1.1.3)
- PASS\* (đạt nhưng có lưu ý): 1 (1.1.5)
- FAIL / N-A: 1 (1.1.4 — UI không có tab "Đặt online")
- BLOCKED: 0

## Lỗi / Phát hiện
- **FIND-01 (1.1.4):** Checklist mong đợi tab lọc "Đặt online" trong trang Lịch sử nhưng UI không có. Cần cập nhật checklist cho khớp UI thực tế (3 tab: Tất cả/Tại bàn/Mang về) hoặc xác nhận yêu cầu bổ sung tab này.
- **FIND-02 (1.1.5):** Lọc theo bàn "ban7" trả về thêm đơn POS00002471CN2 mang nhãn bàn "ban kiem tra ten dai". Nghi do quan hệ gộp bàn. Cần product xác nhận đúng/sai.
- **FIND-03 (UI nhỏ):** Trong dropdown "Tất cả bàn", các mục **"ban 1"** và **"ban 2"** bị **lặp 2 lần**. Có thể do trùng dữ liệu bàn giữa khu vực/tầng. Nên kiểm tra danh sách bàn.

## Ghi chú
- `save_to_disk` của công cụ chụp ảnh không hoạt động trong phiên này nên không lưu được file ảnh vào `screenshot/`. Chi tiết quan sát đã mô tả bằng văn bản; xem thêm `screenshot/0612_0752_history/note.md`.
- Mục 1.2 trong `checklist_history.md` hiện đang để trống (chưa có testcase) nên không kiểm thử trong phiên này.
