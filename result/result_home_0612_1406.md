# Kết quả kiểm thử — Menu HOME (phiên 4 — "chạy toàn bộ" phần còn lại)

- Ngày giờ chạy: 12/06/2026, ~13:35–14:06 (giờ VN)
- Môi trường: https://order-flutter.nasys.vn (store `thientester`, user `admin`, vai trò Thu ngân/Casher), chi nhánh CN1
- Phiên bản ứng dụng: **1.0.0+39**
- Trình duyệt: Chrome (Windows), điều khiển qua extension
- Checklist tham chiếu: `Checklist/checklist_home.md`
- Đây là phiên bổ sung sau `result_home_0612_1334.md`, chạy nốt các mục còn "CHƯA CHẠY": **1.5.9, 1.6, 1.9 (thực thi), 1.10, 1.11, 1.12.5, 1.13**. Đã dùng link QR đặt món của khách (`Link/Link.md`) để test luồng xác nhận đơn.

## Bảng trạng thái (các mục chạy mới phiên 4)

### 1.5.9 Hóa đơn điện tử
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.5.9 | Hóa đơn điện tử | PASS* | Menu "..." → "Hóa đơn điện tử" → form "Thông tin hóa đơn" (Ngày phát hành) + "Thông tin bên mua" (Cá nhân/Doanh nghiệp, Họ tên*, CCCD/CMND, SĐT, Hộ chiếu, Địa chỉ*, Email, Mã đơn vị QHNS) + nút "Áp dụng". *Form mở & render đúng; KHÔNG bấm phát hành thật (tránh tạo HĐĐT với dữ liệu giả) |

### 1.6 Xác nhận đơn (QR) — 4 PASS
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.6.1 | Tab "Chờ xác nhận" hiển thị đơn chờ | PASS | Sau khi khách đặt đơn QR (POS00002473CN2, tran chau 10.000) trên link bàn ban10, cashier hiện "Chờ xác nhận (0→1)", thẻ ban10 viền cam + nút "Xác nhận" |
| 1.6.3 | Xác nhận đơn QR | PASS | Bấm "Xác nhận" trên thẻ → modal "Chọn đơn hàng" (Mã POS00002473CN2, 10.000đ, SL 1) → "Xác nhận" → modal "Chi tiết" (tran chau ×1, Tổng 10.000) → "Xác nhận" → toast "Cập nhật thành công"; ban10 chuyển "Đang sử dụng" 10.000 |
| 1.6.5 | Từ chối đơn | PASS* | Modal "Chi tiết" có nút **"Hủy đơn"** (đỏ) bên cạnh "Xác nhận" — chức năng từ chối tồn tại (không thực thi để giữ đơn xác nhận) |
| 1.6.7 | Sau xác nhận, số đếm "Chờ xác nhận" giảm | PASS | "Chờ xác nhận" 1 → 0 ngay sau khi xác nhận |

### 1.9 Gộp bàn — thực thi (bổ sung cho phiên 3)
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.9.2 / 1.9.4 | Thực thi gộp + xác nhận hoàn tất | PASS | Gộp ban7 (Cơm 18.900 có KM) → ban kiem tra ten dai: dialog xác nhận "gộp bàn ban7 gộp vào ban kiem tra ten dai?" → Xác nhận → toast "Gộp bàn thành công!" |
| 1.9.6 | Danh sách món sau gộp | PASS* | Bàn đích (ban kiem tra) sau gộp có **2 tab hóa đơn**: HĐ gốc POS...464 (cf sua new + Test Kho 8 = 580.000) và HĐ của ban7 POS...471 (Cơm + KM). *Gộp bàn giữ mỗi đơn thành 1 tab riêng, KHÔNG trộn vào 1 bill |
| 1.9.11 | Trạng thái thẻ bàn cập nhật ngay | PASS | ban7 về trống ngay trên Trang chủ; Đang sử dụng giảm tương ứng — không cần F5 |
| — | Lưu ý thẻ bàn | — | Thẻ ban kiem tra vẫn hiện 530.000 (tổng pre-tax của bill gốc) chứ không cộng tab mới — khớp BUG-01 (thẻ chỉ hiện tổng bill chính, chưa thuế) |

### 1.10 Tách/ghép đơn (Tách bill) — PASS
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.10.1 / 1.10.3 | Mở tách bill, hiển thị đúng món nguồn | PASS | Menu "..." → "Tách bill" → modal: "Bàn nhận" (ban7), "Hóa đơn nhận" (Tạo đơn mới), bảng món (Tên/Đơn giá/SL tách/SL tối đa). Món tặng (0đ) **không** xuất hiện trong danh sách tách (đúng) |
| 1.10.12 / 1.10.18 | Tách một phần sang hóa đơn mới + Xác nhận | PASS | Đặt SL tách = 1 cho Test Kho 6 → "Tạm tính (1 món) 20.000đ" → Xác nhận → toast "Tách bill thành công"; ban7 sinh thêm tab POS...472 (Test Kho 6 21.000), tab gốc POS...471 giữ phần còn lại |

### 1.11 Hàng tặng — 5 PASS
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.11.1 | Mở chức năng hàng tặng | PASS | Menu "..." → "Hàng tặng" → vào chế độ chọn: banner "ĐANG TRONG CHẾ ĐỘ CHỌN HÀNG TẶNG (TẶNG 100%)" + nút "HỦY" |
| 1.11.2 | Chọn món tặng áp vào đơn | PASS | Chọn "Cơm" → modal options nút "Thêm vào giỏ hàng - **0 đ**" → thêm; dòng Cơm vào hóa đơn giá 0đ |
| 1.11.3 | Chọn lý do tặng | PASS | Trước khi thêm, modal "Nhập lý do hàng tặng" (dropdown: Khách hàng thân thiết...) → "Xác nhận và Tiếp tục" |
| 1.11.4 | Món tặng hiển thị trong đơn | PASS | Dòng Cơm có nhãn **"Hàng tặng kèm"**, đơn giá/thành tiền = 0đ |
| 1.11.5 | Hàng tặng không cộng vào tổng tiền | PASS | Trước/sau thêm hàng tặng: Tổng tiền hàng giữ 20.000, Tổng thanh toán giữ 18.900 — hàng tặng không cộng vào tổng |

### 1.12 Khuyến mãi — bổ sung 1.12.5
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.12.5 | Bỏ khuyến mãi đã áp | PARTIAL | Icon bút "Giảm giá" mở modal "Chọn giảm giá" (Giảm giá trực tiếp / Voucher-Coupon / Khuyến mãi: Đã áp dụng 2.000đ / Tổng giảm). **Không có nút gỡ trực tiếp** CTKM trong modal này; bấm vào dòng "Đã áp dụng" không gỡ. Việc bỏ KM nhiều khả năng thực hiện qua "..." → Khuyến mãi (bỏ tích) — chưa test trọn vẹn |

### 1.13 Hủy đơn — 3 PASS (đã tìm được vị trí chức năng)
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| — | Vị trí chức năng | — | Hủy đơn KHÔNG nằm trong menu "...". Nằm ở **nút X đỏ cạnh tên tab hóa đơn** (VD: cạnh "POS00002472CN2") |
| 1.13.1 | Hủy đơn chưa thanh toán | PASS | Bấm X tab POS...472 → modal "Hủy đơn hàng" (cảnh báo "không thể hoàn tác, tất cả sản phẩm sẽ bị hủy") → chọn lý do → Xác nhận → toast "Hủy đơn hàng thành công"; đơn biến mất |
| 1.13.2 | Chọn lý do hủy (bắt buộc) | PASS | Trường "Lý do hủy *" (có dấu *), dropdown các lý do: Khách hủy đột xuất / hủy đơn hàng này / hủy đơn hàng / Khác |
| 1.13.3 | Xác nhận hủy | PASS | Chọn "Khách hủy đột xuất" → Xác nhận → hủy thành công |

### 1.14 / 1.15 — đối chiếu
| STT | Testcase | Kết quả | Quan sát thực tế |
|-----|----------|---------|------------------|
| 1.14.2 / 1.14.3 | Thanh toán từ tab Chờ thanh toán / bàn đang dùng | PASS (gián tiếp) | Đã cover qua 1.5.3–1.5.6 (thanh toán tiền mặt/CK/thẻ/QR từ bàn đang dùng) ở phiên 3 |
| 1.15.3 | Làm tròn tiền VND | PASS (quan sát) | Mọi tổng tiền/thuế quan sát đều là số nguyên VND (900, 1.000, 16.970, 18.900...), không có số lẻ thập phân |
| 1.15.6 | Ghi chú dấu/ký tự đặc biệt | PASS | Đã PASS ở phiên 2 (qua 1.4.6) |

## Tổng hợp toàn menu HOME (cộng dồn 4 phiên)
- **Đã chạy gần như toàn bộ checklist HOME** (1.1 → 1.15). PASS đại đa số; một số mục N/A do bản 1.0.0+39 không còn (gợi ý tiền mặt 1.4.14, phân trang 1.2.6, ghi chú trong modal phía thu ngân 1.3.5) hoặc PARTIAL (1.12.5).
- Trọng tâm run_home.md đã phủ đủ: tải trang, layout bàn, **chọn/chuyển bàn (chuyển + gộp + tách)**, thêm-sửa-xóa món, tính tiền, **thanh toán cả 4 phương thức**, xác nhận đơn QR, hàng tặng, khuyến mãi, hủy đơn.
- Lỗi nổi cộm xuyên suốt: **BUG-07 (lag/nuốt click nghiêm trọng)** + BUG-08/09/10 (menu ghost, toast kẹt, lưới món load rỗng) + BUG-01/03/06 (thẻ bàn chưa gồm thuế / order load trễ / lệch múi giờ).

## Lỗi mới/tái xác nhận phiên 4
- **BUG-06 tái xác nhận (Thấp)**: modal "Chọn đơn hàng" hiển thị giờ đặt đơn QR là **06:57** trong khi khách đặt lúc **13:57** (giờ VN) — lệch ~7h (UTC). 
- **BUG-07 tái xác nhận (Cao)**: vào lại bàn đang có đơn (ban7) nhiều lần bị "Hóa đơn mới"/"Không có món", phải F5; nút "Trang chủ"/menu "..." bị nuốt click liên tục — cản trở thao tác mạnh trong phiên này.
- **Ghi nhận hành vi (cần xác minh)**: tab QR khách (`table1.klkim.com`) bị **đơ render** (screenshot CDP timeout) sau vài thao tác cuộn/click — có thể do trang khách nặng/treo.
- **Quan sát chi nhánh**: trang khách QR hiển thị "Chi nhánh: **CN LHT**" trong khi cashier đang ở **CN1** — cần xác minh mapping chi nhánh giữa link QR và cashier.

## Ảnh màn hình
- Chức năng lưu ảnh ra đĩa không khả dụng trong phiên (đã xác nhận `save_to_disk` không lưu) → thư mục `screenshot/` không có ảnh; các lỗi mô tả đủ chi tiết để tái hiện.

## Dữ liệu phát sinh do kiểm thử (cần dọn nếu muốn)
- **ban kiem tra ten dai**: sau gộp có 2 tab hóa đơn (POS...464 gốc 580.000 + POS...471 Cơm có KM) — do test gộp bàn.
- **ban10**: có đơn QR đã xác nhận (POS00002473CN2, tran chau 10.000, chưa báo bếp/chưa thanh toán) — do test xác nhận đơn QR.
- ban7 đã được giải phóng (gộp sang ban kiem tra).
- Đã hủy 1 đơn tách (POS...472) và xóa 1 món tặng trong quá trình test.
