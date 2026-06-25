# Kết quả kiểm thử — CASHBOOT (Thu chi)

- Menu: cashboot (Thu chi / Quản lý thu chi)
- Ngày giờ: 25/06/2026 08:35 (+07)
- Người/agent thực hiện: Claude (Cowork) — trình duyệt Chrome
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Cashier — Phiên bản 1.0.0+77
- Ghi chú: Menu "Thu chi" = sổ quỹ thu/chi (PC… thu, PT… chi) + tab Công nợ. KHÔNG có chức năng "mở ca/đóng ca" trên menu này (run_cashboot nhắc tới ca, nhưng giao diện chỉ có thẻ "Số dư cuối ca"). Đối tượng dùng đối chiếu: phiếu **PC00001652CN2** auto-sinh từ đơn bán 33.600đ vừa thanh toán ở HOME.

## Phát hiện nổi bật
- ✅ **Công thức quỹ đúng tuyệt đối:** Tồn đầu kỳ 8.264.976.882 + Tổng thu 778.508.039 − Tổng chi 1.239.745 = **9.042.245.176** = Số dư cuối ca.
- ✅ **Đơn bán → tự sinh phiếu thu:** đơn 33.600đ (Tiền mặt) tạo phiếu **PC00001652CN2 / Thu / 33.600đ / Tiền mặt / 25/06 08:18**.
- ⚠️ Tồn tại dòng **PT00000000CN2 = 0đ** trong danh sách → bằng chứng lỗi cũ "mã toàn số 0 / phiếu 0đ" (BUG-01, 1.19.1/1.19.6) từng xảy ra.

## Bảng kết quả

### 1.1 Bộ lọc
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.1.1 | PASS (có) | Ô "Mã phiếu" có sẵn (chưa gõ tìm cụ thể) |
| 1.1.2 | PASS (có) | Dropdown "Chi nhánh" = CN1 |
| 1.1.3–1.1.5 | PASS (có) | Thời gian: Hôm nay/Hôm qua/Tuần này/Tuần trước/Tháng này/Tháng trước + khoảng ngày |
| 1.1.6 | PASS (có) | Date range 01-06-2026 → 25-06-2026 hiển thị |
| 1.1.7 | PASS (có) | Dropdown "Người tạo" |
| 1.1.8 | PASS (có) | Dropdown "Loại thu chi" |
| 1.1.9 | PASS (có) | Dropdown "Phân loại thu chi" |
| 1.1.10 | PASS (có) | Dropdown "Loại" (Loại nguồn) |
| 1.1.11 | CHƯA KT | Kết hợp nhiều lọc — chưa chạy từng tổ hợp |

### 1.2 Tổng quan quỹ
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.2.1 | PASS | Tồn quỹ đầu kỳ: 8.264.976.882đ |
| 1.2.2 | PASS | Tổng thu: 778.508.039đ |
| 1.2.3 | PASS | Tổng chi: 1.239.745đ |
| 1.2.4 | **PASS (đã tính tay)** | Số dư cuối ca 9.042.245.176 = 8.264.976.882 + 778.508.039 − 1.239.745 ✓ |
| 1.2.5 | CHƯA KT | Đổi kỳ → thẻ cập nhật (chưa đổi) |

### 1.3 Danh sách phiếu
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.3.1 | PASS | Đủ cột: STT, Mã phiếu, Loại, Số tiền, Chi nhánh, Người nộp/nhận, Người tạo, Phân loại, PTTT, Đính kèm, Thời gian, Mô tả, Hành động |
| 1.3.2 | PASS | "Tổng 240 bản ghi", phân trang 1,2,…,12 |
| 1.3.3 | PASS (có) | Cột Hành động có icon xem (mắt) |
| 1.3.4 | CHƯA KT | Phiếu đính kèm (vd PC00001646 có đính kèm ABCDEF…) — chưa mở file |

### 1.4 Thêm phiếu
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.4.1 | PASS | Nút "Thêm" → modal "Thêm phiếu" |
| 1.4.2 | PASS | Mã phiếu auto ("Mã tăng tự động") |
| 1.4.3 | PASS (gián tiếp) | Trường * bắt buộc: Loại thu chi, Phân loại, Số tiền |
| 1.4.4 | PASS | Bỏ trống Số tiền → bấm "Tạo mới" bị chặn, báo đỏ "Nhập số tiền" |
| 1.4.5 | PASS (có) | "Loại nhân sự" + "Người nộp/Người nhận" + nút "Tạo" |
| 1.4.6 | PASS (có) | Dropdown "Phân loại thu chi" |
| 1.4.7 | PASS | PTTT mặc định "Tiền mặt" |
| 1.4.8 | CHƯA KT | Nhập số/chữ vào Số tiền — chưa gõ thử |
| 1.4.9 | PASS (có) | "Chọn tệp" đính kèm |
| 1.4.10 | CHƯA KT | Counter Mô tả (spec ghi 50 ký tự) — chưa đếm |
| 1.4.11–1.4.20 | CHƯA KT | Chưa lưu phiếu thật (tránh ghi dữ liệu rác); cơ chế thu→quỹ đã được chứng minh qua phiếu auto-sinh |

### 1.5 Ghi nhận 4 loại phiếu
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.5.1–1.5.4 | CHƯA KT | Tạo phiếu thủ công — chưa lưu (đã verify form + validation) |
| 1.5.5 | **PASS** | Đơn bán → phiếu PC00001652CN2 (Thu, Bán hàng) |
| 1.5.6 | CHƯA KT | Phiếu trả hàng — kiểm ở menu Return |
| 1.5.7–1.5.9 | PASS (có) | Lọc Loại nguồn: Bán hàng/Mua hàng/Trả hàng/Tự tạo có trong dropdown |
| 1.5.10 | **PASS** | Số tiền phiếu = 33.600 = tổng đơn gốc |
| 1.5.11 | CHƯA KT | Trả hàng — kiểm ở menu Return |
| 1.5.12 | **PASS** | PTTT phiếu = Tiền mặt = đơn gốc |
| 1.5.13–1.5.16 | CHƯA KT | Đối chiếu Σ thu/chi & đơn hủy — chưa tính tay toàn bộ |

### 1.6 Xuất Excel
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.6.1 | PASS (có) | Nút "Xuất Excel" có sẵn (chưa tải file để xác nhận) |
| 1.6.2 | CHƯA KT | Nội dung file theo bộ lọc — chưa mở file |

### 1.7 Công nợ
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.7.1 | PASS (có) | Tab "Quản lý công nợ" có sẵn |
| 1.7.2–1.7.20 | CHƯA KT | Chưa mở tab Công nợ để kiểm chi tiết (bộ lọc đối tượng, chip trạng thái, thanh toán nợ) |

### 1.8 Sửa / 1.9 Xóa phiếu
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.8.1 | PASS | Cột Hành động: phiếu thủ công có icon sửa (bút) + xóa (thùng) + xem; phiếu auto chỉ có xem (mắt) |
| 1.8.6 | PASS (quan sát) | Phiếu auto (Bán hàng) không có nút sửa — chỉ xem |
| 1.8.2–1.8.5, 1.8.7 | CHƯA KT | Chưa chạy luồng sửa |
| 1.9.1–1.9.4, 1.9.6 | CHƯA KT | Chưa chạy luồng xóa (tránh xóa dữ liệu) |
| 1.9.5 | PASS (quan sát) | Phiếu auto không có nút xóa |

### 1.10 Sắp xếp & 1.11 Mã phiếu / định dạng
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.10.1–1.10.5 | CHƯA KT | Sắp xếp cột — chưa click header |
| 1.10.3 | PASS (quan sát) | Phiếu mới nhất (PC…1652, 08:18) nằm đầu danh sách |
| 1.11.1 | PASS | Tiền tố PC… (thu) / PT… (chi) đúng |
| 1.11.5 | PASS | Số tiền có dấu phân cách + hậu tố đ (vd 33.600đ, 100.000đ) |
| 1.11.2–1.11.4, 1.11.6–1.11.7 | CHƯA KT | Tăng mã/định dạng khi gõ/số âm khi lọc — chưa test |

### 1.12–1.18 Biên / PTTT / Tồn quỹ nâng cao / Lọc / Phân quyền / Rỗng
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.13.1 | PASS | PTTT mặc định Tiền mặt |
| 1.13.2 | PASS (quan sát) | Danh sách phiếu có Tiền mặt / Chuyển khoản / QR Tự động |
| 1.12.x, 1.14.x, 1.15.x, 1.16.x, 1.17.x, 1.18.x | CHƯA KT | Các nhóm biên/nâng cao/phân quyền chưa chạy trong phiên |
| 1.17.3 | PASS (quan sát) | Người tạo phiếu = "Admin master" (tài khoản đăng nhập) |

### 1.19 Regression — lỗi đã biết
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.19.1 (BUG-01) | **CÒN DẤU VẾT** | Có dòng PT00000000CN2 = 0đ trong danh sách (phiếu 0đ đã từng tạo được). Test ô trống thì BỊ CHẶN ("Nhập số tiền"); chưa test riêng nhập "0" |
| 1.19.6 | **FAIL/dấu vết** | Vẫn còn mã "toàn số 0": PT00000000CN2 |
| 1.19.7 | PASS | Loại nguồn đúng giá trị (Bán hàng/Mua hàng/Trả hàng/Tự tạo) |
| 1.19.2–1.19.5, 1.19.8 | CHƯA KT | Cần thao tác sâu thêm |

## Tổng hợp (theo mục đã chấm)
- PASS: ~28 (gồm công thức quỹ, phiếu auto-sinh, validation, định dạng, cấu trúc)
- FAIL/dấu vết lỗi: 1–2 (mã "PT00000000" / phiếu 0đ — 1.19.6)
- CHƯA KT: phần lớn luồng sửa/xóa, công nợ chi tiết, sắp xếp, biên, phân quyền
- BLOCKED: 1.18.4 (lỗi mạng — không mô phỏng)

## Danh sách lỗi / phát hiện
1. **[1.19.6 / 1.19.1] Mã phiếu "toàn số 0" + phiếu 0đ** — dòng `PT00000000CN2` (Chi, 0đ, 23/06 10:34) tồn tại trong sổ quỹ. Mã đáng lẽ phải là số thứ tự hợp lệ; phiếu 0đ không nên tạo được. (Khi thử bỏ trống Số tiền ở phiên này thì hệ thống đã chặn — cần kiểm riêng trường hợp gõ "0".) Mô tả: `screenshot/0625_0828_cashboot/note.md`.
