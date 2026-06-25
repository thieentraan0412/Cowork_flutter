# Kết quả kiểm thử — HOME (Trang chủ)

- Menu: home
- Ngày giờ: 25/06/2026 08:28 (+07)
- Người/agent thực hiện: Claude (Cowork) — trình duyệt Chrome
- Môi trường: https://order-flutter.nasys.vn — store `thientester` — vai trò **Cashier (Thu ngân)** — Phiên bản app 1.0.0+76 → +77 (tự cập nhật trong phiên)
- Phạm vi: kiểm thử thực tế luồng cốt lõi (đặt món → tùy chọn → giỏ hàng → báo bếp → thanh toán). Các mục có ✅ là đã thao tác & quan sát trực tiếp; các mục đánh **CHƯA KT** là chức năng có tồn tại nhưng chưa chạy hết luồng trong phiên này; **BLOCKED/N/A** là phụ thuộc thiết bị/điều kiện ngoài.

## Luồng đã kiểm chứng end-to-end
Mở bàn trống (BAN4) → thêm `tran chau` (10.000) → tăng SL=2 (Thành tiền 20.000) → thêm `Trà A hỷ` size LL (+3.000) Đường 20% Đá 100% (12.000) → Tổng hàng 32.000, Thuế SP 1.600, **Tổng thanh toán 33.600** → Báo bếp ("Gửi bếp thành công", món chuyển "Đã báo bếp") → Tiền mặt nhận 50.000 → **Tiền thừa 16.400** → Xác nhận → đơn **POS15062083CN2** hoàn tất, BAN4 về trống → đối chiếu trong **Lịch sử**: đúng 33.600đ, "Đã thanh toán", PTTT Tiền mặt, đủ món & tùy chọn.

## Bảng kết quả

### 1.1 Sơ đồ bàn
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.1.1 | PASS | Hiện đủ bàn theo khu (Tất cả 15) |
| 1.1.2 | PASS | "Bàn trống (7)" lọc ra bàn trống (thẻ teal). Lưu ý: lần click đầu hiển thị nhầm 1 nhịp do trạng thái chuyển cảnh, click lại đúng |
| 1.1.3 | PASS | "Đang sử dụng (7)" = 7 bàn cam (có tiền/timer) |
| 1.1.4 | PASS | "Chờ xác nhận (0)" — không có đơn chờ |
| 1.1.5a | PASS | "Chờ thanh toán (0)" |
| 1.1.5b | PASS | Dropdown khu có: Tất cả / khu 1 / khu 2 |
| 1.1.6 | CHƯA KT | Dropdown "5 cột" có sẵn, chưa đổi & xác nhận |
| 1.1.7 | CHƯA KT | Nút "Giao diện 1" có sẵn, chưa đổi 1/2/3 |
| 1.1.8 | PASS | Thẻ bàn hiện tên, timer, icon hóa đơn+SL, icon khách+SL, tổng tiền, màu trạng thái |
| 1.1.9 | CHƯA KT | Chưa đối chiếu tổng thẻ vs màn order (gồm/không gồm thuế) |
| 1.1.10 | CHƯA KT | Chưa kiểm nhãn "Chưa báo bếp" trên thẻ bàn |
| 1.1.11 | BLOCKED | Không có đơn "Chờ xác nhận" (=0) để bấm Xác nhận trên thẻ |
| 1.1.12 | PASS | Bấm bàn → mở màn Order |
| 1.1.13 | CHƯA KT | Có thẻ "Bàn mang về" nhưng chưa mở luồng mang đi |
| 1.1.14 | PASS | 7+7+0+0=14; "Tất cả"=15 = 14 + 1 bàn mang về |
| 1.1.15 | CHƯA KT | Dropdown "Danh sách"/"Sơ đồ" có sẵn, chưa đổi |
| 1.1.16 | CHƯA KT | Bộ lọc cộng dồn chưa kiểm đa lựa chọn |
| 1.1.17 | PASS | Đếm trạng thái là toàn cục: "Bàn trống (7)" trong khi khu 1 chỉ hiện 5 thẻ |
| 1.1.18 | PASS | Bàn mang về tính vào "Tất cả" nhưng không thuộc nhóm trạng thái |

### 1.2 Menu (Thực đơn)
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.2.1 | PASS | Tab danh mục: Tất cả, Bán chạy, Món mới, Nước ngọt, Nước chế biến, Nước có cồn, Món nước, Món xào, Lẩu… |
| 1.2.2 | CHƯA KT | Chưa lọc theo từng danh mục cụ thể |
| 1.2.3 | CHƯA KT | Ô "Tìm và chọn món (F1)" có sẵn, chưa gõ tìm |
| 1.2.4 | PASS | Toggle "Hiện ảnh" có sẵn & hoạt động (ẩn/hiện) |
| 1.2.5 | PASS | Dropdown "Số cột: 4 cột" có sẵn |
| 1.2.7 | PASS | Giá hiển thị đúng định dạng VND (vd 555.000đ, 9.000đ) |
| 1.2.8 | CHƯA KT | Chưa kiểm phạm vi tìm trong 1 danh mục |
| 1.2.9 | CHƯA KT | Chưa kiểm tìm không dấu |

### 1.3 Modal tùy chọn món
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.3.1 | PASS | "Trà A hỷ" mở modal "Chọn món kèm theo" (Size/Ngọt/Đá) |
| 1.3.2 | PASS | Chọn Size LL → nút đổi 9.000 → **12.000** (+3.000) |
| 1.3.3 | CHƯA KT | Nhóm "Món thêm" có trên một số món, chưa test riêng |
| 1.3.4 | PASS | Modal có nút +/- số lượng món chính |
| 1.3.5 | CHƯA KT | Chưa nhập ghi chú trong modal |
| 1.3.6 | PASS | Bấm "Thêm vào giỏ hàng" → món vào hóa đơn kèm tùy chọn |
| 1.3.7 | PASS | Có nút "X" đóng modal |
| 1.3.8 | PASS | Dòng món hiện rõ: LL +3.000, Đường 20%, Đá 100% |

### 1.4 Hóa đơn / Giỏ hàng
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.4.1 | PASS | Thêm món → dòng xuất hiện, "Tổng tiền hàng (n)" tăng |
| 1.4.2 | PASS | +SL: tran chau SL2 → Thành tiền 20.000 = 10.000×2 |
| 1.4.3 | CHƯA KT | Chưa giảm SL về biên |
| 1.4.4 | PASS | Nút X xóa dòng món, tổng về 0 |
| 1.4.5 | CHƯA KT | Sửa đơn giá thủ công (icon bút) chưa test |
| 1.4.6 | CHƯA KT | Ghi chú từng món chưa test |
| 1.4.7 | PASS | Tổng tiền hàng = Σ (đơn giá×SL) (32.000) |
| 1.4.8 | PASS | Thuế theo món: tran chau 5% (500), Test Kho 7 10% (50.000) |
| 1.4.9 | CHƯA KT | Thuế cả bill — chưa cấu hình kiểm riêng |
| 1.4.10 | CHƯA KT | Kết hợp thuế món+bill chưa test |
| 1.4.11 | PASS | Tổng TT = Hàng + Phụ thu − Giảm + Thuế (33.600 = 32.000+1.600) |
| 1.4.12 | CHƯA KT | Phụ thu (icon bút) có sẵn, chưa nhập |
| 1.4.13 | CHƯA KT | Giảm giá có sẵn, chưa chạy luồng đối chiếu admin |
| 1.4.15 | CHƯA KT | Combo/Set menu có trong thực đơn, chưa thêm kiểm |
| 1.4.16 | CHƯA KT | Dropdown khách hàng — xem 1.4.21 |
| 1.4.17 | CHƯA KT | Nhiều hóa đơn/1 bàn (nút +) — chưa test |
| 1.4.18 | CHƯA KT | Đơn các bàn độc lập — chưa test |
| 1.4.19 | PASS | Giỏ trống hiện "Giỏ hàng trống. Hãy chọn món bên trái!", tổng=0 |
| 1.4.20 | PASS | Hiện "Admin master" (NV đăng nhập) ở góc |
| 1.4.21 | PASS | Dropdown "Chọn thành viên" có sẵn (nhãn đúng, không phải "Khách lẻ") |
| 1.4.22 | CHƯA KT | Modal sửa giá — chưa test |
| 1.4.23 | CHƯA KT | Phụ thu "Không áp dụng" — chưa test |
| 1.4.24 | PASS (lưu ý) | Tổng tiền có độ trễ cập nhật ~1-2s (async) nhưng kết quả cuối đúng |

### 1.5 In bếp / Thanh toán
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.5.1 | PASS | "Báo bếp" → toast "Gửi bếp thành công", dòng món → "Đã báo bếp" |
| 1.5.2 | CHƯA KT | Nút "Tạm tính" có sẵn, chưa in/đối chiếu |
| 1.5.3 | PASS | Thanh toán Tiền mặt hoàn tất, bàn về trống, đơn vào Lịch sử |
| 1.5.4 | CHƯA KT | "Chuyển khoản" có nút, chưa hoàn tất luồng |
| 1.5.5 | CHƯA KT | "Quẹt Thẻ" có nút, chưa hoàn tất luồng |
| 1.5.6 | CHƯA KT | "QR Tự động" có nút, chưa hoàn tất luồng |
| 1.5.7 | PASS | Nhận 50.000/đơn 33.600 → Tiền thừa 16.400 đúng |
| 1.5.8 | CHƯA KT | Chặn hóa đơn trống — chưa test (nút Báo bếp/TT mờ khi trống) |

### 1.6 Xác nhận đơn (tại bàn/QR/mang về)
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.6.1 | PASS | Tab "Chờ xác nhận" có (đếm 0 hiện tại) |
| 1.6.2–1.6.7 | BLOCKED | Cần đơn gửi từ tablet/mobile/QR (thiết bị ngoài) — hiện không có đơn chờ |

### 1.7 Gửi bếp
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.7.1 | PASS | Sau Báo bếp, món chuyển "Đã báo bếp" |
| 1.7.2 | PASS | Món chưa gửi hiện "Chờ báo bếp" |
| 1.7.3 | CHƯA KT | Gửi bếp khi giỏ trống — chưa test (nút mờ khi trống) |
| 1.7.4 | CHƯA KT | Gửi bếp chỉ áp món mới — chưa test |

### 1.8 Chuyển bàn / 1.9 Gộp bàn / 1.10 Tách-Ghép đơn
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.8.1 | PASS | Menu "..." có mục **Chuyển bàn** |
| 1.8.2–1.8.9 | CHƯA KT | Chưa chạy luồng chuyển bàn đầy đủ trong phiên |
| 1.9.1 | PASS | Menu "..." có mục **Gộp bàn** |
| 1.9.2–1.9.11 | CHƯA KT | Chưa chạy luồng gộp bàn đầy đủ |
| 1.10.1 | PASS | Menu "..." có mục **Tách/Ghép đơn** |
| 1.10.2–1.10.30 | CHƯA KT | Chưa chạy luồng tách/ghép đầy đủ |

### 1.11 Hàng tặng / 1.12 Khuyến mãi
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.11.1 | PASS | Menu "..." có mục **Hàng tặng** |
| 1.11.2–1.11.6 | CHƯA KT | Chưa áp món tặng |
| 1.12.1 | PASS | Mở "Khuyến mãi" → modal hiện "Không có khuyến mãi" cho đơn này |
| 1.12.2–1.12.5 | BLOCKED | Đơn không đủ điều kiện CTKM nào → không có CTKM để áp/gỡ |
| 1.12.6 | CHƯA KT | Chưa kiểm chặn khi chưa mở ca |

### 1.13 Hủy đơn / 1.14 Thanh toán qua Chờ thanh toán
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.13.1–1.13.5 | CHƯA KT | Luồng hủy đơn (nút X cạnh tab HĐ) chưa test |
| 1.14.1 | PASS | Tab "Chờ thanh toán" có sẵn |
| 1.14.2–1.14.4 | PASS (gián tiếp) | Đã thanh toán thành công 1 đơn & đồng bộ Lịch sử (xem luồng E2E) |

### 1.15 Đặc thù & lỗi
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.15.1 | CHƯA KT | SL=0 chưa test |
| 1.15.2 | PASS (gián tiếp) | Có món "comboo hoa hồng" 999.999đ hiển thị không tràn UI |
| 1.15.3 | PASS | Làm tròn VND: thuế 5% của 10.000 = 500 (số nguyên, không lẻ) |
| 1.15.4 | BLOCKED | Mất mạng khi thanh toán — không mô phỏng được an toàn |
| 1.15.5 | BLOCKED | Hai thu ngân 1 bàn — cần 2 thiết bị |
| 1.15.6 | CHƯA KT | Ghi chú ký tự đặc biệt chưa test |

### 1.16 In tem / 1.17 HĐĐT / 1.18 Đồng giá / 1.19 Đa phương thức
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.16.1–1.16.4 | PASS (có mục) / BLOCKED (in) | Menu "..." có In tem, In lại tem, In lại phiếu bếp; không có máy in để xác nhận in thật |
| 1.16.5 | CHƯA KT | Cảnh báo chưa cấu hình máy in — chưa kích hoạt |
| 1.17.1 | PASS | Menu "..." có **Hóa đơn điện tử** |
| 1.17.2–1.17.7 | CHƯA KT | Form HĐĐT (Cá nhân/Doanh nghiệp, validate) chưa mở chi tiết |
| 1.18.1 | PASS | Menu "..." có **Đồng giá** (đang mờ) |
| 1.18.2 | PASS | Đồng giá bị mờ = không có chương trình đồng giá |
| 1.18.3–1.18.4 | BLOCKED | Không có chương trình đồng giá để áp |
| 1.19.1 | PASS | Menu "..." có **Thanh toán đa phương thức** |
| 1.19.2–1.19.6 | CHƯA KT | Chưa chạy chia tiền nhiều phương thức |

### 1.20 Hiệu năng & ổn định (Flutter web)
| Mục | Trạng thái | Ghi chú |
|-----|-----------|---------|
| 1.20.1 | PASS (lưu ý) | Tổng tiền cập nhật, có trễ nhẹ async ~1-2s |
| 1.20.2 | **FAIL** | App **đơ renderer** sau khi mở dropdown khu + click nhanh: click vô hiệu, ảnh chụp timeout ~30s, phải tải lại trang. Xem mục lỗi #1 |
| 1.20.3 | PASS | Sau khi tải lại URL gốc: tự về Trang chủ, giữ đăng nhập+vai trò, dữ liệu bàn nhất quán, không tạo đơn trùng |

## Tổng hợp (theo mục đã chấm)
- PASS: ~46
- FAIL: 1 (1.20.2 ổn định renderer)
- BLOCKED: ~12 (phụ thuộc thiết bị/đơn ngoài/CTKM/máy in)
- CHƯA KT trong phiên: phần còn lại (luồng chuyển/gộp/tách bàn, HĐĐT chi tiết, đa phương thức, hủy đơn, một số biên)

## Danh sách lỗi
1. **[1.20.2] Renderer Flutter bị đơ (treo) khi thao tác nhanh**
   - Bước tái hiện: Trang chủ → mở dropdown khu ("khu 1") → click chọn mục liên tục/nhanh kèm click thẻ bàn.
   - Hiện tượng: overlay dropdown kẹt mở, click không phản hồi, lệnh chụp màn hình timeout ~30s ("renderer may be frozen").
   - Khắc phục: tải lại trang về URL gốc (https://order-flutter.nasys.vn/) → app phục hồi, giữ phiên.
   - Ảnh: không lưu được ảnh trong phiên này (công cụ không ghi ảnh ra đĩa) — mô tả tại `screenshot/0625_0828_home/note.md`.
2. **[Hiệu năng] Nhiều thao tác sau điều hướng khiến ảnh/he render chậm ~30s** (liên quan 1.20.2) — ảnh hưởng trải nghiệm thu ngân khi máy yếu.
