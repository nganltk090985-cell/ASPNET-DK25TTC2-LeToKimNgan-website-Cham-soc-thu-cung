# BÁO CÁO TIẾN ĐỘ TUẦN 2

**Họ và tên:** Nguyễn Thị Ngân
**Mã số sinh viên:** ...
**Lớp:** ...
**Đề tài:** Website Chăm Só Thú Cưng
**Thời gian:** 29/06/2026 - 05/07/2026

---

## 1. Các Bước Chuẩn Bị

### 1.1. Chuẩn bị cho tuần 2

| STT | Nhiệm vụ | Trạng thái | Ghi chú |
|---|---|---|---|
| 1 | Đổi tên project files (.sln, .csproj) | ✅ Hoàn thành | Từ QuáchĐạiBửu → webchamsocthucung |
| 2 | Cập nhật connection string trong Web.config | ✅ Hoàn thành | Data Source: localhost\SQLEXPRESS01 |
| 3 | Xóa thông tin "Quách Đại Bửu" trong source code | ✅ Hoàn thành | index.cshtml, _LayoutUser.cshtml |
| 4 | Chạy script tạo database trên SSMS | ✅ Hoàn thành | Database: chamsocthucung |
| 5 | Kiểm tra lại kết nối SQL Server | ✅ Hoàn thành | Ứng dụng kết nối thành công |
| 6 | Tổ chức lại thư mục project | ✅ Hoàn thành | Tạo folder src, README.md |

### 1.2. Cấu trúc thư mục sau khi tổ chức lại

```
D:\tvu-Project\chamsocthucung\cngan\
├── README.md                          # Tài liệu hướng dẫn đồ án
├── scriptQDB.sql                      # Script tạo database
├── chamsocthucung.docx                # File báo cáo Word
├── Progress_Report\
│   ├── Tuan_1.md                     # Báo cáo tuần 1 ✅
│   └── Tuan_2.md                     # Báo cáo tuần 2 ⬅️
└── src\
    └── chamsocthucung\                # Project ASP.NET MVC
        ├── webchamsocthucung.sln
        ├── webchamsocthucung.csproj
        ├── Controllers/
        ├── Models/
        ├── Views/
        └── ...
```

---

## 2. Các Tài Liệu Liên Quan Đã Nghiên Cứu

### 2.1. Tài liệu nghiên cứu trong tuần

| STT | Tài liệu | Nội dung chính | Áp dụng |
|---|---|---|---|
| 1 | Tài liệu ASP.NET MVC 5 Security | Authentication, Authorization, Session | Đăng nhập Admin/User |
| 2 | Hướng dẫn phân quyền trong ASP.NET MVC | Custom Authorization Filter | AdminPhanQuyen.cs |
| 3 | Bootstrap 4 Documentation | Grid system, Components | Giao diện _LayoutUser |
| 4 | jQuery Validation | Client-side validation | Form đăng ký, đặt hàng |
| 5 | MD5 Hashing in C# | Mã hóa mật khẩu | MahoaMD5.cs |
| 6 | LINQ to SQL Tutorial | Query, Insert, Update, Delete | Các Controller |

### 2.2. Phân tích chi tiết luồng phân quyền

```
Luồng phân quyền Admin:

1. User truy cập /Admin/Index
       ↓
2. Controller kiểm tra Session["Taikhoanadmin"]
       ↓
   ├─ Session == null  → Redirect /Admin/dangnhap
   │
   └─ Session != null → Load View Index
                         ↓
                   Kiểm tra PHANQUYEN
                   cho MAADMIN đang login
                         ↓
                   Hiển thị chức năng
                   được phép truy cập
```

---

## 3. Các Khó Khăn Gặp Phải Trong Tuần

### 3.1. Khó khăn về kết nối Database

| Khó khăn | Mô tả | Giải pháp |
|---|---|---|
| Lỗi kết nối SQL Server lần 2 | `Named Pipes Provider, error 40` vẫn xuất hiện | Đổi `Data Source` từ `localhost` → `localhost\SQLEXPRESS01` |
| Database chưa tồn tại | Ứng dụng báo lỗi khi chạy | Chạy script `scriptQDB.sql` trong SSMS để tạo database |
| Lỗi TCP/IP Protocol | SQL Server không chấp nhận kết nối TCP | Mở SQL Server Configuration Manager → Protocols → bật TCP/IP |

### 3.2. Khó khăn về việc đổi tên project

| Khó khăn | Mô tả | Giải pháp |
|---|---|---|
| Visual Studio lock file | Không thể rename trực tiếp khi project đang mở | Đóng Visual Studio, rename bằng Explorer |
| File trong obj/Debug | Các file cache vẫn chứa tên cũ | Build lại project (Ctrl+Shift+B) để tạo cache mới |
| Permission denied khi xóa thư mục cũ | Thư mục `chamsocthucung` gốc bị lock | Sử dụng `cp -r` + `rm -rf` để copy rồi xóa |

### 3.3. Khó khăn về lỗi thời gian

```
Inner Exception:
Win32Exception: The system cannot find the file specified
```

Lỗi này xuất hiện vì:
- File `QuáchĐạiBửu.csproj.FileListAbsolute.txt` chứa đường dẫn tuyệt đối cũ
- Thư mục obj/Debug chưa được clean
- **Giải pháp:** Xóa thủ công thư mục `obj` và `bin` trong project, rebuild lại

---

## 4. Các Bước Tiến Hành Trong Tuần

### 4.1. Quy trình đổi tên project

```
Bước 1: Backup toàn bộ project
    └── Copy project ra thư mục backup

Bước 2: Đổi tên trong Visual Studio
    ├── Rename solution: QuáchĐạiBửu.sln → webchamsocthucung.sln
    ├── Rename project: QuáchĐạiBửu.csproj → webchamsocthucung.csproj
    └── Rename .csproj.user file

Bước 3: Cập nhật nội dung file .sln
    └── Project reference: "QuáchĐạiBửu" → "webchamsocthucung"

Bước 4: Cập nhật Web.config connection string
    └── Data Source: ADMIN-PC → localhost\SQLEXPRESS01

Bước 5: Tìm và thay thế "Quách Đại Bửu" trong source
    ├── Views/User/index.cshtml
    ├── Views/Shared/_LayoutUser.cshtml
    └── Các file khác (nếu có)

Bước 6: Clean và Rebuild project
    ├── Build → Clean Solution
    ├── Xóa thủ công folder obj/ và bin/
    └── Build → Rebuild Solution
```

### 4.2. Quy trình chạy script database

```
Bước 1: Mở SSMS
    └── Connect đến localhost\SQLEXPRESS01

Bước 2: Mở file scriptQDB.sql
    └── File nằm trong D:\tvu-Project\chamsocthucung\cngan\

Bước 3: Chạy script
    ├── Chọn database master trước
    ├── Chạy CREATE DATABASE chamsocthucung
    └── Chạy USE chamsocthucung và tạo các bảng

Bước 4: Kiểm tra
    ├── Tables đã tạo đủ 17 bảng
    ├── Dữ liệu mẫu đã được insert
    └── Foreign key constraint đúng
```

### 4.3. Các thay đổi code trong tuần

| File | Thay đổi |
|---|---|
| `webchamsocthucung.sln` | Đổi tên project reference |
| `Web.config` | Đổi Data Source: `localhost\SQLEXPRESS01` |
| `Views/User/index.cshtml` | `"Quách Đại Bửu"` → `"Web Chăm Só Thú Cưng"` |
| `Views/Shared/_LayoutUser.cshtml` | Logo text: `Quách Đại Bửu` → `Web Chăm Só Thú Cưng` |

---

## 5. Kết Quả Đạt Được Trong Tuần

### 5.1. Thành tựu chính

| STT | Thành tựu | Chi tiết |
|---|---|---|
| 1 | ✅ Project đổi tên hoàn chỉnh | Tất cả file và reference đã được cập nhật |
| 2 | ✅ Kết nối Database thành công | Ứng dụng chạy bình thường |
| 3 | ✅ Xóa thông tin cá nhân | Không còn "Quách Đại Bửu" trong source |
| 4 | ✅ Database tạo đầy đủ | 17 bảng, dữ liệu mẫu, constraint |
| 5 | ✅ README.md hoàn chỉnh | Tài liệu hướng dẫn chi tiết |
| 6 | ✅ Tổ chức thư mục | src/, Progress_Report/, README.md |

### 5.2. Danh sách tài khoản đã xác minh

| Loại | Tài khoản | Mật khẩu | Trạng thái |
|---|---|---|---|
| Admin | admin | 123123 | ✅ Hoạt động |
| Nhân viên 1 | staff | staff123 | ✅ Hoạt động |
| Nhân viên 2 | staff1 | staff123 | ✅ Hoạt động |
| Nhân viên 3 | staff2 | staff123 | ✅ Hoạt động |

---

## 6. Kế Hoạch Tuần Sau

| STT | Nhiệm vụ | Ưu tiên |
|---|---|---|
| 1 | Viết báo cáo tuần 3 (Tuan_3.md) | Cao |
| 2 | Hoàn thiện cấu trúc thư mục project | Cao |
| 3 | Chuẩn bị tài liệu báo cáo đồ án | Cao |
| 4 | Push code lên GitHub | Trung bình |
| 5 | Tiếp tục tìm hiểu chi tiết từng chức năng | Trung bình |

---

## 7. Nhận Xét Cá Nhân

> **Tuần thứ 2** là tuần tập trung vào việc chuẩn bị môi trường và làm sạch đồ án. Việc đổi tên project từ "Quách Đại Bửu" sang "webchamsocthucung" là cần thiết để phù hợp với thông tin cá nhân của mình. Khó khăn lớn nhất trong tuần này là lỗi kết nối SQL Server — nguyên nhân chính là tên SQL Server instance khác nhau trên từng máy. Giải pháp là phải kiểm tra chính xác tên instance bằng SQL Server Configuration Manager và SSMS trước khi cấu hình connection string. Tuần sau sẽ tập trung vào việc viết báo cáo chi tiết từng chức năng và chuẩn bị tài liệu bảo vệ đồ án.

---

**Ngày báo cáo:** 05/07/2026
**Chữ ký sinh viên:** ___________________
