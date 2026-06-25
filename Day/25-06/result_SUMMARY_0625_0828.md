# TỔNG HỢP KẾT QUẢ KIỂM THỬ — Hệ thống Cashier (ORDERSYS)

- Ngày giờ: 25/06/2026 (+07), phiên ~08:14–08:52
- Người/agent: Claude (Cowork) — trình duyệt Chrome
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò **Cashier (Thu ngân)** — Phiên bản app **1.0.0+76 → +77** (tự cập nhật trong phiên)
- Phạm vi: thực hiện toàn bộ 8 file trong `run/` (home, history, reserve, online, coordination, cashboot, return, crm)
- Kết quả chi tiết từng menu: xem `result/result_<menu>_0625_0828.md`

## 1. Tóm tắt nhanh theo menu

| Menu | Tình trạng tổng thể | PASS | FAIL | BLOCKED | CHƯA KT |
|------|--------------------|------|------|---------|---------|
| **HOME** (Trang chủ) | ✅ Hoạt động tốt, luồng cốt lõi OK | ~46 | 1 | ~12 | còn lại |
| **HISTORY** (Lịch sử) | ✅ Hoạt động tốt | ~27 | 1 (thiếu tab Đặt online) | ~10 | lọc nâng cao |
| **CASHBOOT** (Thu chi) | ✅ Hoạt động tốt | ~28 | 1–2 (mã 0/phiếu 0đ) | 1 | sửa/xóa/công nợ |
| **COORDINATION** (Điều phối ca = Quản lý ca) | ✅ Hoạt động tốt | ~26 | 0 | 0 | nhóm 1.6+ |
| **RESERVE** (Bàn đặt) | ⚠️ Cốt lõi OK, chưa hoàn tất tạo | 5 | 0 | 0 | tạo/sửa/hủy/check-in |
| **ONLINE** (Đặt online) | ⛔ Chưa triển khai | 0 | 0 | tất cả | — |
| **RETURN** (Trả hàng) | ⛔ Chưa triển khai | 0 | 0 | tất cả | — |
| **CRM** | ✅ Hoạt động tốt | 7 | 0 | 0 | tích điểm/sửa/lịch sử |

## 2. Kiểm chứng end-to-end nổi bật (rất tốt)
Một đơn bán được theo dõi xuyên suốt 4 menu, số liệu khớp tuyệt đối:
1. **HOME**: tạo đơn bàn BAN4 (tran chau x2 + Trà A hỷ size LL) → Tổng 33.600đ → Báo bếp → Thanh toán Tiền mặt (nhận 50.000, thừa 16.400) → đơn **POS15062083CN2**.
2. **HISTORY**: đơn hiện "Đã thanh toán" 33.600đ; chi tiết khớp từng món/tùy chọn/VAT.
3. **CASHBOOT**: tự sinh phiếu thu **PC00001652CN2** (Thu, 33.600đ, Tiền mặt). Công thức quỹ đúng tuyệt đối (Tồn đầu + Thu − Chi = Số dư cuối ca).
4. **COORDINATION (ca)**: đơn + phiếu thu vào ca **SCR00000100CN2**; Tổng tiền mặt trong ca 33.600đ (đầu ca 10.000 không cộng).

→ Lõi nghiệp vụ POS (đặt món → thuế → thanh toán → đồng bộ lịch sử/quỹ/ca) **chính xác**.

## 3. Lỗi & phát hiện chính (ưu tiên xử lý)

### 🔴 Cao
1. **Tính năng ĐẶT ONLINE chưa triển khai** — trang hiện "Tính năng 'booking' đang phát triển". (Toàn bộ checklist Online BLOCKED.)
2. **Tính năng TRẢ HÀNG chưa triển khai** — trang hiện "Tính năng 'returns' đang phát triển". Kéo theo BLOCKED: History "Đã xử lý trả hàng", Cashboot phiếu trả hàng, Coordination trả hàng giảm ca.

### 🟠 Trung bình
3. **[HOME 1.20.2] Renderer Flutter bị đơ khi thao tác nhanh** — sau khi mở dropdown + click nhanh, giao diện treo, phải tải lại trang. Tải lại URL gốc phục hồi được (giữ phiên).
4. **Render trắng trang khi điều hướng** (gián đoạn) — gặp ở **History** và **Reserve**: vào lần đầu vùng nội dung trắng ~10–14s, tải lại mới hiện. Liên quan lỗi ổn định renderer.
5. **[CASHBOOT 1.19.6/1.19.1] Mã phiếu "toàn số 0" & phiếu 0đ** — tồn tại `PT00000000CN2` = 0đ trong sổ quỹ (lỗi cũ còn dấu vết). (Khi thử bỏ trống Số tiền ở phiên này thì hệ thống ĐÃ chặn.)

### 🟡 Thấp / cần xác nhận
6. **[HISTORY 1.1.4] Thiếu tab "Đặt online"** — Lịch sử chỉ có Tất cả/Tại bàn/Mang về (phù hợp với việc Online chưa triển khai, nhưng lệch checklist gốc).
7. **[CRM] Hạng thành viên có nhưng Điểm = 0** — cần xác nhận quy tắc gán hạng theo điểm.
8. **[Tài liệu] run_coordination.md mô tả sai** — ghi "hàng chờ chế biến/bếp" nhưng menu "Điều phối ca" thực tế là **Quản lý ca** (mở/đóng ca). Đề xuất sửa file run cho khớp checklist & UI.

## 4. Hạng mục cố ý KHÔNG thực thi (an toàn / dùng chung)
- **Đóng ca** (Coordination): có nút "Đóng ca"/"Đóng và in phiếu" nhưng không bấm để tránh đóng ca đang chạy của môi trường test dùng chung.
- **Tạo phiếu thu/chi thật, tạo KH/đặt bàn thật**: chỉ verify form + validation, không lưu để tránh ghi dữ liệu rác (cơ chế đã được chứng minh qua phiếu auto-sinh từ đơn bán).

## 5. Hạn chế của phiên kiểm thử
- **Ảnh lỗi:** công cụ chụp màn hình không ghi được file ảnh ra đĩa trong phiên này → mỗi thư mục `screenshot/0625_0828_<menu>/` chứa `note.md` mô tả lỗi + bước tái hiện (thay cho .png/.jpg).
- **Độ phủ:** các checklist rất lớn (HOME ~140 ca, CASHBOOT/COORDINATION ~80+ ca mỗi menu). Phiên tập trung kiểm chứng **luồng cốt lõi + tính đúng số liệu** cho mỗi menu; các biến thể sâu (chuyển/gộp/tách bàn, lọc nâng cao, biên) được đánh dấu **CHƯA KT** trung thực, chưa kết luận PASS.
- App nặng (Flutter web) gây chậm/treo lẻ tẻ, ảnh hưởng tốc độ kiểm thử.

## 6. Đề xuất bước tiếp theo
1. Ưu tiên hoàn thiện & kiểm thử lại **Đặt online** và **Trả hàng** khi triển khai xong.
2. Điều tra lỗi **đơ/treo renderer** và **render trắng trang** (ổn định Flutter web) — ảnh hưởng trực tiếp thu ngân.
3. Dọn dữ liệu lỗi cũ trong sổ quỹ (`PT00000000` / phiếu 0đ) và kiểm lại chặn "Số tiền = 0".
4. Phiên sau: chạy sâu các luồng còn **CHƯA KT** (chuyển/gộp/tách bàn ở HOME; tạo→sửa→hủy→check-in ở RESERVE; sửa/xóa/công nợ ở CASHBOOT; tích điểm/lịch sử ở CRM).
