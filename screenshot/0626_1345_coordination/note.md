# Ghi chú ảnh lỗi — Coordination (Điều phối ca) — 0626_1345

> Công cụ chụp màn hình của môi trường automation **không lưu được file ảnh ra đĩa** (giống các phiên History/Cashboot/Coordination trước — `save_to_disk` không có tác dụng). Dưới đây mô tả bằng văn bản + số liệu đối chứng để tái hiện từng phát hiện.
> App khi test: **1.0.0+81**. Route: `#/pos-shell-route/pos-shift-route`. Thời điểm: 26/06/2026 ~13:45 (+07).

## FIND-01 — Modal "Chi tiết ca" không render trên ca nhiều giao dịch
- **Ca rỗng SCR00000099CN2:** bấm "Chi tiết ca" → modal mở OK, hiển thị: Mã ca SCR00000099CN2, Mã nhân sự 00001, Họ tên Admin master, Giới tính —, Chức vụ Quản lý, Tiền mặt đầu ca 0đ, Tổng tiền mặt cuối ca 0đ, Tiền mặt bàn giao thực tế 1đ. (Kèm quirk: mở modal làm layout co về dạng mobile 373px.)
- **Ca nhiều giao dịch SCR00000097CN2 (18 GD):** bấm "Chi tiết ca" **≥4 lần** → nút sáng (pressed) nhưng **modal KHÔNG hiện**, layout giữ nguyên desktop. Không mở được bảng Thu/Chi theo phương thức trong modal.
- **Tác động:** không kiểm được 1.6.2/1.6.3 trong modal trên ca có dữ liệu. Số liệu Thu/Chi đã xác nhận qua panel chính.
- **Tái hiện:** chọn 1 ca có nhiều giao dịch → bấm "Chi tiết ca".

## FIND-02 — Lệch nhãn "Tiền mặt trong ca" giữa hộp Đóng ca và panel
- **Panel chi tiết SCR00000100CN2:** dòng "Tổng tiền mặt trong ca" = **79.550đ** (KHÔNG gồm tiền đầu ca 10.000).
- **Hộp "THÔNG TIN ĐÓNG CA"** (khi bấm Đóng ca): dòng "Tiền mặt trong ca" = **89.550đ** (= 79.550 + 10.000 tiền đầu ca).
- Cùng cụm chữ "...tiền mặt trong ca" nhưng 2 con số khác nhau (lệch đúng = tiền mặt đầu ca). Về nghiệp vụ 89.550 = tiền thực có trong két để bàn giao → hợp lý, nhưng **nên thống nhất nhãn** để tránh nhầm với panel.

## FIND-03 — Lớp phủ ma Flutter (dropdown/modal kẹt overlay)
- **Dropdown lọc loại** (Tất cả/Phiếu bán hàng/…): sau khi chọn, overlay danh sách **không tự đóng**, đè lên bảng giao dịch; bấm ra ngoài không tắt → phải **reload trang**.
- **Mở modal "Chi tiết ca"** trên ca rỗng làm **layout co về 373px (mobile)**; nút Đóng/X bấm không ăn ngay → reload mới về desktop.
- **Mở "MỞ CA"/"Đóng ca"** đôi khi chỉ làm mờ thanh nav (backdrop) nhưng nội dung modal không vẽ → reload rồi thao tác lại thì bình thường.
- Trùng quirk checklist 1.16.6. **Khắc phục: reload trang.**

## FIND-04 — CN1 (nhãn hiển thị) vs CN2 (hậu tố mã)
- Role-picker & menu ☰ hiển thị chi nhánh **CN1**; menu Thu chi cột "Tên chi nhánh" = CN1.
- Nhưng mọi mã đều mang hậu tố **CN2**: ca SCR…CN2, bán hàng POS…CN2, phiếu thu PC…CN2.
- Nhất quán nội bộ (không mâu thuẫn giữa các màn) nhưng nhãn (CN1) ≠ hậu tố mã (CN2). Trùng phát hiện các phiên trước.

## FIND-05 — Chưa cấu hình máy in
- Bấm "In phiếu ca" trên ca đã đóng → toast **"Cảnh báo: Chưa thiết lập cấu hình máy in. Vui lòng vào Cài đặt để thiết lập máy in."**
- Lệnh in được kích hoạt đúng (1.10.3 PASS) nhưng không kiểm được nội dung phiếu (1.10.4 BLOCKED).

## LỆCH-01 — 1.3.5 không có nút "..."
- 4 thẻ tổng hợp (Bán hàng/Trả hàng/Phiếu thu/Phiếu chi) hiển thị **sẵn** breakdown phương thức (Tiền mặt/Chuyển khoản/Quẹt thẻ/QR tự động) ngay trên thẻ → không có nút "..." như checklist mô tả. Vẫn đạt mục tiêu xem chi tiết.

## Bằng chứng đối soát ĐÚNG (số liệu)
- **Đồng bộ real-time:** trước test SCR100 = 9 GD, Bán hàng 4/75.600, Phiếu thu 70.100, Tổng TM 70.100. Sau khi tạo+trả tiền mặt đơn **POS15062093CN2 (9.450đ)** → 11 GD (1 hủy), Bán hàng 5/85.050, Phiếu thu 79.550, Tổng TM 79.550; tự sinh **PC00001656CN2 (9.450đ)**. Reload giữ nguyên.
- **Chỉ tính tiền mặt (1.5.3):** SCR097 Phiếu thu = Tiền mặt 1.202.700 + Chuyển khoản 2.786.950 = 3.989.650; nhưng "Tổng tiền mặt trong ca" = **1.202.700** (CK bị loại).
- **Đối chiếu Thu chi:** PC00001656CN2 = 9.450đ / Tiền mặt / Admin master / 26/06 13:36 — khớp giữa Điều phối ca và Thu chi.
- **Đóng/mở ca:** đóng SCR100 (bàn giao 89.550, chênh 0, giờ đóng 13:40:35) → mở lại SCR00000101CN2 (đầu ca 10.000, 13:43:22). Môi trường còn đúng 1 ca hoạt động.
