# test_order — Bộ kiểm thử hệ thống Cashier (table1.klkim.com)

Thư mục này tập hợp toàn bộ tài liệu, hướng dẫn và kết quả kiểm thử cho hệ thống cashier.

Sử dụng trình duyệt chorme
## Thông tin đăng nhập
- URL: https://order-flutter.nasys.vn/#/auth-route
- Store ID: `thientester`
- Username: `admin`
- Password: `12345678`
- Sau khi đăng nhập: chọn **Casher**.

## Danh sách menu kiểm thử
home, history, reserve, online, coordination, cashboot, return, crm

## Cấu trúc thư mục
```
test_order/
├── README.md              ← tệp này
├── begintest.md           ← yêu cầu gốc
├── Checklist/             ← checklist cơ bản cho từng menu
│   ├── checklist_home.md
│   ├── checklist_history.md
│   ├── checklist_reserve.md
│   ├── checklist_online.md
│   ├── checklist_coordination.md
│   ├── checklist_cashboot.md
│   ├── checklist_return.md
│   └── checklist_crm.md
├── run/                   ← hướng dẫn Claude thực hiện kiểm thử từng menu
│   ├── run_home.md
│   ├── run_history.md
│   ├── run_reserve.md
│   ├── run_online.md
│   ├── run_coordination.md
│   ├── run_cashboot.md
│   ├── run_return.md
│   └── run_crm.md
├── result/                ← kết quả kiểm thử: <menu>_<ngày>_<giờ>.md
│   └── result_home_0625_1733.md  (ví dụ mẫu)
└── screenshot/            ← ảnh lỗi: <ngày_giờ_tênmenu>/
```

## Quy ước
- **Checklist**: đánh số phân cấp `1.` → `1.1` → `1.1.1`.
- **Result**: đặt tên `result_<menu>_<MMDD>_<HHmm>.md` (ví dụ `result_home_0625_1733.md`).
- **Screenshot**: lưu vào `screenshot/<MMDD_HHmm_tênmenu>/`, chỉ chụp phần **bị lỗi**.
