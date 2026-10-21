## Phần 1 – CLI vs GUI và cấu trúc câu lệnh

**1. Phân tích `ls -Force C:\Windows\Logs`**

| Thành phần | Giá trị |
|---|---|
| Command | `ls` (alias của `Get-ChildItem`) |
| Option/Flag | `-Force` (hiện cả file ẩn/hệ thống) |
| Argument | `C:\Windows\Logs` (đối tượng cần xem) |

**2. Vì sao phải dùng Terminal với máy chủ Cloud?**

Máy chủ Cloud thường **không có giao diện đồ họa** (chỉ có dòng lệnh) nên không thể dùng chuột. Muốn làm việc phải kết nối từ xa bằng **SSH** rồi gõ lệnh. Ngoài ra Terminal nhẹ, nhanh và điều khiển từ xa được.

## Phần 2 – Điều hướng hệ thống file

**3.** Di chuyển bằng Relative Path:

```powershell
cd quan-ly-sinh-vien
```

**4.** Absolute Path tới `main.py`:

```
C:\Users\student\Desktop\quan-ly-sinh-vien\src\main.py
```

**5.** Xem nội dung `data\` (kể cả file ẩn) khi đang đứng trong `src\`:

```powershell
ls -Force ..\data
```

(`..` là thư mục cha, từ đó vào `data`; `-Force` để hiện cả file ẩn.)

## Phần 3 – Thao tác file và thư mục

**6.** Tạo 2 thư mục con (PowerShell tự tạo luôn thư mục cha `quan-ly-sinh-vien` còn thiếu):

```powershell
mkdir quan-ly-sinh-vien\src, quan-ly-sinh-vien\data
```

**7.** Tạo 3 file rỗng trong một dòng lệnh (`main.py`, `utils.py` thuộc `src\`; `README.md` ở thư mục gốc):

```powershell
New-Item quan-ly-sinh-vien\src\main.py, quan-ly-sinh-vien\src\utils.py, quan-ly-sinh-vien\README.md
```

**8.** Đổi tên và sao lưu:

```powershell
# Đổi tên
mv quan-ly-sv quan-ly-sinh-vien
# (hoặc: Rename-Item quan-ly-sv quan-ly-sinh-vien)

# Sao lưu toàn bộ
cp quan-ly-sinh-vien backup-quan-ly-sinh-vien -Recurse
```

`-Recurse` là cờ đệ quy, copy cả nội dung bên trong; thiếu cờ này chỉ copy được thư mục rỗng.

## Phần 4 – Xử lý lỗi Terminal

**9. Log lỗi số 2 (`cd scr`)**

- **Chẩn đoán:** lỗi **`No such file or directory`** (không tìm thấy đường dẫn). Nguyên nhân khả dĩ nhất là **gõ sai tên** (`scr` thay vì `src`).
- **Kiểm tra bằng Tab:** gõ `cd s` rồi nhấn **Tab**. PowerShell tự điền tên thật là `src`. Nếu Tab không điền gì thì thư mục không tồn tại hoặc bạn đứng sai vị trí (kiểm tra thêm bằng `pwd`, `ls`).

**10. Log lỗi số 3 (`Access is denied`)**

- **Chẩn đoán:** lỗi **`Access is denied`** (bị từ chối quyền). Trên Windows có hai nguyên nhân thường gặp: chưa mở PowerShell với quyền quản trị, hoặc chính sách chạy script (Execution Policy) đang chặn file `.ps1`.
- **Khắc phục (theo hướng Lesson 04):** chuột phải PowerShell → **Run as Administrator**, rồi chạy lại:

```powershell
.\setup.ps1
```

**11. Log lỗi số 1 (`rm old-version`)**

- **Chẩn đoán:** thư mục `old-version` **còn file/thư mục con** mà bạn chưa chỉ định `-Recurse`. PowerShell hỏi xác nhận để tránh xóa nhầm toàn bộ dữ liệu bên trong.
- **Đơn thuốc:**

```powershell
rm old-version -Recurse -Force
```

`-Recurse` xóa cả nội dung con; `-Force` bỏ qua hỏi xác nhận. **Cẩn thận:** xóa xong không khôi phục được.

**12. Log lỗi số 4 – Quy trình 3 bước đọc log lỗi**

| Bước | Câu trả lời |
|---|---|
| (a) Dòng chứa thông điệp lỗi trực tiếp nhất | Dòng **cuối cùng** (đọc từ dưới lên): `FileNotFoundError: [Errno 2] No such file or directory: 'data/input.csv'` |
| (b) Từ khóa lỗi | `FileNotFoundError` / `No such file or directory` |
| (c) Điều cần kiểm tra tiếp | Vị trí đang đứng là `...\quan-ly-sinh-vien\src`, nên đường dẫn tương đối `data/input.csv` bị hiểu thành `src\data\input.csv` (không tồn tại). Cần sửa: chạy lệnh từ thư mục gốc (`cd ..` rồi `python src\main.py`) hoặc đổi đường dẫn trong code thành `../data/input.csv`. |
