---
title: "Worklog Tuần 4"
date: 2026-05-11
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn.
{{% /notice %}}

### Mục tiêu tuần 4:

* Tìm hiểu các dịch vụ mạng và giám sát trên AWS.
* Thực hành triển khai hệ thống mạng cơ bản, giám sát tài nguyên và quản lý DNS.
* Nâng cao kỹ năng cấu hình và kết nối các dịch vụ AWS.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|-----|----------|-------------|-----------------|----------------|
| 2 | Lab 08: Cấu hình Route 53 và quản lý DNS Domain | 11/05/2026 | 11/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | Module: Tìm hiểu Elastic Load Balancer và Auto Scaling Group | 12/05/2026 | 12/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | Lab 12: Thiết lập CloudWatch Alarm và SNS Notification | 13/05/2026 | 13/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | Module: Amazon VPC, Route Table và Internet Gateway | 14/05/2026 | 14/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | Lab 09: Triển khai VPC, Public Subnet và Security Group cho EC2 | 15/05/2026 | 15/05/2026 | https://cloudjourney.awsstudygroup.com/ |

---

## Chi tiết Lab đã thực hành

---

### Lab 08 – Amazon Route 53

#### 1. Quản lý DNS

- Tạo Hosted Zone.
- Thêm bản ghi A Record và CNAME.
- Kiểm tra khả năng phân giải tên miền.

**Hiểu:**

- Cách Route 53 quản lý DNS.
- Vai trò của Hosted Zone và các loại bản ghi DNS.

---

### Lab 12 – CloudWatch & SNS

#### 1. Giám sát tài nguyên

- Theo dõi CPU Utilization của EC2.
- Tạo CloudWatch Alarm.
- Gửi thông báo qua Amazon SNS khi vượt ngưỡng.

**Hiểu:**

- Cách giám sát tài nguyên theo thời gian thực.
- Thiết lập cảnh báo tự động khi hệ thống gặp sự cố.

---

### Lab 09 – Amazon VPC

#### 1. Cấu hình mạng

- Tạo VPC với CIDR Block.
- Tạo Public Subnet.
- Gắn Internet Gateway.
- Cấu hình Route Table.
- Tạo Security Group cho EC2.

**Hiểu:**

- Kiến trúc mạng cơ bản trong AWS.
- Cách cho phép EC2 truy cập Internet.

---

### Module thực hành – Elastic Load Balancer

- Tìm hiểu Application Load Balancer (ALB).
- Tìm hiểu Target Group.
- Phân phối lưu lượng truy cập đến nhiều EC2.

**Hiểu:**

- Cơ chế cân bằng tải.
- Tăng tính sẵn sàng của ứng dụng.

---

### Module thực hành – Auto Scaling

- Tìm hiểu Launch Template.
- Tạo Auto Scaling Group.
- Thiết lập chính sách mở rộng và thu hẹp tài nguyên.

**Hiểu:**

- Tự động mở rộng hệ thống theo nhu cầu.
- Tối ưu hiệu năng và chi phí.

---

## Kết quả đạt được:

- Hiểu nguyên lý hoạt động của Amazon VPC và các thành phần mạng cơ bản.
- Biết cách cấu hình:
  - Internet Gateway.
  - Route Table.
  - Security Group.
- Thành thạo các thao tác cơ bản với Amazon Route 53:
  - Tạo Hosted Zone.
  - Quản lý DNS Records.
- Hiểu cơ chế hoạt động của Elastic Load Balancer và Auto Scaling Group.
- Biết sử dụng CloudWatch kết hợp Amazon SNS để giám sát và gửi cảnh báo.
- Có khả năng triển khai một hệ thống AWS cơ bản với mạng, DNS, cân bằng tải và giám sát tài nguyên.