---
title: "Worklog Tuần 2"
date: 2026-04-27
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Hoàn thành các nội dung của khóa học **AWS Cloud for Beginner**.
* Hiểu các dịch vụ nền tảng của AWS và cách triển khai tài nguyên cơ bản.
* Thực hành tạo, quản lý và giám sát tài nguyên trên AWS.

---

### Các công việc cần triển khai:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|-----|----------|-------------|-----------------|----------------|
| 2 | Module 01-01: Giới thiệu AWS Cloud, Global Infrastructure và mô hình Cloud Computing | 27/04/2026 | 27/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | Module 01-02: AWS Identity and Access Management (IAM) và bảo mật tài khoản | 28/04/2026 | 28/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | Lab 01: Tạo và cấu hình IAM User, User Group, MFA | 29/04/2026 | 29/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | Lab 02: Khởi tạo Amazon EC2, cấu hình Security Group và kết nối EC2 | 30/04/2026 | 30/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | Lab 03: Làm việc với Amazon S3 (Bucket, Object, Versioning) | 01/05/2026 | 01/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 7 | Lab 04: Theo dõi tài nguyên với CloudWatch và Billing Dashboard | 02/05/2026 | 02/05/2026 | https://cloudjourney.awsstudygroup.com/ |

---

## Chi tiết Lab đã thực hành

---

### Lab 01 – AWS IAM

#### 1. Quản lý người dùng và phân quyền

- Tạo IAM User.
- Tạo IAM Group.
- Gán User vào Group.
- Cấp quyền thông qua Policy.

**Hiểu:**

- Vai trò của IAM trong quản lý tài khoản AWS.
- Nguyên tắc phân quyền tối thiểu (Least Privilege).

---

#### 2. Thiết lập bảo mật tài khoản

- Kích hoạt MFA.
- Thiết lập Password Policy.
- Kiểm tra quyền truy cập của User.

**Hiểu:**

- Tăng cường bảo mật tài khoản AWS.
- Giảm rủi ro truy cập trái phép.

---

### Lab 02 – Amazon EC2

#### 1. Khởi tạo EC2 Instance

- Chọn Amazon Machine Image (AMI).
- Chọn Instance Type.
- Tạo Key Pair.
- Cấu hình Security Group.

**Hiểu:**

- Quy trình triển khai máy chủ ảo trên AWS.
- Vai trò của AMI và Security Group.

---

#### 2. Kết nối và quản lý EC2

- Kết nối EC2 bằng EC2 Instance Connect.
- Theo dõi trạng thái Instance.
- Khởi động, dừng và khởi động lại EC2.

**Hiểu:**

- Cách quản lý vòng đời của EC2 Instance.

---

### Lab 03 – Amazon S3

#### 1. Quản lý Bucket

- Tạo S3 Bucket.
- Upload và Download Object.
- Tạo thư mục lưu trữ.

#### 2. Quản lý dữ liệu

- Bật Versioning.
- Thiết lập Bucket Policy.
- Kiểm tra quyền truy cập đối tượng.

**Hiểu:**

- Nguyên lý lưu trữ Object Storage.
- Cách bảo vệ và quản lý dữ liệu trên Amazon S3.

---

### Lab 04 – CloudWatch & Billing

#### 1. Giám sát tài nguyên

- Theo dõi CPU Utilization của EC2.
- Xem Metrics trên CloudWatch.
- Thiết lập Alarm cơ bản.

#### 2. Quản lý chi phí

- Truy cập Billing Dashboard.
- Kiểm tra Free Tier Usage.
- Theo dõi Cost Explorer.

**Hiểu:**

- Giám sát hiệu năng tài nguyên AWS.
- Kiểm soát mức sử dụng để tránh phát sinh chi phí.

---

## Kết quả đạt được:

- Hiểu kiến trúc tổng quan của AWS Cloud.
- Nắm được cách quản lý người dùng và phân quyền bằng IAM.
- Triển khai thành công EC2 Instance và kết nối từ AWS Console.
- Thành thạo các thao tác cơ bản với Amazon S3:
  - Tạo Bucket.
  - Upload/Download dữ liệu.
  - Kích hoạt Versioning.
- Biết sử dụng CloudWatch để theo dõi tài nguyên.
- Hiểu cách kiểm tra chi phí và mức sử dụng Free Tier thông qua AWS Billing Dashboard và Cost Explorer.
- Hoàn thành các bài thực hành nền tảng, tạo tiền đề cho các nội dung nâng cao trong các tuần tiếp theo.