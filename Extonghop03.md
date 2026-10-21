## 1. Đường dẫn hiện tại lồng bao nhiêu cấp?

```
D:\Nam1\HocKy1\MonHoc\CongNgheThongTin\BaiTapLon\Session02\BaoCaoCuoiKy\Chuong1\Hinh anh\anh 1.jpg
```

Đếm từ gốc ổ đĩa, không tính tên ổ và không tính file:

`Nam1` (1) → `HocKy1` (2) → `MonHoc` (3) → `CongNgheThongTin` (4) → `BaiTapLon` (5) → `Session02` (6) → `BaoCaoCuoiKy` (7) → `Chuong1` (8) → `Hinh anh` (9)

**→ Đang lồng 9 cấp thư mục.**

## 2. Vi phạm quy tắc nào?

- **Quy tắc 3 Cấp Thư mục:** tối đa 3 cấp (trụ cột → môn học/dự án → nhóm nội dung), hiện vượt tới 9 cấp, gấp 3 lần. Đường dẫn quá dài dễ gây lỗi "File Not Found" khi copy sang máy khác, khó tìm file.
- **Mô hình 4 Trụ Cột:** không có thư mục cấp 1 là `01_HocTap`, `02_Projects`, `03_Personal`, `04_Media`; thư mục gốc đặt theo năm/học kỳ tùy tiện.
- **Quy tắc đặt tên:** `Hinh anh` và `anh 1.jpg` có khoảng trắng; tên chung chung, không đồng nhất (`MonHoc`, `Session02`).

## 3. Thiết kế lại (tuân thủ 3 cấp + 4 trụ cột)

```
D:\01_HocTap\IT101\BaoCaoCuoiKy\chuong-1-anh-1.jpg
```

Nếu muốn tách riêng ảnh thì dùng cấp 3 là nhóm nội dung:

```
D:\01_HocTap\IT101\BaoCaoCuoiKy\HinhAnh\chuong-1-anh-1.jpg
```

Phân tích đường dẫn đề xuất (3 cấp, file nằm trong thư mục cấp 3):

| Cấp | Thư mục | Ý nghĩa |
|---|---|---|
| 1 | `01_HocTap` | Trụ cột: việc học |
| 2 | `IT101` | Môn học |
| 3 | `BaoCaoCuoiKy` | Nhóm nội dung (hoặc thêm `HinhAnh` nếu cần phân loại) |

> Lưu ý: nếu chọn phương án có `HinhAnh` thì thành 4 cấp, vượt quy tắc. Vì vậy **phương án chuẩn nên dùng:**
>
> **`D:\01_HocTap\IT101\BaoCaoCuoiKy\chuong-1-anh-1.jpg`**

Tên file đã đổi sang `kebab-case`, không dấu, không khoảng trắng. Thông tin "Chương 1" được giữ lại trong tên file để không mất phân loại khi bỏ các thư mục thừa.
