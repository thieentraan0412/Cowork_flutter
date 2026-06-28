# Danh sách Link & Tài khoản

Tổng hợp các đường dẫn dùng trong quá trình kiểm thử. Mỗi link kèm **công dụng** và **khi nào dùng**.

## Tài khoản đăng nhập (test)

**Tài khoản admin (toàn quyền):**

| Thông tin | Giá trị |
|-----------|---------|
| ID store | `thientester` |
| Tài khoản | `admin` |
| Mật khẩu | `12345678` |

**Tài khoản con — quyền Thu ngân (giới hạn chi nhánh):**

| Thông tin | Giá trị |
|-----------|---------|
| ID store | `thientester` |
| Tài khoản | `cashier` |
| Mật khẩu | `123456` |

> Đây là tài khoản test — được phép thực hiện mọi thao tác.
> Dùng tài khoản **Thu ngân** để kiểm các testcase phân quyền/phạm vi chi nhánh (vd Coordination 1.17.1).

## Bảng link

| Link | Đường dẫn | Công dụng | Khi nào dùng |
|------|-----------|-----------|--------------|
| **Đặt món QR** | https://table1.klkim.com/v2/system/table | Trang admin quản lý bàn, hiển thị mã QR từng bàn (gồm cả bàn Mang về). Quét/click QR để mở trang đặt món của khách. | Tạo đơn "Chờ xác nhận" để test xác nhận/từ chối đơn (mục 1.6, 1.1.11, 1.14.4). |
| **Admin (Dashboard)** | https://table1.klkim.com/v2/dashboard | Trang quản trị tổng (quản lý đơn hàng, dữ liệu, báo cáo...). | Đối chiếu hóa đơn sau thanh toán, kiểm tra dữ liệu phía quản trị. |
| **Bếp (KDS)** | https://table1.klkim.com/v2/kitchen | Màn hình bếp — hiển thị món được báo bếp, trạng thái chế biến. | Kiểm tra món sau khi "Báo bếp", đối chiếu luồng Coordination. |
| **CTKM (Khuyến mãi)** | https://table1.klkim.com/v2/crm/promotion-program | Cấu hình chương trình khuyến mãi (tạo/sửa/đặt điều kiện, hiệu lực). | Chuẩn bị dữ liệu cho mục 1.12 (áp / bỏ / hết hiệu lực / không đủ điều kiện KM). |
| **Đồng giá** | https://table1.klkim.com/v2/crm/promotion-program | Cấu hình chương trình đồng giá (cùng trang quản lý chương trình với CTKM). | Chuẩn bị dữ liệu cho mục 1.18.3 (áp dụng đồng giá). |
| **Setting (Tham số)** | https://table1.klkim.com/v2/system/parameter/admin | Bật/tắt và cấu hình tham số hệ thống, gồm **"Thuế trên đơn bán hàng"**. | Cấu hình thuế cả bill (mục 1.4.9/1.4.10) và các thiết lập khác. |

## Lưu ý quan trọng

- **Admin và Cashier là 2 link riêng** → khi cấu hình bên admin/CRM (CTKM, Đồng giá) **không cần đăng xuất Cashier**, chỉ cần quay lại trang Cashier (tải lại trang nếu cần) để áp dụng.
- **Riêng Setting (tham số hệ thống)**: sau khi đổi setting, thu ngân **cần đăng xuất rồi đăng nhập lại** thì thay đổi mới có hiệu lực.
- **CTKM và Đồng giá dùng chung 1 URL** (trang `promotion-program`) — phân biệt bằng loại chương trình tạo bên trong.
