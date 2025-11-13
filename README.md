# SoftwareTechnologyProject

## 1. Giới thiệu
Dự án Bookstore là hệ thống quản lý sách online với đầy đủ các tính năng:
- Quản lý sách, giỏ hàng, đơn hàng, thanh toán.
- Hồ sơ người dùng và đăng nhập/đăng ký.
- Wishlist, forum, voucher.
- Hỗ trợ khách hàng & thông báo.
- Dashboard thống kê kho và doanh thu (admin).

Ứng dụng được triển khai bằng **Frontend: ReactJS + TailwindCSS** và **Backend: Spring Boot (Java)**, kết nối với **PostgreSQL**. 

Docker được sử dụng để đóng gói và triển khai ứng dụng.

---

## 2. Công nghệ sử dụng

| Nhóm         | Công nghệ                 | Mục đích sử dụng |
| ------------ | ------------------------ | ---------------- |
| Frontend     | ReactJS + TailwindCSS     | Xây dựng giao diện người dùng, component UI nhanh, responsive |
| Backend      | Spring Boot (Java)        | Tạo RESTful API, xử lý logic nghiệp vụ |
| Database     | PostgreSQL                | Lưu trữ dữ liệu chính (users, books, orders, ...) |
| Auth & Security | JWT (JSON Web Token)    | Xác thực & phân quyền user – admin |
| API Docs     | Swagger UI                | Tài liệu và kiểm thử API |
| Test API     | Postman                   | Kiểm thử các endpoint trước khi tích hợp Frontend |
| Dev & Deploy | Docker, AWS / Render      | Đóng gói và triển khai ứng dụng |
| IDE          | IntelliJ / VSCode         | Môi trường phát triển |
| Version Control | Git + GitHub            | Quản lý mã nguồn, chia nhánh theo module |

---

## 3. Phân công module

| STT | Module                         | FE + BE liên quan                 | Owner |
| --- | ------------------------------ | -------------------------------- | ----- |
| 1   | Trang chủ & Hồ sơ              | HomePage, Search API             | Đức Thịnh |
| 2   | Đăng nhập, Đăng ký             | Auth API, Profile UI             | Đức Toàn |
| 3   | Quản lý sách                   | Book List, Book Detail           | Tấn Lộc |
| 4   | Giỏ hàng & thanh toán sơ bộ    | Cart, Checkout Preview           | Vũ Minh |
| 5   | Thanh toán                     | Cart, Checkout Preview           | Tiến Đạt |
| 6   | Quản lý đơn hàng               | Orders API, Order Detail         | Hữu Tâm |
| 7   | Wishlist, Forum, Voucher       | Wishlist Page                    | Mai Thái |
| 8   | Chi tiết sản phẩm & Filter     | Book List, Book Detail           | Hoàng Phương |
| 9   | Quản lý kho & Thống kê         | Dashboard (Charts)               | Cao Thái |
| 10  | Hỗ trợ khách hàng & Thông báo | Chat UI, Chat API, Notifications API | Ngọc Huy |

> Mỗi module có **owner riêng**, phát triển trên **feature branch** của mình.

---

## 4. Quy tắc làm việc nhóm

### 4.1. Git Flow (Cấu trúc nhánh)
```

main       -> Nhánh chính, deploy production
└── develop -> Nhánh tổng hợp, merge từ feature/*
├── feature/module1-home-search
├── feature/module2-auth
├── ...

````

- **feature/*:** nhánh phát triển riêng từng module.
- **hotfix/*:** sửa lỗi khẩn cấp sau deploy production.

### 4.2. Quy tắc tạo & đặt nhánh
```bash
git checkout develop
git pull origin develop
git checkout -b feature/moduleX-short-name
````

* Ví dụ: `feature/module3-books`

### 4.3. Quy tắc commit

```
[type]: [mô tả ngắn]
```

**Type thông dụng:**

* `feat:` thêm tính năng mới
* `fix:` sửa lỗi
* `refactor:` tối ưu code, không đổi chức năng
* `style:` chỉnh giao diện, format code
* `docs:` cập nhật tài liệu
* `test:` thêm/sửa test
* `chore:` config, script, v.v.

**Ví dụ:**

```
feat: add book CRUD API for admin
fix: update cart total calculation bug
style: adjust button color on login page
```

### 4.4. Quy trình làm việc

#### A. Làm việc trong nhánh riêng

```bash
git checkout feature/moduleX
# code & commit nhỏ
git push origin feature/moduleX
```

#### B. Pull Request (PR)

* Tạo PR từ `feature/moduleX` → `develop`.
* Gắn label: `ready for review`.
* Thành viên khác review → approve → merge.
* Xóa nhánh `feature/moduleX` sau khi merge.

#### C. Merge develop → main

* Khi toàn bộ module ổn định & test OK:

```bash
git checkout main
git merge develop
git push origin main
```

* Triển khai version lên AWS / Render.

### 4.5. Đồng bộ code (tránh conflict)

```bash
git checkout develop
git pull origin develop
git checkout feature/moduleX
git merge develop
# nếu conflict → fix → commit → push
git push origin feature/moduleX
```

---

## 5. Quy tắc code & .gitignore

* Không push thư mục build:

  * FE: `node_modules/`, `.env`, `dist/`
  * BE: `target/`, `.idea/`, `.iml/`
* Dùng `.gitignore` riêng cho FE & BE.
* Chuẩn hóa code:

  * `camelCase` cho biến, hàm
  * `PascalCase` cho class (Java)
  * RESTful API chuẩn: `/api/books/{id}`
* Test kỹ trước khi push:

  * Backend: Postman
  * Frontend: chạy local
  * Kiểm thử Docker local với DB chung

---

## 6. Triển khai

* Build Docker cho BE & FE.
* Deploy lên **AWS / Render**.
* Sử dụng DB PostgreSQL chung.

---

## 7. Liên hệ

* Mỗi module có owner riêng (tham khảo bảng phân công ở mục 3).
* Các vấn đề code, merge, conflict → trao đổi trực tiếp trên GitHub PR hoặc chat nhóm.
