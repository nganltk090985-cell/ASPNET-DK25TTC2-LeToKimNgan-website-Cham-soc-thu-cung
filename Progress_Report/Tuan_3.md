# BÁO CÁO TIẾN ĐỘ TUẦN 3

**Họ và tên:** Nguyễn Thị Ngân
**Mã số sinh viên:** ...
**Lớp:** ...
**Đề tài:** Website Chăm Só Thú Cưng
**Thời gian:** 06/07/2026 - 12/07/2026

---

## 1. Các Bước Chuẩn Bị

### 1.1. Nhiệm vụ tuần 3

| STT | Nhiệm vụ | Trạng thái | Ghi chú |
|---|---|---|---|
| 1 | Viết chi tiết từng chức năng trong báo cáo | ✅ Hoàn thành | 12 chức năng admin + 11 user |
| 2 | Mô tả sơ đồ Database 17 bảng | ✅ Hoàn thành | ERD, quan hệ 1:N, N:N |
| 3 | Lập bảng phân quyền chi tiết | ✅ Hoàn thành | QL_SANPHAM, QL_KHACHHANG... |
| 4 | Tạo sơ đồ cấu trúc project | ✅ Hoàn thành | Tree view đầy đủ |
| 5 | Viết hướng dẫn cài đặt chi tiết | ✅ Hoàn thành | SSMS, Visual Studio, SQL Server |
| 6 | Tổng hợp link đăng nhập tất cả trang | ✅ Hoàn thành | Admin + User |

---

## 2. Các Tài Liệu Liên Quan Đã Nghiên Cứu

### 2.1. Phân tích chi tiết từng chức năng

#### A. Nhóm chức năng người dùng (Frontend)

| STT | Chức năng | Controller | View | Mô tả luồng xử lý |
|---|---|---|---|---|
| 1 | Xem sản phẩm | UserController | sanpham.cshtml | Load SANPHAM → join LOAI, THUONGHIEU → hiển thị grid |
| 2 | Chi tiết sản phẩm | UserController | Chitiet.cshtml | Load SP theo MASP → hiển thị HINH, MAUSAC, KICHTHUOC |
| 3 | Tìm kiếm sản phẩm | UserController | Ketquatimkiem.cshtml | LINQ query theo TENSP → kết quả phân trang |
| 4 | Giỏ hàng | GioHangController | GioHang.cshtml | Session["Giohang"] → List<Giohang> → tính tổng |
| 5 | Đặt hàng | GioHangController | DatHang.cshtml | Validate → tạo DONDATHANG → CTDONDATHANG → trừ SOLUONG |
| 6 | Đăng ký tài khoản | UserController | dangky.cshtml | Validate → MahoaMD5 → insert KHACHHANG |
| 7 | Đăng nhập | UserController | dangnhap.cshtml | Check TENDNKH + MATKHAUKH (MD5) → Session["Taikhoan"] |
| 8 | Khách sản thú cưng | UserController | khachsanthucung.cshtml | Load DichVu(LoaiDV=0) + ChiTietDichVu → form đăng ký |
| 9 | Spa thú cưng | UserController | spathucung.cshtml | Load DichVu(LoaiDV=1) + ChiTietDichVu → form đăng ký |
| 10 | Đăng ký dịch vụ | UserController | TrangDangKy.cshtml | Insert DangKyDichVu → gửi yêu cầu |
| 11 | Liên hệ | UserController | Lienhe.cshtml | Form gửi thông tin liên hệ |

#### B. Nhóm chức năng quản trị (Backend)

| STT | Chức năng | Controller | Mô tả |
|---|---|---|---|
| 1 | Quản lý sản phẩm | SanPhamController | CRUD SANPHAM + HINH, KICHTHUOC |
| 2 | Quản lý thương hiệu | ThuongHieuController | CRUD THUONGHIEU |
| 3 | Quản lý loại | LoaiController | CRUD LOAI |
| 4 | Quản lý màu sắc | MausacController | CRUD MAUSAC |
| 5 | Quản lý kích thước | KichThuocController | CRUD KICHTHUOC |
| 6 | Quản lý hình ảnh | HinhController | CRUD HINH, upload file |
| 7 | Quản lý khách hàng | KhachHangController | CRUD KHACHHANG |
| 8 | Quản lý đơn hàng | DonHangController | Xem/duyệt/hủy DONDATHANG |
| 9 | Quản lý kho | KhoHangController | Nhập kho: Insert PHIEUNHAPKHO, cập nhật SOLUONG |
| 10 | Phân quyền | AdminPQController | CRUD PHANQUYEN, CHUCNANG_QUYEN |
| 11 | Thống kê | ThongKeController | Đếm đơn hàng, doanh thu |
| 12 | Đổi mật khẩu | AdminController | Cập nhật MATKHAU |

---

## 3. Các Khó Khăn Gặp Phải

### 3.1. Khó khăn khi viết chi tiết từng chức năng

| Khó khăn | Mô tả | Giải pháp |
|---|---|---|
| Phức tạp luồng đặt hàng | Đặt hàng liên quan đến 3 bảng: DONDATHANG, CTDONDATHANG, KHACHHANG | Vẽ sơ đồ luồng xử lý trước khi viết |
| Đăng ký dịch vụ nhiều bước | Khách sạn → Chọn loại → Chọn chi tiết → Đăng ký → Xác nhận | Mô tả từng bước trong báo cáo |
| Phân quyền phức tạp | Mỗi nhân viên có quyền khác nhau, kiểm tra ở mỗi Action | Tìm hiểu AdminPhanQuyen.cs filter |

### 3.2. Khó khăn khi mô tả Database

| Khó khăn | Mô tả | Giải pháp |
|---|---|---|
| 17 bảng với nhiều quan hệ | Foreign key phức tạp giữa các bảng | Vẽ sơ đồ ERD chi tiết |
| Bảng trung gian PHANQUYEN | Quan hệ N:N giữa ADMIN và CHUCNANG_QUYEN | Giải thích rõ trong báo cáo |
| Constraint và Trigger | Ràng buộc CHECK, DEFAULT, FOREIGN KEY | Liệt kê chi tiết từng constraint |

---

## 4. Các Bước Tiến Hành Trong Tuần

### 4.1. Phân tích luồng xử lý đặt hàng

```
Luồng Đặt Hàng:

1. User chọn sản phẩm → Thêm vào giỏ
   Session["Giohang"] ← List<Giohang>

2. User xem giỏ hàng → /GioHang/GioHang
   Hiển thị danh sách + tính tổng tiền

3. User nhấn "Đặt hàng" → /GioHang/DatHang
   ├─ Nếu chưa đăng nhập → Redirect /User/dangnhap
   └─ Nếu đã đăng nhập → Hiển thị form

4. User điền thông tin giao hàng → Submit
   ├─ Tạo DONDATHANG mới (NGAYDAT = NOW, TINHTRANGDH = false)
   ├─ Với mỗi item trong giohang:
   │   ├─ Tạo CTDONDATHANG (MADH, MASP, SOLUONG, DONGIA)
   │   └─ Trừ SOLUONG trong SANPHAM
   └─ Xóa Session["Giohang"]

5. Xác nhận → /GioHang/Xacnhandonhang
   Hiển thị thông tin đơn hàng
```

### 4.2. Phân tích luồng đăng ký dịch vụ

```
Luồng Đăng Ký Dịch Vụ:

1. User chọn "Khách sạn thú cưng" → /User/khachsanthucung
   ├─ Load DichVu WHERE LoaiDV = 0 (Khách sạn chó)
   ├─ Load DichVu WHERE LoaiDV = 0 (Khách sạn mèo)
   └─ Load ChiTietDichVu theo MaDV + điều kiện cân nặng

2. User chọn dịch vụ → /User/TrangDangKy
   ├─ Validate thông tin thú cưng
   ├─ Validate thông tin chủ
   └─ Submit

3. Backend xử lý → Insert DangKyDichVu
   ├─ MaKH = Session["Taikhoan"].MAKH
   ├─ MaCT = Chi tiết dịch vụ đã chọn
   ├─ NgayDangKy = DateTime.Now
   └─ TinhTrang = 0 (Chờ xác nhận)

4. Admin duyệt → /DonHang/DonDKDV
   ├─ Cập nhật TinhTrang = 1 (Đã duyệt)
   └─ Thông báo cho khách
```

### 4.3. Phân tích hệ thống phân quyền

```
AdminPhanQuyen Attribute:

[AdminPhanQuyen(MACHUCNANG = "QL_SANPHAM")]
public ActionResult Index() { ... }

Khi User truy cập:
  1. Kiểm tra Session["Taikhoanadmin"] != null
  2. Lấy MAADMIN từ Session
  3. Truy vấn PHANQUYEN WHERE MAADMIN = X AND MACHUCNANG = "QL_SANPHAM"
  4. Nếu không có quyền → Redirect /BaoLoi/KhongCoQuyen
  5. Nếu có quyền → Cho phép truy cập
```

---

## 5. Kết Quả Đạt Được Trong Tuần

### 5.1. Tài liệu đã hoàn thành

| STT | Tài liệu | Mô tả |
|---|---|---|
| 1 | README.md | Hướng dẫn cài đặt, sử dụng, sơ đồ project |
| 2 | Tuan_1.md | Báo cáo tuần 1 |
| 3 | Tuan_2.md | Báo cáo tuần 2 |
| 4 | Tuan_3.md | Báo cáo tuần 3 (hiện tại) |

### 5.2. Phân tích thống kê

| Thông số | Giá trị |
|---|---|
| Tổng số Controller | 14 |
| Tổng số View | ~100 |
| Tổng số bảng Database | 17 |
| Số chức năng Admin | 12 |
| Số chức năng User | 11 |
| Số chức năng quyền | 12 |

---

## 6. Kế Hoạch Tuần Sau

| STT | Nhiệm vụ | Ưu tiên |
|---|---|---|
| 1 | Push project lên GitHub | Rất cao |
| 2 | Hoàn thiện README chi tiết hơn | Cao |
| 3 | Viết Tuan_4.md | Cao |
| 4 | Chuẩn bị slide bảo vệ | Cao |
| 5 | Kiểm tra lại toàn bộ chức năng | Trung bình |

---

## 7. Nhận Xét Cá Nhân

> **Tuần thứ 3** tập trung vào việc phân tích chi tiết từng chức năng để viết báo cáo. Đồ án có quy mô lớn với nhiều chức năng phức tạp, đặc biệt là hệ thống **phân quyền** với 12 loại quyền khác nhau và 4 nhân viên được gán quyền riêng biệt. Phần khó nhất trong tuần này là **luồng đặt hàng** vì nó liên quan đến nhiều bảng và phải đồng thời cập nhật số lượng tồn kho. Hệ thống **dịch vụ thú cưng** (khách sạn + spa) cũng là điểm nổi bật của đồ án vì không phải đồ án thương mại điện tử nào cũng có.

---

**Ngày báo cáo:** 12/07/2026
**Chữ ký sinh viên:** ___________________
