# Website Chăm Sóc Thú Cưng

## 1. Giới Thiệu Đồ Án

Đồ án **Website Chăm Sóc Thú Cưng** là hệ thống thương mại điện tử (e-commerce) dành cho cửa hàng thú cưng, được xây dựng trên nền tảng **ASP.NET MVC 5 (.NET Framework 4.7.2)** với **SQL Server**.

Hệ thống cung cấp:
- **Trang người dùng**: xem sản phẩm, giỏ hàng, đặt hàng, đăng ký dịch vụ (khách sạn, spa) cho thú cưng
- **Trang quản trị**: quản lý sản phẩm, đơn hàng, khách hàng, phân quyền nhân viên, thống kê.

---

## 2. Yêu Cầu Hệ Thống

### 2.1. Phần mềm cần cài đặt

| Phần mềm | Phiên bản tối thiểu | Link tải |
|---|---|---|
| **SQL Server Express** | 2019 trở lên | https://www.microsoft.com/en-us/sql-server/sql-server-downloads |
| **SQL Server Management Studio (SSMS)** | 18.x trở lên | https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms |
| **Visual Studio 2019/2022** | 2019 trở lên | https://visualstudio.microsoft.com/downloads/ |

### 2.2. Cài đặt SQL Server (SQL Server Express)

**Bước 1:** Tải SQL Server Express
- Truy cập: https://www.microsoft.com/en-us/sql-server/sql-server-downloads
- Chọn **"Download now"** ở mục **SQL Server Express**

**Bước 2:** Chạy file cài đặt
- Chọn **"Basic"** hoặc **"Custom"**
- Ở mục **Instance Name**: ghi nhớ tên instance (mặc định là `SQLEXPRESS` hoặc `SQLEXPRESS01`)
- Ở mục **Authentication**: chọn **"Mixed Mode"** (Windows + SQL Authentication)
- Đặt **SA password** (mật khẩu này dùng cho kết nối từ ứng dụng)
- Hoàn tất cài đặt

**Bước 3:** Bật TCP/IP Protocol
- Mở **SQL Server Configuration Manager**
- Chọn **SQL Server Network Configuration** > **Protocols for SQLEXPRESS01** (hoặc tên instance của bạn)
- Bật **TCP/IP** > OK
- Restart service **SQL Server**

**Bước 4:** Tạo database `chamsocthucung`
- Mở **SSMS** (SQL Server Management Studio)
- Kết nối đến `localhost\SQLEXPRESS01` (hoặc tên instance bạn đặt)
- Mở file `scriptQDB.sql` trong thư mục gốc project
- Chạy toàn bộ script (phím tắt: `Ctrl + A` rồi `F5`)
- Database `chamsocthucung` sẽ được tạo cùng dữ liệu mẫu

### 2.3. Cài đặt Visual Studio

**Bước 1:** Tải Visual Studio
- Truy cập: https://visualstudio.microsoft.com/downloads/
- Tải **Visual Studio Community 2022** (miễn phí)

**Bước 2:** Cài đặt workload
- Chạy Visual Studio Installer
- Chọn workload: **"ASP.NET and web development"**
- Hoàn tất cài đặt

**Bước 3:** Mở project
- Mở Visual Studio
- Chọn **Open a project or solution**
- Duyệt đến file `webchamsocthucung.sln` trong thư mục `chamsocthucung`
- Nhấn **Open**

**Bước 4:** Cấu hình Connection String
- Mở file `Web.config` trong project
- Kiểm tra dòng `Data Source` trong `connectionStrings`:
```xml
<add name="WebCuaHangThuCung"
     connectionString="Data Source=localhost\SQLEXPRESS01;Initial Catalog=chamsocthucung;Integrated Security=True"
     providerName="System.Data.SqlClient" />
```
- Thay `localhost\SQLEXPRESS01` bằng tên SQL Server instance của bạn

**Bước 5:** Chạy project
- Nhấn `F5` hoặc nhấn nút **IIS Express** (Chrome/Firefox)
- Website sẽ mở tại `https://localhost:44335/`

---

## 3. Tài Khoản Đăng Nhập

### 3.1. Tài khoản Admin (Quản trị)

| Tài khoản | Mật khẩu | Vai trò | Quyền hạn |
|---|---|---|---|
| **admin** | **123123** | Quản trị viên | Toàn quyền (tất cả chức năng) |
| **staff** | **staff123** | Nhân viên 1 | Quản lý khách hàng |
| **staff1** | **staff123** | Nhân viên 2 | Quản lý sản phẩm |
| **staff2** | **staff123** | Nhân viên 3 | Quản lý sản phẩm |

### 3.2. Tài khoản Khách hàng (Người dùng)

| Tài khoản | Mật khẩu | Ghi chú |
|---|---|---|
| **n nnn** | *(MD5 hashed)* | Tài khoản demo |
| **minh** | *(MD5 hashed)* | Tài khoản demo |
| **demo** | *(MD5 hashed)* | Tài khoản demo |
| **VoLam** | *(MD5 hashed)* | Tài khoản demo |
| **quachdaibu** | *(MD5 hashed)* | Tài khoản demo |

> Các tài khoản khách hàng cần đăng ký trực tiếp trên website để có mật khẩu.

---

## 4. Các Link Đăng Nhập

### 4.1. Trang Admin (Quản trị)

| Chức năng | Link |
|---|---|
| **Trang đăng nhập Admin** | `/Admin/dangnhap` hoặc `/Admin/dangnhap` |
| **Trang quản trị chính** | `/Admin/Index` (sau khi đăng nhập) |
| **Danh sách Admin** | `/Admin/listadmin` |
| **Đổi mật khẩu Admin** | `/Admin/DoiMK` |
| **Thông tin Admin** | `/Admin/thongtinadmin` |

### 4.2. Trang Quản Lý Phân Quyền

| Chức năng | Link |
|---|---|
| **Danh sách phân quyền** | `/AdminPQ/DSPhanQuyen` |
| **Tạo phân quyền** | `/AdminPQ/Create` |
| **Danh sách chức năng** | `/AdminPQ/DSChucNang` |

### 4.3. Trang Người Dùng (Khách hàng)

| Chức năng | Link |
|---|---|
| **Trang chủ** | `/` hoặc `/User/index` |
| **Đăng nhập** | `/User/dangnhap` |
| **Đăng ký** | `/User/dangky` |
| **Quên mật khẩu** | `/User/QuenMK` |
| **Sản phẩm** | `/User/sanpham` |
| **Giỏ hàng** | `/GioHang/GioHang` |
| **Đặt hàng** | `/GioHang/DatHang` |
| **Khách sạn thú cưng** | `/User/khachsanthucung` |
| **Spa thú cưng** | `/User/spathucung` |
| **Liên hệ** | `/User/Lienhe` |
| **Giới thiệu** | `/User/gioithieu` |
| **Blog** | `/User/blogs` |
| **Thông tin cá nhân** | `/User/thongtincanhan` |
| **Lịch sử dịch vụ** | `/User/ListServiceRegis` |

---

## 5. Các Chức Năng Chính

### 5.1. Chức năng Người dùng (Frontend)

| STT | Chức năng | Mô tả |
|---|---|---|
| 1 | Xem sản phẩm | Lọc theo loại, thương hiệu, giá, tìm kiếm |
| 2 | Chi tiết sản phẩm | Hình ảnh, mô tả, giá, số lượng |
| 3 | Giỏ hàng | Thêm, xóa, cập nhật số lượng sản phẩm |
| 4 | Đặt hàng | Thông tin giao hàng, xác nhận đơn hàng |
| 5 | Đăng ký / Đăng nhập | Tài khoản khách hàng với mật khẩu MD5 |
| 6 | Quên mật khẩu | Gửi email đặt lại mật khẩu |
| 7 | Khách sạn thú cưng | Đặt phòng khách sạn cho chó/mèo theo cân nặng |
| 8 | Spa thú cưng | Đặt dịch vụ spa, cắt tỉa, tắm rửa |
| 9 | Đăng ký dịch vụ | Combo dịch vụ khách sạn + spa |
| 10 | Liên hệ | Form gửi liên hệ |
| 11 | Thông tin cá nhân | Xem/sửa thông tin tài khoản |

### 5.2. Chức năng Admin (Backend)

| STT | Chức năng | Mô tả |
|---|---|---|
| 1 | Quản lý sản phẩm | CRUD sản phẩm, hình ảnh, kích thước, màu sắc |
| 2 | Quản lý thương hiệu | CRUD thương hiệu |
| 3 | Quản lý loại sản phẩm | CRUD loại (chó, mèo, phụ kiện...) |
| 4 | Quản lý khách hàng | CRUD thông tin khách hàng |
| 5 | Quản lý đơn hàng | Xem, duyệt, hủy đơn hàng |
| 6 | Quản lý kho | Nhập kho sản phẩm |
| 7 | Quản lý hình ảnh | Upload quản lý hình sản phẩm |
| 8 | Quản lý màu sắc | CRUD màu sắc sản phẩm |
| 9 | Quản lý kích thước | CRUD kích thước sản phẩm |
| 10 | Quản lý phân quyền | Gán quyền cho từng nhân viên |
| 11 | Quản lý chức năng | Định nghĩa chức năng hệ thống |
| 12 | Thống kê | Thống kê doanh thu, đơn hàng |
| 13 | Đổi mật khẩu | Đổi mật khẩu admin |

### 5.3. Phân Quyền Chi Tiết

| Mã quyền | Tên quyền | Quản trị | Nhân viên 1 | Nhân viên 2 | Nhân viên 3 |
|---|---|:---:|:---:|:---:|:---:|
| QL_CHUCNANG | Quản lý chức năng | Có | Không | Không | Không |
| QL_DONDATHANG | Quản lý đơn hàng | Có | Không | Không | Không |
| QL_HINHMOTA | Quản lý hình mô tả | Có | Không | Không | Không |
| QL_KHACHHANG | Quản lý khách hàng | Có | **Có** | Không | Không |
| QL_KHOSANPHAM | Quản lý kho | Có | Không | Không | Không |
| QL_KICHTHUOC | Quản lý kích thước | Có | Không | Không | Không |
| QL_LOAISANPHAM | Quản lý loại sản phẩm | Có | Không | Không | Không |
| QL_MAUSAC | Quản lý màu sắc | Có | Không | Không | Không |
| QL_PHANQUYEN | Quản lý phân quyền | Có | Không | Không | Không |
| QL_QUANTRIVIEN | Quản lý quản trị viên | Có | Không | Không | Không |
| QL_SANPHAM | Quản lý sản phẩm | Có | Không | **Có** | **Có** |
| QL_THUONGHIEU | Quản lý thương hiệu | Có | Không | Không | Không |

---

## 6. Sơ Đồ Cấu Trúc Project

```
D:\tvu-Project\chamsocthucung\cngan\
├── README.md                          # File hướng dẫn này
├── scriptQDB.sql                      # Script tạo database + dữ liệu mẫu
├── chamsocthucung\                    # Project ASP.NET MVC
│   ├── webchamsocthucung.sln         # Solution file (đã đổi tên)
│   ├── webchamsocthucung.csproj      # Project file (đã đổi tên)
│   ├── webchamsocthucung.csproj.user # User settings
│   ├── Web.config                     # Cấu hình ứng dụng
│   ├── Global.asax                    # Application entry point
│   ├── Global.asax.cs
│   │
│   ├── App_Start\                     # Cấu hình khởi tạo
│   │   ├── AdminPhanQuyen.cs          # Bộ lọc phân quyền
│   │   ├── BundleConfig.cs            # Bundle CSS/JS
│   │   ├── FilterConfig.cs             # Cấu hình filter
│   │   └── RouteConfig.cs             # Cấu hình routing
│   │
│   ├── Controllers\                   # Các Controller (11 files)
│   │   ├── AdminController.cs         # Quản trị - đăng nhập, quản lý admin
│   │   ├── AdminPQController.cs       # Phân quyền - chức năng, phân quyền
│   │   ├── BaoLoiController.cs        # Xử lý lỗi
│   │   ├── DonHangController.cs       # Quản lý đơn hàng
│   │   ├── GioHangController.cs       # Giỏ hàng, đặt hàng
│   │   ├── HinhController.cs          # Quản lý hình ảnh
│   │   ├── KhachHangController.cs     # Quản lý khách hàng
│   │   ├── KhoHangController.cs       # Quản lý kho
│   │   ├── KichThuocController.cs     # Quản lý kích thước
│   │   ├── LoaiController.cs          # Quản lý loại sản phẩm
│   │   ├── MausacController.cs        # Quản lý màu sắc
│   │   ├── SanPhamController.cs       # Quản lý sản phẩm
│   │   ├── ThongKeController.cs       # Thống kê
│   │   ├── ThuongHieuController.cs     # Quản lý thương hiệu
│   │   └── UserController.cs          # Người dùng - đăng nhập, trang chủ, giỏ hàng
│   │
│   ├── Models\                        # Các Model + LINQ to SQL
│   │   ├── DataClasses.dbml            # File DBML (database diagram)
│   │   ├── DataClasses.designer.cs     # File sinh tự động từ DBML
│   │   ├── DangKy.cs
│   │   ├── DangKyModel.cs              # Model đăng ký
│   │   ├── DangNhapModel.cs            # Model đăng nhập
│   │   ├── DoiMKadmin.cs               # Model đổi mật khẩu
│   │   ├── Giohang.cs                  # Model giỏ hàng
│   │   ├── KTDinhdangngay.cs
│   │   ├── LienheModel.cs              # Model liên hệ
│   │   ├── MahoaMD5.cs                 # Helper mã hóa MD5
│   │   ├── ProductViewModel.cs
│   │   ├── QuenMKModel.cs              # Model quên mật khẩu
│   │   └── ResetPassword.cs            # Model đặt lại mật khẩu
│   │
│   ├── ViewModels\
│   │   └── ListDVViewModel.cs          # ViewModel cho danh sách dịch vụ
│   │
│   ├── Views\                         # Các View (Razor)
│   │   ├── Shared\                     # Layout dùng chung
│   │   │   ├── _LayoutAdmin.cshtml     # Layout trang Admin
│   │   │   └── _LayoutUser.cshtml      # Layout trang người dùng
│   │   │
│   │   ├── Admin\                      # Views Admin (7 files)
│   │   │   ├── Index.cshtml             # Trang quản trị chính
│   │   │   ├── dangnhap.cshtml          # Trang đăng nhập Admin
│   │   │   ├── listadmin.cshtml          # Danh sách admin
│   │   │   ├── thongtinadmin.cshtml       # Thông tin cá nhân admin
│   │   │   ├── Create.cshtml
│   │   │   ├── Edit.cshtml
│   │   │   └── Delete.cshtml
│   │   │
│   │   ├── AdminPQ\                    # Views Phân quyền (8 files)
│   │   │   ├── DSPhanQuyen.cshtml       # Danh sách phân quyền
│   │   │   ├── DSChucNang.cshtml         # Danh sách chức năng
│   │   │   ├── ChiTietDSPhanQuyen.cshtml
│   │   │   ├── Create.cshtml
│   │   │   ├── CreateCN.cshtml          # Tạo chức năng
│   │   │   ├── Edit.cshtml
│   │   │   ├── EditCN.cshtml            # Sửa chức năng
│   │   │   └── Delete.cshtml
│   │   │
│   │   ├── SanPham\                    # Views Sản phẩm (5 files)
│   │   │   ├── Index.cshtml             # Danh sách sản phẩm
│   │   │   ├── Create.cshtml
│   │   │   ├── Edit.cshtml
│   │   │   ├── Delete.cshtml
│   │   │   └── Details.cshtml
│   │   │
│   │   ├── ThuongHieu\                 # Views Thương hiệu (5 files)
│   │   ├── Loai\                       # Views Loại sản phẩm (5 files)
│   │   ├── MauSac\                     # Views Màu sắc (5 files)
│   │   ├── KichThuoc\                  # Views Kích thước (4 files)
│   │   ├── Hinh\                       # Views Hình ảnh (5 files)
│   │   ├── KhachHang\                  # Views Khách hàng (5 files)
│   │   ├── DonHang\                    # Views Đơn hàng (4 files)
│   │   ├── GioHang\                    # Views Giỏ hàng (6 files)
│   │   ├── KhoHang\                    # Views Kho (5 files)
│   │   ├── ThongKe\                    # Views Thống kê (1 file)
│   │   ├── BaoLoi\                     # Views Lỗi (1 file)
│   │   │
│   │   └── User\                       # Views Người dùng (23 files)
│   │       ├── index.cshtml             # Trang chủ
│   │       ├── dangnhap.cshtml          # Đăng nhập
│   │       ├── dangky.cshtml             # Đăng ký
│   │       ├── sanpham.cshtml           # Tất cả sản phẩm
│   │       ├── Chitiet.cshtml           # Chi tiết sản phẩm
│   │       ├── SPTheoloai.cshtml        # Sản phẩm theo loại
│   │       ├── SPTheothuonghieu.cshtml   # Sản phẩm theo thương hiệu
│   │       ├── Ketquatimkiem.cshtml      # Kết quả tìm kiếm
│   │       ├── loai.cshtml               # Danh sách loại
│   │       ├── thuonghieu.cshtml         # Danh sách thương hiệu
│   │       ├── hinhanh.cshtml            # Hình ảnh
│   │       ├── listhinhanhnho.cshtml
│   │       ├── listhinhanhnhoduoi.cshtml
│   │       ├── hinhthuonghieu.cshtml     # Hình thương hiệu
│   │       ├── gioithieu.cshtml           # Giới thiệu
│   │       ├── Lienhe.cshtml             # Liên hệ
│   │       ├── thongbaolienhe.cshtml
│   │       ├── khachsanthucung.cshtml    # Khách sạn thú cưng
│   │       ├── spathucung.cshtml         # Spa thú cưng
│   │       ├── blogs.cshtml              # Blog
│   │       ├── thongtincanhan.cshtml     # Thông tin cá nhân
│   │       ├── Edit.cshtml               # Sửa thông tin
│   │       ├── QuenMK.cshtml            # Quên mật khẩu
│   │       ├── QuenMKxacnhan.cshtml     # Xác nhận quên mật khẩu
│   │       ├── ResetPassword.cshtml     # Đặt lại mật khẩu
│   │       ├── TrangDangKy.cshtml       # Trang đăng ký dịch vụ
│   │       └── ListServiceRegis.cshtml  # Lịch sử đăng ký dịch vụ
│   │
│   ├── Content\                        # CSS, fonts, icons
│   ├── Scripts\                        # JavaScript, jQuery
│   ├── fonts\                          # Fonts
│   ├── Properties\                     # Assembly info
│   ├── bin\                            # Output build
│   └── obj\                            # Build objects
```

---

## 7. Sơ Đồ Database (Database Diagram)

```
                              +---------------+
                              | ADMIN         |
                              |---------------|
                              | MAADMIN (PK)  |
                              | HOTEN         |
                              | DIACHI        |
                              | DIENTHOAI     |
                              | TENLOAI       |
                              | TENDN         |
                              | MATKHAU       |
                              | AVATAR        |
                              | EMAIL         |
                              +-------+-------+
                                      |
                                      | 1:N
                                      v
                              +---------------+
                              | PHANQUYEN     | <-- Junction table
                              |---------------|     (Admin ↔ ChucNang_Quyen)
                              | MAPQ (PK)     |
                              | MAADMIN (FK)  |---------+
                              | MACHUCNANG(FK)|---------+
                                                      |
                                                      v
                              +---------------+       |
                              | CHUCNANG_QUYEN|       |
                              |---------------|       |
                              | MACHUCNANG(PK)| <------+
                              | TENCN         |
                              +---------------+

+---------------+     1:N     +---------------+     1:N     +---------------+
| THUONGHIEU    |------------>| SANPHAM       |------------>| CTDONDATHANG  |
|---------------|             |---------------|             |---------------|
| MATH (PK)     |             | MASP (PK)     |             | MADH (FK)     |------+
| TENTH         |             | TENSP         |             | MASP (FK)     |      |
| LOGO          |             | DONGIAMUA     |             | SOLUONG       |      |
| ANHIEN        |             | DONGIABAN     |             | DONGIA        |      |
+---------------+             | MATH (FK)     |<----+       | THANHTIEN     |      |
        |                     | MALOAI (FK)   |     |       +---------------+      |
        |                     | MAMAUSAC(FK)  |     |               |
        | 1:N                  | MAMAUSAC(FK)  |     |               | 1:N
        v                     | SOLUONG       |     |               v
+---------------+             | HINHANH       |     |       +---------------+
| LOAI           |------------>| MOTA          |     |       | DONDATHANG   |
|---------------|             | THANHTOANON   |     |       |---------------|
| MALOAI (PK)   |             | ANHIEN        |     |       | MADH (PK)     |
| TENLOAI       |             +-------+-------+     |       | MAKH (FK)     |------+
+---------------+                     |             |       | NGAYDAT       |
        |                              | 1:N         |       | NGAYGIAO      |
        |                              v             |       | TINHTRANGDH   |
        |                     +---------------+     |       | DATHANHTOAN  |
        |                     | HINH           |     |       | TONGTIEN      |
        |                     |---------------|     |       +---------------+
        |                     | MAHINH (PK)   |     |               ^
        |                     | MASP (FK)     |-----+               | 1:N
        |                     | HINH1         |                     |
        |                     | ANHIEN        |     +---------------+
        |                     +---------------+     | KHACHHANG     |
        |                                               |---------------|
        |                     +---------------+     | MAKH (PK)     |
        |                     | MAUSAC         |     | HOTENKH       |
        |                     |---------------|     | DIENTHOAI     |
        |                     | MAMAUSAC (PK)  |     | DIACHI        |
        |                     | TENMAUSAC      |     | TENDNKH       |
        |                     | ANHIEN        |     | MATKHAUKH     |
        |                     +---------------+     | EMAIL         |
        |                                               | NGAYSINH      |
        |                     +---------------+     | HINHANH       |
        |                     | KICHTHUOC     |     +---------------+
        |                     |---------------|             |
        |                     | MAKICHTHUOC(PK)|            | 1:N
        |                     | MASP (FK)     |-------------+   v
        |                     | TENKICHTHUOC  |             +---------------+
        |                     | ANHIEN        |             | DangKyDichVu  |
        |                     +---------------+             |---------------|
        |                                               | SoDK (PK)     |
        |                     +---------------+         | MaKH (FK)     |-----+
        |                     | PHIEUNHAPKHO  |         | MaCT (FK)     |-----+
        |                     |---------------|         | NgayDangKy    |
        |                     | MAPHIEUNK (PK)|         | Hoten         |
        |                     | NGAYNK        |         | SDT           |
        |                     | MASP (FK)     |---------+ Diachi        |
        |                     | SOLUONG       |             | TongTien      |
        |                     +---------------+             | TinhTrang     |
        |                                               +---------------+
        |                                               /               \
        v                                              /                 \
+---------------+                                     /                   \
| GIAMGIA        |                                /                       \
|---------------|                               v                           v
| MAGIAMGIA (PK) |              +---------------+           +---------------+
| MASP (FK)     |-------------->| ChiTietDichVu |<----------| DichVu        |
| PHAMTRAMGIAM  |              |---------------|           |---------------|
| ANHIEN        |              | MaCT (PK)     |           | MaDV (PK)     |
+---------------+              | TieuDe        |           | TenDV         |
                                | DieuKien      |           | ComboDV       |
                                | DonGia        |           | LoaiDV        |
                                | MaDV (FK)     |-----------+---------------+
                                +---------------+
```

---

## 8. Danh Sách Bảng (Tables)

| STT | Tên bảng | Mô tả |
|---|---|---|
| 1 | **ADMIN** | Bảng quản trị viên |
| 2 | **CHUCNANG_QUYEN** | Danh mục chức năng quyền |
| 3 | **PHANQUYEN** | Bảng trung gian gán quyền cho admin |
| 4 | **KHACHHANG** | Thông tin khách hàng |
| 5 | **SANPHAM** | Sản phẩm (thú cưng, phụ kiện) |
| 6 | **THUONGHIEU** | Thương hiệu |
| 7 | **LOAI** | Loại sản phẩm (chó, mèo, phụ kiện) |
| 8 | **MAUSAC** | Màu sắc sản phẩm |
| 9 | **KICHTHUOC** | Kích thước sản phẩm |
| 10 | **HINH** | Hình ảnh sản phẩm |
| 11 | **GIAMGIA** | Chương trình giảm giá |
| 12 | **PHIEUNHAPKHO** | Phiếu nhập kho |
| 13 | **DONDATHANG** | Đơn đặt hàng |
| 14 | **CTDONDATHANG** | Chi tiết đơn đặt hàng |
| 15 | **DichVu** | Dịch vụ (khách sạn, spa) |
| 16 | **ChiTietDichVu** | Chi tiết dịch vụ (theo cân nặng) |
| 17 | **DangKyDichVu** | Đăng ký dịch vụ của khách |

---

## 9. Cấu Hình Kết Nối Database

```xml
<!-- Web.config - Connection String -->
<connectionStrings>
  <add name="WebCuaHangThuCung"
       connectionString="Data Source=localhost\SQLEXPRESS01;
                        Initial Catalog=chamsocthucung;
                        Integrated Security=True"
       providerName="System.Data.SqlClient" />
</connectionStrings>
```

**Lưu ý:** Thay `localhost\SQLEXPRESS01` bằng tên SQL Server instance của bạn.

---

## 10. Công Nghệ Sử Dụng

| Layer | Công nghệ |
|---|---|
| Frontend | HTML5, CSS3, Bootstrap 4, JavaScript, jQuery |
| Backend | ASP.NET MVC 5, C#, .NET Framework 4.7.2 |
| ORM | LINQ to SQL (DBML) |
| Database | SQL Server Express 2019 |
| UI Components | PagedList, Razor |
| Icons | Font Awesome, Glyphicons, IcoMoon |
| Authentication | Session + Cookie, MD5 hashing |
| Validation | jQuery Validation, Data Annotations |
