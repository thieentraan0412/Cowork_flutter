# Ghi chú lỗi — Menu HOME (phiên 0616_0808, app 1.0.0+52)

> Công cụ điều khiển Chrome **không xuất được ảnh PNG ra đĩa** (lệnh lưu ảnh làm **treo renderer** của ứng dụng Flutter, phải tải lại trang để khôi phục). Vì vậy lỗi được mô tả bằng văn bản kèm dữ liệu đối chứng, giống cách làm các phiên trước.

---

## BUG-01 (FAIL) — 1.8.4 "Chuyển bàn cho chọn bàn đang sử dụng" — **CHƯA FIX ở 1.0.0+52**

**Mức độ:** Trung bình · **Trạng thái:** tồn tại liên tục 0612 → 0613 → 0614 → 0615 → **0616**

**Mô tả:** Khi mở chức năng **Chuyển bàn** từ một bàn đang có đơn, hệ thống **vẫn cho chọn một bàn ĐANG SỬ DỤNG** làm bàn đích. Đúng yêu cầu (1.8.4) là chỉ được chọn **bàn trống**.

**Các bước tái hiện:**
1. Vào 1 bàn đang có đơn (ví dụ ban1 có món).
2. Bấm nút **"..."** (menu chức năng) trong hóa đơn → chọn **"Chuyển bàn"**.
3. Hộp **"Chọn bàn chuyển đến"** mở ra. Tab: Tất cả (14) / Đang sử dụng (4) / Bàn trống (10) / Chờ xác nhận (0).
4. Bấm vào thẻ **"ban3"** — bàn này **đang sử dụng** (nhãn **"1 khách"**).

**Kết quả thực tế (LỖI):** ban3 (đang dùng) **được tô chọn (highlight xanh đậm)** và nút **"Chọn" sáng lên (cho phép bấm)**.

**Kết quả mong đợi:** Bàn đang sử dụng không được chọn làm đích (bị mờ/khóa như bàn hiện tại "Bàn hiện tại"), nút "Chọn" vẫn xám.

**Đối chứng trong hộp thoại:**
- Bàn hiện tại hiển thị **xám + nhãn "Bàn hiện tại"** (đúng — không chọn được).
- Nhưng **ban3 / ban5** (đang dùng, có nhãn số khách) **vẫn chọn được** (sai).

*(Đã bấm "Đóng" để hủy thao tác, không thực hiện chuyển bàn thật nhằm tránh phá dữ liệu môi trường dùng chung.)*

---

## Quan sát / lưu ý khác

**LƯU Ý-A — Vệ sinh dữ liệu (Thấp):** Một số bàn tích lũy nhiều **hóa đơn 0đ** (BAN3 hiển thị ~23 hóa đơn, BAN5 ~43 hóa đơn). Nên rà soát và dọn các đơn rỗng tồn đọng.

**LƯU Ý-B — UX overlay (Thấp):** Các dropdown trên thanh công cụ Trang chủ (**Khu vực / Số cột / Giao diện**) đôi khi để lại **lớp phủ "ma" chặn click toàn màn hình** sau khi chọn; bấm ra ngoài không tự đóng, phải bấm vùng trống thanh công cụ hoặc tải lại trang. Cần kiểm tra cơ chế đóng overlay (modal barrier) của các dropdown này.

**LƯU Ý-C — Render trễ (môi trường tự động hóa):** Ứng dụng Flutter (CanvasKit) cập nhật hiển thị **trễ** sau thao tác (số lượng/tổng tiền/ô tìm kiếm) — giá trị đúng nhưng hiện sau một thao tác kế tiếp. Không phải lỗi nghiệp vụ, nhưng gây khó cho kiểm thử tự động và có thể gây nhầm cho người dùng cuối ở thiết bị yếu.

---

## Mục BLOCKED (thiếu dữ liệu, không phải lỗi)
- **1.6.x (Xác nhận đơn)** và **1.14.4 (thanh toán đơn tablet/mobile)**: phiên này **không có đơn ở trạng thái "Chờ xác nhận"** (số đếm = 0). Cần tạo trước 1 đơn qua **QR_BAN / tablet** rồi mới kiểm được.
