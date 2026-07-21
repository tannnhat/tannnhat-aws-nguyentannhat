---
title: "Worklog Tuần 6"
date: 2026-05-25
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Tìm hiểu các dịch vụ Serverless trên AWS.
* Hiểu cách xây dựng ứng dụng không cần quản lý máy chủ.
* Thực hành triển khai API và xử lý sự kiện bằng AWS Lambda.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|-----|----------|-------------|-----------------|----------------|
| 2 | Module: Tìm hiểu AWS Lambda và kiến trúc Serverless | 25/05/2026 | 25/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | Lab 22: Tạo và triển khai AWS Lambda Function | 26/05/2026 | 26/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | Module: Amazon API Gateway và tích hợp với Lambda | 27/05/2026 | 27/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | Lab 18: Xây dựng REST API bằng API Gateway và Lambda | 28/05/2026 | 28/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | Lab 25: Tích hợp Amazon S3 Trigger với AWS Lambda và kiểm tra kết quả | 29/05/2026 | 29/05/2026 | https://cloudjourney.awsstudygroup.com/ |

---

## Chi tiết Lab đã thực hành

---

### Lab 22 – AWS Lambda

#### 1. Tạo Lambda Function

- Tạo Lambda Function mới.
- Chọn Runtime phù hợp.
- Viết và triển khai hàm xử lý.
- Thực hiện Test Event.

**Hiểu:**

- Mô hình Serverless Computing.
- Chu trình thực thi của AWS Lambda.

---

### Lab 18 – Amazon API Gateway

#### 1. Xây dựng REST API

- Tạo REST API.
- Tích hợp với AWS Lambda.
- Triển khai API Stage.
- Kiểm tra Endpoint bằng trình duyệt hoặc Postman.

**Hiểu:**

- Cách API Gateway chuyển yêu cầu đến Lambda.
- Quy trình triển khai API trên AWS.

---

### Lab 25 – Amazon S3 Trigger

#### 1. Kích hoạt Lambda bằng sự kiện

- Tạo S3 Event Notification.
- Liên kết Bucket với Lambda Function.
- Upload tệp lên S3 để kích hoạt Lambda.

**Hiểu:**

- Kiến trúc Event-Driven.
- Tự động xử lý dữ liệu khi có sự kiện phát sinh.

---

### Module thực hành – Monitoring Serverless

- Theo dõi Log trên Amazon CloudWatch.
- Kiểm tra thời gian thực thi Lambda.
- Xem lịch sử Invoke và Error Log.

**Hiểu:**

- Giám sát và xử lý lỗi của ứng dụng Serverless.
- Phân tích hiệu năng của Lambda Function.

---

## Kết quả đạt được:

- Hiểu kiến trúc Serverless trên nền tảng AWS.
- Triển khai thành công AWS Lambda Function và thực hiện kiểm thử.
- Xây dựng REST API bằng Amazon API Gateway kết hợp với Lambda.
- Cấu hình Amazon S3 Trigger để tự động kích hoạt Lambda Function.
- Biết cách sử dụng Amazon CloudWatch để theo dõi Log và giám sát hoạt động của Lambda.
- Hiểu cơ chế Event-Driven Architecture và cách các dịch vụ AWS tích hợp với nhau.
- Hoàn thành các bài thực hành về Serverless Computing, tạo nền tảng cho việc phát triển ứng dụng hiện đại trên AWS.