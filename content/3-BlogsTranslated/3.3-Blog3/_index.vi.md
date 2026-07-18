---
title: "Blog 3"
date: 2024-03-14
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# Bắt đầu với Healthcare Data Lakes: Quản lý dữ liệu bằng Microservices

Healthcare data lakes đang trở thành nền tảng quan trọng giúp các tổ chức y tế lưu trữ, quản lý và phân tích lượng dữ liệu ngày càng lớn. Thay vì lưu trữ dữ liệu ở nhiều hệ thống riêng biệt, data lake tập trung toàn bộ dữ liệu vào một nơi, từ đó hỗ trợ phân tích và ra quyết định hiệu quả hơn.

Trong bài viết này, tác giả trình bày cách áp dụng kiến trúc microservices để xây dựng hệ thống data lake. Mỗi thành phần của hệ thống được triển khai như một dịch vụ độc lập, giúp việc mở rộng, bảo trì và cập nhật trở nên đơn giản hơn. Giải pháp cũng tận dụng nhiều dịch vụ của AWS để xây dựng một nền tảng xử lý dữ liệu hiện đại.

---

## Kiến trúc hệ thống

Kiến trúc mới chia hệ thống thành nhiều microservice thay vì chỉ sử dụng một dịch vụ duy nhất. Điều này giúp:

- Dễ mở rộng khi có thêm nguồn dữ liệu mới.
- Giảm ảnh hưởng giữa các thành phần.
- Cho phép triển khai và cập nhật độc lập.
- Tăng khả năng tái sử dụng.

Các microservice giao tiếp thông qua cơ chế publish/subscribe nhằm giảm sự phụ thuộc trực tiếp giữa các dịch vụ.

---

## Các thành phần chính

### Core Microservice

Đây là thành phần trung tâm chịu trách nhiệm:

- Quản lý Data Lake trên Amazon S3.
- Lưu metadata bằng DynamoDB.
- Ghi dữ liệu thông qua AWS Lambda.
- Phát sự kiện bằng Amazon SNS.

---

### Front Door Microservice

Đây là điểm tiếp nhận yêu cầu từ người dùng.

Chức năng bao gồm:

- Cung cấp REST API.
- Xác thực bằng Amazon Cognito.
- Kiểm tra dữ liệu trùng lặp.
- Chuyển dữ liệu vào hệ thống xử lý.

---

### Staging ER7 Microservice

Microservice này chịu trách nhiệm:

- Tiếp nhận dữ liệu HL7v2.
- Chuyển đổi ER7 sang JSON.
- Kiểm tra lỗi định dạng.
- Gửi kết quả trở lại hệ thống.

---

## Công nghệ sử dụng

| Thành phần | Dịch vụ AWS |
|------------|-------------|
| Data Storage | Amazon S3 |
| Metadata | Amazon DynamoDB |
| Compute | AWS Lambda |
| Workflow | AWS Step Functions |
| Messaging | Amazon SNS |
| API | Amazon API Gateway |
| Authentication | Amazon Cognito |

---

## Điểm nổi bật

Giải pháp sử dụng kiến trúc event-driven kết hợp microservices để:

- Tăng khả năng mở rộng.
- Giảm sự phụ thuộc giữa các dịch vụ.
- Hỗ trợ xử lý dữ liệu theo thời gian thực.
- Dễ bảo trì và triển khai.

Ngoài ra, AWS CloudFormation Cross-Stack References được sử dụng để chia sẻ tài nguyên giữa nhiều stack khác nhau mà vẫn đảm bảo tính độc lập.

---

## Kết luận

Việc kết hợp microservices với các dịch vụ AWS giúp xây dựng một healthcare data lake có khả năng mở rộng cao, dễ quản lý và đáp ứng tốt yêu cầu xử lý dữ liệu y tế. Đây là một kiến trúc phù hợp cho các hệ thống cần tính linh hoạt và khả năng phát triển lâu dài.