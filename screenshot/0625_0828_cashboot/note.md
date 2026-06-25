# Phát hiện CASHBOOT (Thu chi) — 25/06/2026 08:35

> Công cụ chụp màn hình không ghi ảnh ra đĩa trong phiên này → mô tả văn bản.

## Phát hiện #1 — [1.19.6 / 1.19.1] Mã phiếu "toàn số 0" & phiếu 0đ
- Trong "Quản lý thu chi", lọc mặc định Tháng này, có dòng:
  - `PT00000000CN2` — Loại **Chi** — Số tiền **0đ** — CN1 — Admin master — Mua tôm hùm bông — Tiền mặt — 23/06/2026 10:34.
- **Vấn đề:** mã phiếu là chuỗi toàn số 0 (không phải số thứ tự hợp lệ) và phiếu có số tiền 0đ vẫn tồn tại.
- **Lưu ý:** Khi thử "Thêm phiếu" bỏ trống Số tiền ở phiên này → hệ thống ĐÃ chặn (báo đỏ "Nhập số tiền"). Cần kiểm riêng trường hợp gõ đúng số "0" để xác nhận BUG-01 đã fix hay chưa.

## Đối chiếu tốt (không lỗi)
- Đơn bán 33.600đ (Tiền mặt) ở HOME → tự sinh phiếu thu `PC00001652CN2` (Thu, 33.600đ, Tiền mặt, 25/06 08:18). Khớp số tiền & PTTT.
- Công thức quỹ đúng: 8.264.976.882 + 778.508.039 − 1.239.745 = 9.042.245.176 (Số dư cuối ca).
