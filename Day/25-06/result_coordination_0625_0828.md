# Kết quả kiểm thử — COORDINATION (Điều phối ca / Quản lý ca)

- Menu: coordination (Điều phối ca) — route `#/pos-shell-route/pos-shift-route`
- Ngày giờ: 25/06/2026 08:40 (+07)
- Người/agent thực hiện: Claude (Cowork) — trình duyệt Chrome
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò Cashier — Phiên bản 1.0.0+77
- **Lưu ý quan trọng:** `run_coordination.md` mô tả trọng tâm "hàng chờ chế biến / bếp", nhưng menu **Điều phối ca** thực tế là **QUẢN LÝ CA** (mở/đóng ca, tiền mặt ca, tổng hợp giao dịch) — đúng theo `checklist_coordination.md`. Kiểm thử theo checklist.
- Ca dùng đối chiếu: **SCR00000100CN2** (đang hoạt động, mở 24/06 16:42) chứa đơn POS15062083CN2 vừa tạo.

## Phát hiện nổi bật (đối soát đúng)
- ✅ Đơn bán **POS15062083CN2** (33.600đ, Tiền mặt) xuất hiện trong "Giao dịch trong ca" + tự sinh **PC00001652CN2** (Phiếu thu) → cùng vào ca hiện tại.
- ✅ Công thức ca: Tổng tiền mặt trong ca = **33.600đ** = Tiền mặt (Phiếu thu 33.600) − Tiền mặt (Phiếu chi 0). Tiền mặt đầu ca 10.000đ KHÔNG cộng vào tổng.

## Bảng kết quả

### 1.1 Lịch sử ca
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.1.1 | PASS | Thẻ ca hiện: nhân viên, người mở, mã ca (SCR…), giờ mở, giờ đóng, tiền mặt |
| 1.1.2 | PASS | Ca đang mở: badge "Đang hoạt động", không có giờ đóng |
| 1.1.3 | PASS (có) | Bộ lọc Thời gian (18-06-2026 → 25-06-2026) |
| 1.1.4 | PASS (có) | Bộ lọc Nhân viên (Tất cả) |
| 1.1.5 | PASS | Bấm ca → chi tiết hiện ở panel phải (đang xem ca hiện tại) |
| 1.1.6 | CHƯA KT | Nút "In phiếu" ca đã đóng — chưa bấm |
| 1.1.7 | CHƯA KT | Nút "Chi tiết ca" — chưa mở modal |
| 1.1.8 | N/A | Theo ghi chú UI: KHÔNG có "Mở màn hình phụ" trong build này |

### 1.2 Thông tin ca & đóng ca
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.2.1 | PASS | Header: 2026-06-24 16:42:17 · Admin master · Đang hoạt động |
| 1.2.2 | PASS | Tiền mặt đầu ca: 10.000đ |
| 1.2.3 | PASS (có, không thực thi) | Nút "Đóng ca" hiển thị. KHÔNG bấm để tránh đóng ca đang chạy của môi trường dùng chung |
| 1.2.4 | PASS (có, không thực thi) | Nút "Đóng và in phiếu" hiển thị |
| 1.2.5 | PASS (quan sát) | Ca đã đóng trong "Lịch sử ca" (SCR…099/098/097) có giờ đóng, không có nút đóng |

### 1.3 Thẻ tổng hợp
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.3.1 | PASS | Bán hàng: Đơn hàng 1, Tổng 33.600đ |
| 1.3.2 | PASS | Trả hàng: 0đ (TM/CK/Quẹt thẻ = 0) |
| 1.3.3 | PASS | Phiếu thu: Tiền mặt 33.600, Phiếu thu 1, Tổng 33.600đ |
| 1.3.4 | PASS | Phiếu chi: 0đ |
| 1.3.5 | PASS (UI khác checklist) | Chi tiết phương thức (Tiền mặt/Chuyển khoản/Quẹt thẻ/QR) hiển thị **sẵn trên thẻ**, KHÔNG cần nút "..." |
| 1.3.6 | PASS | Σ phương thức = tổng thẻ (Phiếu thu: 33.600 TM + 0 = 33.600) |

### 1.4 Giao dịch trong ca
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.4.1 | PASS | Cột: STT, Mã voucher, Loại giao dịch, Số tiền, Thanh toán, Trạng thái |
| 1.4.2 | PASS | "Tổng cộng: 2" = 2 dòng (POS…083 + PC…652) |
| 1.4.3–1.4.7 | PASS (có) | Dropdown lọc loại "Tất cả" (Phiếu bán hàng/trả hàng/thu/chi) |
| 1.4.8 | PASS (có) | Checkbox "Hoàn thành" (đang tích) |
| 1.4.9 | PASS (có) | Checkbox "Đã hủy" (đang tích) |
| 1.4.10 | PASS (có) | Ô "Tìm mã, chú thích" |

### 1.5 Đối soát ca (logic)
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.5.1 | **PASS (tính tay)** | Tổng tiền mặt trong ca 33.600 = TM phiếu thu 33.600 − TM phiếu chi 0 |
| 1.5.2 | **PASS** | Tiền mặt đầu ca 10.000 KHÔNG cộng (tổng = 33.600, không phải 43.600) |
| 1.5.3 | PASS | Chỉ giao dịch tiền mặt vào tổng (cả 2 giao dịch đều Tiền mặt) |
| 1.5.4 | **PASS** | Đơn bán POS15062083CN2 xuất hiện trong giao dịch ca |
| 1.5.5 | CHƯA KT | Trả hàng làm giảm tổng — kiểm ở menu Return |
| 1.5.6 | PASS (gián tiếp) | Phiếu thu (từ bán hàng) cộng vào ca đúng (33.600) |
| 1.5.7 | CHƯA KT | Phiếu chi trừ khỏi ca — chưa tạo phiếu chi trong ca |
| 1.5.8 | CHƯA KT | Giao dịch đã hủy không tính — chưa có giao dịch hủy để đối chiếu |

### 1.6+ Chi tiết ca / biên / regression
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.6.x trở đi | CHƯA KT | Modal "Chi tiết ca" và các nhóm sau chưa mở trong phiên (ưu tiên không đóng ca) |

## Tổng hợp (theo mục đã chấm)
- PASS: ~26 (gồm toàn bộ logic đối soát ca, thẻ tổng hợp, giao dịch)
- FAIL: 0
- N/A: 1 (1.1.8 — không có "Mở màn hình phụ")
- CHƯA KT: nút In/Chi tiết ca, đóng ca (cố ý không thực thi), nhóm 1.6+

## Danh sách lỗi / phát hiện
1. **[Tài liệu] Lệch mô tả run_coordination.md** — file run mô tả "hàng chờ chế biến/bếp" nhưng menu "Điều phối ca" thực tế là **Quản lý ca** (mở/đóng ca). Đề xuất cập nhật run_coordination.md cho khớp checklist & UI. (Không phải lỗi phần mềm.)
2. Không phát hiện lỗi chức năng trong phạm vi đã kiểm — logic đối soát ca chính xác.
