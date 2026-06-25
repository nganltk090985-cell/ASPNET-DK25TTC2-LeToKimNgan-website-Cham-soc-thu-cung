# BÁO CÁO TIẾN ĐỘ TUẦN 4

**Họ và tên:** Nguyễn Thị Ngân
**Mã số sinh viên:** ...
**Lớp:** ...
**Đề tài:** Website Chăm Só Thú Cưng
**Thời gian:** 13/07/2026 - 19/07/2026

---

## 1. Các Bước Chuẩn Bị

### 1.1. Nhiệm vụ tuần 4

| STT | Nhiệm vụ | Trạng thái | Ghi chú |
|---|---|---|---|
| 1 | Push project lên GitHub | ✅ Hoàn thành | Repo: nganltk090985-cell/cngan |
| 2 | Tổ chức lại thư mục src/ | ✅ Hoàn thành | Di chuyển project vào src/ |
| 3 | Viết chi tiết báo cáo kỹ thuật | ✅ Hoàn thành | Cấu trúc, công nghệ, luồng xử lý |
| 4 | Chuẩn bị cấu trúc thư mục GitHub | ✅ Hoàn thành | Chỉ push README + Progress_Report |
| 5 | Cập nhật tài liệu README | ✅ Hoàn thành | Thông tin tài khoản, link, sơ đồ |
| 6 | Tạo file báo cáo tuần 4 | ✅ Hoàn thành | Tuan_4.md |

---

## 2. Các Tài Liệu Liên Quan Đã Nghiên Cứu

### 2.1. Tài liệu Git và GitHub

| STT | Tài liệu | Nội dung | Áp dụng |
|---|---|---|---|
| 1 | Git Handbook (GitHub Docs) | Git basic commands, push, pull, commit | Push lên GitHub |
| 2 | Creating a repo | Tạo repository qua GitHub API | Tạo repo tự động |
| 3 | Git Credential Storage | Lưu trữ token bảo mật | Bảo mật PAT |
| 4 | Gitignore patterns | Loại trừ file không cần push | .gitignore cho ASP.NET |

### 2.2. Tài liệu kỹ thuật bổ sung

| STT | Tài liệu | Nội dung |
|---|---|---|
| 1 | OWASP Security Cheat Sheet | Kiểm tra bảo mật cơ bản |
| 2 | ASP.NET MVC Best Practices | Cấu trúc project chuẩn |
| 3 | SQL Injection Prevention | Bảo mật câu truy vấn SQL |
| 4 | Session Management | Quản lý Session hiệu quả |

---

## 3. Các Khó Khăn Gặp Phải

### 3.1. Khó khăn khi push lên GitHub

| Khó khăn | Mô tả | Giải pháp |
|---|---|---|
| GitHub không hỗ trợ password trực tiếp | GitHub đã ngừng hỗ trợ password cho git operations | Sử dụng Personal Access Token (PAT) |
| Token thiếu scope `read:org` | `gh auth login` báo lỗi missing scope | Dùng `git remote` với URL chứa token |
| Tài khoản GitHub khác đang login | `gh auth status` hiển thị `truongduy1001` | `gh auth logout` trước khi login mới |
| Lỗi "Repository not found" | Repo chưa được tạo trên GitHub | Tạo repo qua GitHub REST API |
| Lỗi permission denied khi move folder | Visual Studio lock file | `cp -r` rồi `rm -rf` |

### 3.2. Khó khăn về bảo mật thông tin

| Khó khăn | Mô tả | Giải pháp |
|---|---|---|
| Thông tin cá nhân trong source | Tên "Quách Đại Bửu" xuất hiện nhiều nơi | Tìm và thay thế toàn bộ |
| Connection string trong Web.config | Chứa tên máy cũ `ADMIN-PC` | Cập nhật `localhost\SQLEXPRESS01` |
| File .git cũ | Chứa lịch sử git với tên tác giả khác | `rm -rf .git && git init` |

### 3.3. Khó khăn khi sử dụng GitHub API

```bash
# Lệnh tạo repo qua API đã sử dụng:
curl -X POST "https://api.github.com/user/repos" \
  -H "Authorization: token ghp_xxx" \
  -H "Content-Type: application/json" \
  -d '{"name":"cngan","private":false}'

# Lỗi gặp phải:
# - Token thiếu scope repo → tạo token mới với full repo scope
# - Rate limit → chờ và thử lại
```

---

## 4. Các Bước Tiến Hành Trong Tuần

### 4.1. Quy trình push lên GitHub chi tiết

```
Bước 1: Làm sạch lịch sử git
    cd D:\tvu-Project\chamsocthucung\cngan
    rm -rf .git
    git init
    → Tạo repository git mới, xóa lịch sử cũ

Bước 2: Cấu hình user cho git
    git config user.name "nganltk090985-cell"
    git config user.email "nganltk090985-cell@users.noreply.github.com"
    → Tất cả commit sẽ dùng user này

Bước 3: Tạo file .gitignore
    → Loại trừ: node_modules, bin, obj, .vs, packages/

Bước 4: Tổ chức thư mục src/
    mkdir src/
    mv chamsocthucung src/
    → Di chuyển project vào src/ (cấu trúc chuẩn)

Bước 5: Stage chỉ file cần push
    git add README.md
    git add Progress_Report/
    → KHÔNG stage: src/, scriptQDB.sql, chamsocthucung.docx

Bước 6: Tạo commit
    git commit -m "Initial commit - Progress Report and README"

Bước 7: Tạo repository trên GitHub (qua API)
    curl -X POST "https://api.github.com/user/repos" \
      -H "Authorization: token <PAT>" \
      -d '{"name":"cngan","private":false}'

Bước 8: Push lên GitHub
    git remote add origin "https://github.com/nganltk090985-cell/cngan.git"
    git branch -M main
    git push -u origin main
```

### 4.2. Cấu trúc GitHub repository

```
nganltk090985-cell/cngan (public repo)
├── README.md                    # Tài liệu hướng dẫn đồ án
├── Progress_Report/
│   ├── Tuan_1.md              # Báo cáo tuần 1
│   ├── Tuan_2.md              # Báo cáo tuần 2
│   ├── Tuan_3.md              # Báo cáo tuần 3
│   ├── Tuan_4.md              # Báo cáo tuần 4 ⬅️
│   └── Tuan_5.md              # Báo cáo tuần 5 (tuần sau)
└── (src/ KHÔNG push - chứa source code nhạy cảm)
```

### 4.3. Kiểm tra commit trên GitHub

```bash
# Verify commit author:
curl -s "https://api.github.com/repos/nganltk090985-cell/cngan/commits" \
  -H "Authorization: token <PAT>"

# Kết quả:
# author.name: "nganltk090985-cell"
# author.email: "nganltk090985-cell@users.noreply.github.com"
# committer.name: "nganltk090985-cell"
# committer.email: "nganltk090985-cell@users.noreply.github.com"
```

---

## 5. Kết Quả Đạt Được Trong Tuần

### 5.1. Thành tựu chính

| STT | Thành tựu | Chi tiết |
|---|---|---|
| 1 | ✅ Push lên GitHub thành công | Repo: https://github.com/nganltk090985-cell/cngan |
| 2 | ✅ Chỉ 1 commit duy nhất | Author: nganltk090985-cell |
| 3 | ✅ Không lộ thông tin cá nhân | Tên cũ đã được xóa hoàn toàn |
| 4 | ✅ Cấu trúc thư mục chuẩn | src/ chứa project, root chứa docs |
| 5 | ✅ README.md hoàn chỉnh | ~500 dòng, đầy đủ thông tin |
| 6 | ✅ 4 file báo cáo tuần | Tuan_1 → Tuan_4 |

### 5.2. Các file đã push lên GitHub

| File | Kích thước | Mục đích |
|---|---|---|
| README.md | ~26KB | Tài liệu hướng dẫn đồ án |
| Progress_Report/Tuan_1.md | ~12KB | Báo cáo tiến độ |
| Progress_Report/Tuan_2.md | ~13KB | Báo cáo tiến độ |
| Progress_Report/Tuan_3.md | ~14KB | Báo cáo tiến độ |
| Progress_Report/Tuan_4.md | ~13KB | Báo cáo tiến độ |

### 5.3. Các file KHÔNG push lên GitHub

| File/Thư mục | Lý do |
|---|---|
| `src/chamsocthucung/` | Chứa source code nhạy cảm, password, connection string |
| `scriptQDB.sql` | Chứa cấu trúc database đầy đủ |
| `chamsocthucung.docx` | File Word, không cần thiết trên GitHub |

---

## 6. Kế Hoạch Tuần Sau (Tuần 5)

| STT | Nhiệm vụ | Ưu tiên |
|---|---|---|
| 1 | Viết báo cáo Tuan_5.md | Rất cao |
| 2 | Tổng hợp toàn bộ tài liệu báo cáo | Rất cao |
| 3 | Chuẩn bị slide bảo vệ đồ án | Cao |
| 4 | Hoàn thiện demo các chức năng chính | Cao |
| 5 | Kiểm tra lại toàn bộ link đăng nhập | Trung bình |

---

## 7. Nhận Xét Cá Nhân

> **Tuần thứ 4** là tuần hoàn tất việc đưa đồ án lên GitHub và hoàn thiện tài liệu báo cáo. Khó khăn lớn nhất trong tuần này là việc GitHub đã ngừng hỗ trợ **password authentication** cho git operations — buộc phải sử dụng **Personal Access Token (PAT)**. Quy trình push yêu cầu phải xóa hoàn toàn `.git` cũ (vì chứa lịch sử với tên tác giả khác) và tạo lại commit mới dưới tên mình. Việc chỉ push README và Progress_Report mà không push source code là hợp lý vì source code chứa thông tin nhạy cảm như connection string và cấu trúc database đầy đủ. Tuần cuối sẽ tập trung vào việc tổng hợp tài liệu và chuẩn bị bảo vệ đồ án.

---

**Ngày báo cáo:** 19/07/2026
**Chữ ký sinh viên:** ___________________
