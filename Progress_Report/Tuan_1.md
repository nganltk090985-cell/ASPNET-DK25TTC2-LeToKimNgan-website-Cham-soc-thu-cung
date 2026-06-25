# BÁO CÁO TIẾN ĐỘ TUẦN 1

**Họ và tên:** Nguyễn Thị Ngân
**Mã số sinh viên:** ...
**Lớp:** ...
**Đề tài:** Website Chăm Só Thú Cưng
**Thời gian:** 22/06/2026 - 28/06/2026

---

## 1. Các Bước Chuẩn Bị

### 1.1. Chuẩn bị môi trường phát triển

| STT | Nhiệm vụ | Trạng thái | Ghi chú |
|---|---|---|---|
| 1 | Cài đặt Visual Studio 2022 Community | ✅ Hoàn thành | Cài workload ASP.NET and web development |
| 2 | Cài đặt SQL Server Express 2019 | ✅ Hoàn thành | Instance: SQLEXPRESS01 |
| 3 | Cài đặt SQL Server Management Studio (SSMS) | ✅ Hoàn thành | Phiên bản 18.x |
| 4 | Bật TCP/IP Protocol trong SQL Server Configuration Manager | ✅ Hoàn thành | Cần thiết để ứng dụng kết nối được |
| 5 | Tạo database `chamsocthucung` trên SQL Server | ✅ Hoàn thành | Chạy script tạo database |
| 6 | Clone/Download source code đồ án từ thư mục làm việc | ✅ Hoàn thành | |

### 1.2. Các công cụ sử dụng

| Công cụ | Phiên bản | Mục đích |
|---|---|---|
| Visual Studio 2022 Community | 17.x | Môi trường phát triển chính |
| SQL Server Express | 2019 | Hệ quản trị cơ sở dữ liệu |
| SSMS | 18.12 | Quản lý database |
| SQL Server Configuration Manager | - | Bật TCP/IP |
| Git | - | Quản lý phiên bản source code |

---

## 2. Các Tài Liệu Liên Quan Đã Nghiên Cứu

### 2.1. Tài liệu đọc và tham khảo

| STT | Tài liệu | Nội dung chính |
|---|---|---|
| 1 | Giáo trình ASP.NET MVC 5 | Tìm hiểu mô hình MVC, Razor View, Controller, Routing |
| 2 | Tài liệu LINQ to SQL | Cách sử dụng DBML để ánh xạ database sang model |
| 3 | W3Schools Bootstrap | Hướng dẫn Bootstrap 4 grid, component |
| 4 | Tài liệu SQL Server | Câu lệnh T-SQL, stored procedure, constraint |
| 5 | Đồ án mẫu tham khảo | Tham khảo cấu trúc project e-commerce |

### 2.2. Kiến thức ôn tập

- **ASP.NET MVC Pattern:** Model - View - Controller
- **Entity Framework / LINQ to SQL:** Ánh xạ bảng SQL sang class C#
- **Session và Cookie:** Lưu trạng thái đăng nhập người dùng
- **HTML/CSS/JS:** Xây dựng giao diện web
- **Bootstrap 4:** Responsive web design

---

## 3. Các Khó Khăn Gặp Phải Trong Tuần

### 3.1. Khó khăn về môi trường

| Khó khăn | Mô tả | Giải pháp |
|---|---|---|
| SQL Server không kết nối được | Lỗi Named Pipes Provider, error 40 khi chạy ứng dụng | Bật TCP/IP Protocol trong SQL Server Configuration Manager và restart service |
| Sai tên SQL Server instance | `Data Source=ADMIN-PC` trong Web.config không tồn tại trên máy mới | Đổi thành `localhost\SQLEXPRESS01` phù hợp với máy thực tế |
| Visual Studio không restore NuGet packages | Một số package bị missing | Chạy NuGet Package Restore hoặc cài lại packages |

### 3.2. Khó khăn về kiến thức

| Khó khăn | Mô tả | Giải pháp |
|---|---|---|
| Chưa quen với LINQ to SQL | Chưa hiểu rõ cách DBML hoạt động | Ôn lại lý thuyết, xem ví dụ từ đồ án mẫu |
| Phân biệt ASP.NET và ASP.NET MVC | Nhầm lẫn giữa Web Forms và MVC pattern | Tìm hiểu lại kiến trúc MVC 5 |
| Session trong ASP.NET MVC | Chưa nắm rõ cách lưu trạng thái đăng nhập | Sử dụng `Session["Taikhoan"]` và kiểm tra null ở Controller |

---

## 4. Các Bước Tiến Hành Trong Tuần

### 4.1. Phase 1: Khảo sát và tiếp nhận đồ án

```
Bước 1: Mở project trong Visual Studio
    └── File → Open → webchamsocthucung.sln

Bước 2: Kiểm tra cấu trúc project
    ├── Controllers/     (13 controller)
    ├── Models/          (Linq to SQL DBML + models)
    ├── Views/           (Razor views)
    ├── App_Start/      (Route, Filter, Bundle config)
    └── Content/, Scripts/

Bước 3: Kiểm tra kết nối database
    ├── Mở Web.config
    ├── Kiểm tra connectionString "WebCuaHangThuCung"
    └── Sửa Data Source phù hợp

Bước 4: Chạy thử project (F5)
    └── Kiểm tra website có load được không
```

### 4.2. Phase 2: Phân tích cấu trúc project

**Sơ đồ cấu trúc Controllers:**
```
Controllers/
├── AdminController.cs        → Quản trị, đăng nhập admin
├── AdminPQController.cs     → Phân quyền chức năng
├── BaoLoiController.cs      → Xử lý lỗi truy cập
├── DonHangController.cs    → Quản lý đơn hàng
├── GioHangController.cs    → Giỏ hàng, đặt hàng
├── HinhController.cs       → Quản lý hình ảnh sản phẩm
├── KhachHangController.cs  → Quản lý khách hàng
├── KhoHangController.cs    → Quản lý nhập kho
├── KichThuocController.cs  → Quản lý kích thước
├── LoaiController.cs      → Quản lý loại sản phẩm
├── MausacController.cs     → Quản lý màu sắc
├── SanPhamController.cs   → Quản lý sản phẩm
├── ThongKeController.cs    → Thống kê
├── ThuongHieuController.cs → Quản lý thương hiệu
└── UserController.cs       → Trang người dùng
```

**Phân tích Database Schema (17 bảng):**
- Bảng chính: `SANPHAM`, `KHACHHANG`, `ADMIN`, `DONDATHANG`
- Bảng tham chiếu: `THUONGHIEU`, `LOAI`, `MAUSAC`, `KICHTHUOC`
- Bảng giao dịch: `CTDONDATHANG`, `DangKyDichVu`, `ChiTietDichVu`
- Bảng quản trị: `PHANQUYEN`, `CHUCNANG_QUYEN`

### 4.3. Phase 3: Chạy thử các chức năng cơ bản

| Chức năng | Kết quả | Ghi chú |
|---|---|---|
| Trang chủ User | ✅ Hoạt động | Hiển thị sản phẩm, thương hiệu |
| Đăng nhập Admin | ✅ Hoạt động | Tài khoản: admin / 123123 |
| Đăng nhập User | ✅ Hoạt động | Kiểm tra Session |
| Giỏ hàng | ✅ Hoạt động | Thêm, xóa, cập nhật số lượng |
| Đặt hàng | ✅ Hoạt động | Tạo đơn hàng vào database |
| Quản lý sản phẩm | ✅ Hoạt động | CRUD đầy đủ |
| Khách sạn thú cưng | ✅ Hoạt động | Đăng ký dịch vụ theo cân nặng |
| Spa thú cưng | ✅ Hoạt động | Combo dịch vụ |

---

## 5. Kế Hoạch Tuần Sau

| STT | Nhiệm vụ | Mục tiêu |
|---|---|---|
| 1 | Đổi tên project từ "Quách Đại Bửu" sang "webchamsocthucung" | Chuẩn bị báo cáo |
| 2 | Xóa thông tin cá nhân trong source code | Bảo mật |
| 3 | Viết README.md chi tiết | Tài liệu đồ án |
| 4 | Sửa lỗi SQL Server connection string | Đảm bảo kết nối |
| 5 | Kiểm tra lại toàn bộ chức năng | Đảm bảo hoạt động |

---

## 6. Nhận Xét Cá Nhân

> **Tuần đầu tiên** chủ yếu tập trung vào việc tiếp nhận đồ án, làm quen với môi trường phát triển và cấu trúc code. Đồ án có quy mô khá lớn với 13 controllers, 17 bảng database và nhiều chức năng phức tạp như giỏ hàng, đặt hàng, phân quyền, và dịch vụ thú cưng. Việc nắm bắt toàn bộ luồng xử lý mất khá nhiều thời gian nhưng bước đầu đã hiểu được kiến trúc tổng quan của hệ thống.

---

**Ngày báo cáo:** 28/06/2026
**Chữ ký sinh viên:** ___________________
