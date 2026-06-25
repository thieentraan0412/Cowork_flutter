# Kết quả kiểm thử — HISTORY (Lịch sử)

- Menu: history
- Ngày giờ: 25/06/2026 08:28 (+07)
- Người/agent thực hiện: Claude (Cowork) — trình duyệt Chrome
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Cashier
- Phạm vi: kiểm thử list + chi tiết đơn; đối chiếu đơn vừa tạo ở HOME. Đơn dùng để đối chiếu: **POS15062083CN2** (33.600đ, Tiền mặt).

## Bảng kết quả

### 1.1 Bộ lọc loại đơn
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.1.1 | PASS | Tab "Tất cả" hiện mọi đơn (Tổng: 3 đơn — cả đã/chưa TT) |
| 1.1.2 | CHƯA KT | Tab "Tại bàn" có sẵn, chưa lọc xác nhận |
| 1.1.3 | CHƯA KT | Tab "Mang về" có sẵn, chưa lọc xác nhận |
| 1.1.4 | **FAIL/khác checklist** | KHÔNG có tab "Đặt online". Chỉ có 3 tab: Tất cả / Tại bàn / Mang về |
| 1.1.5 | CHƯA KT | Có dropdown "Tất cả bàn" (chọn bàn); chưa lọc theo bàn cụ thể |
| 1.1.6 | CHƯA KT | Cần đối chiếu Quản lý bàn (admin) — ngoài phạm vi phiên |
| 1.1.7 | CHƯA KT | Chưa xác nhận tab "Tại bàn" loại đơn mang về |

### 1.2 Tìm kiếm & bộ lọc
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.2.1 | CHƯA KT | Ô tìm theo mã đơn có sẵn |
| 1.2.2 | CHƯA KT | Tìm theo SĐT — chưa test |
| 1.2.3 | CHƯA KT | Tìm không khớp — chưa test |
| 1.2.4–1.2.8 | CHƯA KT | Dropdown "Trạng thái: Tất cả" có sẵn; chưa lọc từng trạng thái |
| 1.2.9 | CHƯA KT | Dropdown "Tài khoản" có sẵn |
| 1.2.10 | PASS | Mặc định "Hôm nay" — 3 đơn đều ngày 25/06/2026 |
| 1.2.11–1.2.14 | CHƯA KT | Hôm qua/Tuần/Tháng/Tùy chọn — chưa đổi |
| 1.2.15–1.2.19 | CHƯA KT | Kết hợp lọc / biên ngày / tìm tên KH — chưa test |
| 1.2.20 | PASS | Nút "Xuất Excel" có sẵn trên thanh lọc (chưa tải file để xác nhận nội dung) |
| 1.2.21–1.2.27 | CHƯA KT | Quý này/Năm nay/chặn ngày tương lai/Hủy-Áp dụng/đủ mục trạng thái — chưa mở hộp thoại ngày |
| 1.2.26 | PASS | Bộ lọc mặc định: Tất cả / Trạng thái Tất cả / Tất cả bàn / Hôm nay |

### 1.3 Danh sách đơn
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.3.1 | PASS | Thẻ hiện: tên bàn, Khách lẻ, ngày giờ, mã POS, số tiền |
| 1.3.2 | PASS | Đã TT = thẻ xanh; Chưa TT = thẻ xám |
| 1.3.3 | PASS | HĐĐT: "Không xác định" / "Chờ ký" |
| 1.3.4 | PASS | Màu thẻ phân biệt đúng theo trạng thái |
| 1.3.5 | PASS | Số tiền thẻ (33.600) = tổng trong chi tiết |
| 1.3.6 | PASS | "Tổng: 3 đơn" khớp số thẻ |

### 1.4 Chi tiết đơn hàng
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.4.1 | PASS | "..." → "Chi tiết" mở modal "Chi tiết hóa đơn", đúng mã POS15062083CN2 |
| 1.4.2 | PASS | Ngày tạo 25/06/2026 08:14, Người tạo Admin master, Bàn ban4, Khách lẻ |
| 1.4.3 | PASS | Món: Trà A hỷ (9.000×1, +LL 3.000, Đường 20%, Đá 100%); tran chau (10.000×2) |
| 1.4.4 | PASS | Tổng tiền hàng 32.000 = 12.000 + 20.000 |
| 1.4.5 | PASS | Phụ thu 0 / Giảm giá 0 / Tích điểm 0 / VAT 1.600 |
| 1.4.6 | PASS | Tổng TT 33.600 = 32.000 + 0 − 0 − 0 + 1.600 |
| 1.4.7 | PASS | Hình thức TT: Tiền mặt (đúng lúc thanh toán) |
| 1.4.8 | PASS | Nút "Đóng" → quay về danh sách, giữ bộ lọc |
| 1.4.9 | PASS (gián tiếp) | Chi tiết mở qua "..." → "Chi tiết" như kỳ vọng |
| 1.4.10 | CHƯA KT | Menu "..." đơn chưa TT — chưa mở |
| 1.4.11 | PASS | "Số khách": 1 |
| 1.4.12 | PASS | Có mục "Ghi chú" (rỗng vì đơn không ghi chú) |
| 1.4.13 | PASS | Tiêu đề "Chi tiết hóa đơn" + badge "Đã thanh toán" |
| 1.4.14 | CHƯA KT | Menu "..." đơn đã TT: thấy mục "Chi tiết"; chưa xác nhận đủ 5 mục |
| 1.4.15–1.4.16 | BLOCKED | Cần đơn Công nợ / Đã hủy để kiểm menu — chưa tạo |
| 1.4.17 | PASS | Dòng "Tích điểm" hiển thị (0), không trừ tổng |

### 1.5 Tạo đơn từ Trang chủ & kiểm tra Lịch sử
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.5.1 | PASS | Đơn chưa TT (POS15062084CN2 ban4) xuất hiện, "Chưa thanh toán", thẻ xám |
| 1.5.2 | PASS | Đơn đã TT (POS15062083CN2) "Đã thanh toán", thẻ xanh, 33.600 |
| 1.5.3 | BLOCKED | Đơn công nợ — chưa tạo (cần TT một phần) |
| 1.5.4 | BLOCKED | Chi tiết công nợ — phụ thuộc 1.5.3 |
| 1.5.5 | PASS | Mã/bàn/tiền/PTTT/trạng thái khớp đơn vừa tạo |
| 1.5.6 | PASS | Đơn mới xuất hiện trong Lịch sử (sau điều hướng/reload) |
| 1.5.7–1.5.8 | BLOCKED | Cần đơn công nợ để kiểm lọc |

### 1.6 Luồng công nợ
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.6.1–1.6.22 | BLOCKED/CHƯA KT | Cần tạo đơn thanh toán một phần (công nợ) — chưa thực hiện trong phiên |

## Tổng hợp (theo mục đã chấm)
- PASS: ~27
- FAIL/khác checklist: 1 (1.1.4 — thiếu tab "Đặt online")
- BLOCKED: ~10 (cần đơn công nợ / đã hủy)
- CHƯA KT: phần lọc nâng cao (trạng thái, khoảng ngày, tìm kiếm)

## Danh sách lỗi / phát hiện
1. **[1.1.4] Thiếu tab "Đặt online" trong Lịch sử** — chỉ có Tất cả / Tại bàn / Mang về. (Có thể đúng theo build hiện tại; checklist gốc kỳ vọng có tab này.) Ảnh: `screenshot/0625_0828_history/note.md`.
2. **[Ổn định — liên quan HOME 1.20.2] Trang Lịch sử render trắng khi điều hướng từ màn Order.** Lần đầu vào Lịch sử từ màn Order, vùng nội dung trắng/đen hoàn toàn ~14s, phải tải lại trang mới hiện danh sách. Sau reload hoạt động bình thường. Lỗi gián đoạn (intermittent).
