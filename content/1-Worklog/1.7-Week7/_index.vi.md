---
title: "Worklog Tuần 7"
date: 2026-06-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Tìm hiểu về quản lý container và dịch vụ Kubernetes trên AWS.
* Hiểu cách triển khai ứng dụng bằng Amazon ECS và Amazon EKS.
* Thực hành triển khai ứng dụng container trên nền tảng AWS.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|-----|----------|-------------|-----------------|----------------|
| 2 | Module: Tìm hiểu Docker Container và Amazon Elastic Container Registry (ECR) | 01/06/2026 | 01/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | Lab 31: Đẩy Docker Image lên Amazon ECR | 02/06/2026 | 02/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | Module: Amazon Elastic Container Service (ECS) và Fargate | 03/06/2026 | 03/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | Lab 28: Triển khai ứng dụng bằng Amazon ECS Fargate | 04/06/2026 | 04/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | Lab 34: Tìm hiểu Amazon Elastic Kubernetes Service (EKS) và triển khai Pod cơ bản | 05/06/2026 | 05/06/2026 | https://cloudjourney.awsstudygroup.com/ |

---

## Chi tiết Lab đã thực hành

---

### Lab 31 – Amazon Elastic Container Registry (ECR)

#### 1. Quản lý Docker Image

- Tạo Amazon ECR Repository.
- Build Docker Image.
- Đăng nhập vào ECR.
- Push Docker Image lên Repository.

**Hiểu:**

- Quy trình lưu trữ Docker Image trên AWS.
- Quản lý phiên bản Image.

---

### Lab 28 – Amazon ECS Fargate

#### 1. Triển khai ứng dụng

- Tạo ECS Cluster.
- Tạo Task Definition.
- Triển khai Service bằng AWS Fargate.
- Kiểm tra trạng thái ứng dụng.

**Hiểu:**

- Triển khai Container không cần quản lý máy chủ.
- Cách ECS tự động quản lý tài nguyên.

---

### Lab 34 – Amazon EKS

#### 1. Kubernetes cơ bản

- Tạo EKS Cluster.
- Kết nối bằng kubectl.
- Triển khai Pod và Deployment.
- Kiểm tra trạng thái Cluster.

**Hiểu:**

- Kiến trúc Kubernetes trên AWS.
- Quản lý ứng dụng container bằng Amazon EKS.

---

### Module thực hành – Container Monitoring

- Theo dõi Container bằng CloudWatch.
- Kiểm tra ECS Service Health.
- Xem Log ứng dụng.

**Hiểu:**

- Giám sát và xử lý sự cố ứng dụng container.
- Theo dõi hiệu năng dịch vụ.

---

## Kết quả đạt được:

- Hiểu khái niệm Container và Docker trong môi trường AWS.
- Thành thạo quy trình lưu trữ Docker Image bằng Amazon ECR.
- Triển khai thành công ứng dụng bằng Amazon ECS Fargate.
- Hiểu sự khác biệt giữa Amazon ECS và Amazon EKS.
- Làm quen với Kubernetes thông qua Amazon EKS.
- Biết cách theo dõi Container và dịch vụ bằng Amazon CloudWatch.
- Hoàn thành các bài thực hành về Container Services, tạo nền tảng cho việc triển khai các ứng dụng microservices trên AWS.