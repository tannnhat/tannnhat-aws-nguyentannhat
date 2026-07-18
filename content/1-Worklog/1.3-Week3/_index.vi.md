---
title: "Worklog Tuần 3"
date: 2026-05-04
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn.
{{% /notice %}}

### Mục tiêu tuần 3:

* Tìm hiểu các dịch vụ lưu trữ và cơ sở dữ liệu trên AWS.
* Hiểu cách quản lý dữ liệu bằng Amazon S3 và Amazon RDS.
* Thực hành triển khai, quản lý và giám sát các dịch vụ lưu trữ trên AWS.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|-----|----------|-------------|-----------------|----------------|
| 2 | Module 03-01: Amazon S3 (Bucket, Object, Storage Class) | 04/05/2026 | 04/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | Module 03-02: Amazon RDS và các hệ quản trị cơ sở dữ liệu | 05/05/2026 | 05/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | Lab 05: Tạo và quản lý Amazon S3 Bucket | 06/05/2026 | 06/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | Lab 06: Triển khai Amazon RDS MySQL và kết nối từ EC2 | 07/05/2026 | 07/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | Lab 07: Backup, Snapshot và Monitoring với CloudWatch | 08/05/2026 | 08/05/2026 | https://cloudjourney.awsstudygroup.com/ |

---

## Chi tiết Lab đã thực hành

---

### Lab 05 – Amazon S3

#### 1. Tạo và quản lý Bucket

- Tạo Amazon S3 Bucket.
- Upload và Download Object.
- Tạo thư mục và quản lý dữ liệu.
- Thiết lập Bucket Policy.

**Hiểu:**

- Cách lưu trữ dữ liệu bằng Object Storage.
- Quản lý quyền truy cập đối với Bucket.

---

#### 2. Quản lý dữ liệu

- Bật Versioning.
- Xóa và khôi phục Object.
- Tìm hiểu Storage Classes.

**Hiểu:**

- Cách bảo vệ dữ liệu trên Amazon S3.
- Tối ưu chi phí lưu trữ.

---

### Lab 06 – Amazon RDS

#### 1. Triển khai cơ sở dữ liệu

- Tạo RDS MySQL Instance.
- Cấu hình Security Group.
- Thiết lập thông tin Database.

**Hiểu:**

- Quy trình triển khai cơ sở dữ liệu được quản lý trên AWS.

---

#### 2. Kết nối Database

- Kết nối RDS từ EC2.
- Kiểm tra kết nối bằng MySQL Client.
- Thực hiện tạo bảng và thêm dữ liệu.

**Hiểu:**

- Cách ứng dụng kết nối tới Amazon RDS.

---

### Lab 07 – Backup và Monitoring

#### 1. Sao lưu dữ liệu

- Tạo Database Snapshot.
- Khôi phục Database từ Snapshot.
- Kiểm tra Backup tự động.

#### 2. Giám sát hệ thống

- Theo dõi CPU và Storage trên CloudWatch.
- Thiết lập Alarm cơ bản.
- Kiểm tra trạng thái hoạt động của RDS.

**Hiểu:**

- Cách bảo vệ dữ liệu bằng Snapshot.
- Giám sát hiệu năng của dịch vụ AWS.

---

## Kết quả đạt được:

- Hiểu cách hoạt động của Amazon S3 và các Storage Classes.
- Thành thạo các thao tác cơ bản trên Amazon S3:
  - Tạo Bucket.
  - Upload/Download dữ liệu.
  - Thiết lập Versioning.
- Triển khai thành công Amazon RDS MySQL.
- Kết nối được EC2 với RDS để thực hiện thao tác trên cơ sở dữ liệu.
- Biết cách tạo Snapshot và khôi phục dữ liệu khi cần thiết.
- Sử dụng CloudWatch để theo dõi tài nguyên và thiết lập cảnh báo cơ bản.
- Hoàn thành các bài thực hành về lưu trữ và cơ sở dữ liệu, tạo nền tảng cho các nội dung AWS nâng cao ở những tuần tiếp theo.