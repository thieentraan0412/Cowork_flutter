# Kết quả kiểm thử — Menu HOME (phiên 5)

- Ngày giờ chạy: 12/06/2026, ~21:15 (giờ VN)
- Môi trường: https://order-flutter.nasys.vn (store `thientester`, user `admin`, vai trò Thu ngân/Casher), chi nhánh **CN1**
- Phiên bản ứng dụng: **1.0.0+39**
- Trình duyệt: Chrome (Windows), điều khiển qua extension
- Checklist tham chiếu: `Checklist/checklist_home.md`
- Hướng dẫn: `run/run_home.md`

## ⛔ KẾT LUẬN PHIÊN: BLOCKED TOÀN MENU HOME

Menu **Trang chủ (Home)** **không thể sử dụng** trong phiên này: sau khi đăng nhập Thu ngân và vào Trang chủ, **toàn bộ màn hình kẹt ở trạng thái skeleton** (thanh tìm kiếm, thanh filter và lưới sơ đồ bàn đều là placeholder xám). Đã chờ > 30 giây và **reload toàn trang** nhiều lần → vẫn không render. Vì lưới bàn và thanh công cụ không hiển thị, **không thực hiện được bất kỳ mục checklist nào (1.1 → 1.15)**.

→ Đây là **lỗi nghiêm trọng (Critical / Blocker)** mới phát sinh. Các phiên trước trong ngày (`result_home_0612_1106/1334/1406.md`) chạy Home bình thường → đây là **regression**, nhiều khả năng do **dữ liệu đơn tồn đọng từ các phiên test trước** (đơn chưa thanh toán có `info_payment = null`).

## 🐞 BUG-CRIT-01 — Trang chủ kẹt skeleton do crash parse `info_payment` (Critical)

**Mức độ:** Critical / Blocker — chặn toàn bộ menu Home.

**Hiện tượng:** Vào Trang chủ → lưới sơ đồ bàn không bao giờ load, đứng yên ở skeleton; thanh filter không bấm được.

**Nguyên nhân (xác định qua Console DevTools):** Ngay khi tải Trang chủ, app sinh **> 520 lỗi** lặp lại:
```
exception from OrderDetail
TypeError: Cannot read properties of null (reading 'gal')
InfoPayment.fromJson DataDetail error: Null check operator used on a null value
InfoPayment.fromJson OrderDetail error: Null check operator used on a null value
Failed to parse InfoPayment from JSON: Null check operator used on a null value
OdrOrder.fromJson info_payment error: Exception: Failed to parse InfoPayment from JSON: Null check operator used on a null value
```
API **trả về dữ liệu order bình thường** (log in ra cả bản ghi order), nhưng **client crash khi parse trường `info_payment` bị null** → cascade lỗi `OrderDetail` (`reading 'gal'`) → lưới bàn không render. Đây là **lỗi client-side parsing**, không phải lỗi mạng/API.

**Bản ghi order liên quan trong log (ví dụ):**
- `order_id 2456` — menu_id 112 "Test Kho 7", price 500.000
- `order_id 2511` — menu_id 113 "Test Kho 8", price 500.000
- `order_id 2515` — menu_id 113 "Test Kho 8", price 500.000

**Các bước tái hiện:**
1. Đăng nhập store `thientester` / `admin` / `12345678` → chọn **Thu ngân** (CN1).
2. Vào **Trang chủ**.
3. Quan sát: lưới bàn kẹt skeleton; mở DevTools Console thấy error storm `InfoPayment.fromJson ... Null check`.
4. Reload `#/pos-shell-route` và chờ > 30s → vẫn kẹt.

**Đối chứng (cô lập lỗi):** Menu **Lịch sử** tải BÌNH THƯỜNG (Tổng 9 đơn, hiển thị đủ thẻ đơn) → app không hỏng toàn cục; lỗi **chỉ ở luồng parse order của Trang chủ**. Trong Lịch sử có các đơn **Chưa thanh toán** tồn đọng nghi là nguồn dữ liệu xấu: `ban 2 POS00002474CN2 (10.000)`, `ban10 POS00002473CN2 (10.000)`, `ban kiem tra ten dai POS00002471CN2 (20.000)`.

**Ảnh:** `screenshot/0612_2115_home/note.md` (mô tả ảnh + log; `save_to_disk` không khả dụng trong phiên).

**Đề xuất:**
- Dev: thêm null-safe khi parse `InfoPayment` / `OdrOrder.info_payment`; 1 đơn lỗi không được làm sập toàn bộ lưới bàn (cô lập lỗi từng thẻ bàn).
- Vận hành: dọn/đóng các đơn test tồn đọng (thanh toán hoặc hủy `POS...2471/2473/2474`) để khôi phục Trang chủ, sau đó chạy lại checklist Home.

## Bảng trạng thái checklist HOME

Tất cả các mục **BLOCKED** vì màn hình Home không render (xem BUG-CRIT-01).

### 1.1 Sơ đồ bàn
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.1.1 | Hiển thị danh sách bàn theo khu | BLOCKED | Lưới bàn kẹt skeleton, không render |
| 1.1.2 | Lọc tab "Bàn trống" | BLOCKED | Thanh filter là skeleton, không bấm được |
| 1.1.3 | Lọc tab "Đang sử dụng" | BLOCKED | nt |
| 1.1.4 | Lọc tab "Chờ xác nhận" | BLOCKED | nt |
| 1.1.5 | Lọc tab "Chờ thanh toán" / Lọc theo khu | BLOCKED | nt |
| 1.1.6 | Đổi số cột hiển thị | BLOCKED | Toolbar không render |
| 1.1.7 | Đổi giao diện (1/2/3) | BLOCKED | nt |
| 1.1.8 | Thẻ bàn hiển thị thông tin | BLOCKED | Không có thẻ bàn |
| 1.1.9 | Tổng tiền trên thẻ bàn | BLOCKED | nt |
| 1.1.10 | Trạng thái "Chưa báo bếp" | BLOCKED | nt |
| 1.1.11 | Nút "Xác nhận" trên thẻ | BLOCKED | nt |
| 1.1.12 | Bấm vào bàn | BLOCKED | Không vào được Order vì không có thẻ bàn |
| 1.1.13 | Thêm đơn mang về | BLOCKED | Không thấy thẻ "Bàn mang về" |
| 1.1.14 | Số liệu các tab nhất quán | BLOCKED | Không có số đếm |

### 1.2 Menu (Thực đơn)
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.2.1 – 1.2.x | Toàn bộ | BLOCKED | Không vào được màn hình Order (phải bấm vào bàn từ Home — đang kẹt) |

### 1.3 Modal tùy chọn món
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.3.1 – 1.3.8 | Toàn bộ | BLOCKED | Phụ thuộc màn hình Order |

### 1.4 Hóa đơn / Giỏ hàng
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.4.1 – 1.4.20 | Toàn bộ | BLOCKED | Phụ thuộc màn hình Order |

### 1.5 In bếp / Thanh toán
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.5.1 – 1.5.9 | Toàn bộ | BLOCKED | Phụ thuộc màn hình Order |

### 1.6 – 1.15 (Xác nhận đơn, chuyển/gộp/tách bàn, hàng tặng, khuyến mãi, hủy đơn, thanh toán, trường hợp đặc thù)
| STT | Testcase | Kết quả | Ghi chú |
|-----|----------|---------|---------|
| 1.6 – 1.15 | Toàn bộ | BLOCKED | Mọi luồng đều bắt đầu từ Trang chủ → đang kẹt |

## Tổng hợp
- **PASS:** 0
- **FAIL:** 0
- **BLOCKED:** Toàn bộ checklist HOME (1.1 → 1.15)
- **N/A:** 0
- **Lỗi chặn:** **BUG-CRIT-01** (Critical) — Trang chủ kẹt skeleton do crash parse `info_payment` null.

## Khuyến nghị tiếp theo
1. Dọn đơn test tồn đọng (`POS...2471 / 2473 / 2474`) qua Lịch sử (thanh toán hoặc hủy) hoặc nhờ dev xoá đơn dữ liệu xấu.
2. Sau khi Trang chủ render lại, chạy lại đầy đủ checklist Home (tham khảo các phiên trước đã PASS phần lớn).
3. Báo dev sửa parsing null-safe cho `InfoPayment` / `OdrOrder` để 1 đơn lỗi không làm sập toàn bộ Trang chủ.
