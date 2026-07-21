---
title: "Blog 1"
date: 2026-04-22
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---



# Xây dựng Healthcare Data Lake bằng kiến trúc Microservices

## Giới thiệu

Trong lĩnh vực y tế, dữ liệu được tạo ra từ nhiều nguồn khác nhau như hệ thống quản lý bệnh viện, hồ sơ bệnh án điện tử, thiết bị y tế và các ứng dụng chăm sóc sức khỏe. Việc tập trung toàn bộ dữ liệu vào một **Data Lake** giúp tổ chức dễ dàng lưu trữ, quản lý và phân tích thông tin để hỗ trợ việc ra quyết định.

Kiến trúc Data Lake trên AWS không chỉ giúp xử lý khối lượng dữ liệu lớn mà còn đảm bảo khả năng mở rộng, tính bảo mật và tuân thủ các yêu cầu về quyền riêng tư của bệnh nhân.

---

## Kiến trúc Microservices

Phiên bản mới của giải pháp được thiết kế theo mô hình **Microservices** thay vì chỉ sử dụng một ứng dụng duy nhất.

Việc chia hệ thống thành nhiều dịch vụ nhỏ mang lại nhiều lợi ích:

- Các thành phần hoạt động độc lập.
- Dễ dàng mở rộng từng dịch vụ.
- Giảm ảnh hưởng khi cần nâng cấp hoặc sửa lỗi.
- Hỗ trợ phát triển song song giữa nhiều nhóm.

Các dịch vụ giao tiếp với nhau thông qua cơ chế **Publish/Subscribe**, giúp giảm sự phụ thuộc trực tiếp giữa các thành phần.

---

## Kiến trúc tổng thể

Giải pháp bao gồm nhiều microservice khác nhau, mỗi microservice đảm nhận một nhiệm vụ riêng như:

- Tiếp nhận dữ liệu từ bên ngoài.
- Kiểm tra và xác thực dữ liệu.
- Phân tích định dạng HL7.
- Lưu trữ dữ liệu vào Data Lake.
- Gửi thông báo đến các dịch vụ khác.

Các thành phần được kết nối thông qua Amazon SNS để truyền thông điệp theo mô hình bất đồng bộ.

---

## Đặc điểm của Microservices

Một kiến trúc Microservices thường có các đặc điểm sau:

- Dịch vụ nhỏ và độc lập.
- Có thể triển khai riêng biệt.
- Giao tiếp thông qua API hoặc sự kiện.
- Dễ tái sử dụng.
- Có khả năng mở rộng linh hoạt.

Khi thiết kế cần cân nhắc đến hiệu năng, khả năng mở rộng, mức độ phụ thuộc giữa các dịch vụ và việc quản lý của nhóm phát triển.

---

## Các dịch vụ AWS được sử dụng

Giải pháp sử dụng nhiều dịch vụ AWS khác nhau:

| Chức năng | Dịch vụ AWS |
|-----------|-------------|
| Lưu trữ dữ liệu | Amazon S3 |
| Hàng đợi | Amazon SQS |
| Thông báo | Amazon SNS |
| Xử lý sự kiện | AWS Lambda |
| Điều phối quy trình | AWS Step Functions |
| Cơ sở dữ liệu | Amazon DynamoDB |
| API | Amazon API Gateway |
| Định tuyến sự kiện | Amazon EventBridge |

---

## Pub/Sub Hub

Hệ thống sử dụng mô hình **Hub-and-Spoke** với Amazon SNS đóng vai trò trung tâm.

Ưu điểm:

- Giảm kết nối trực tiếp giữa các dịch vụ.
- Dễ mở rộng hệ thống.
- Hỗ trợ xử lý bất đồng bộ.
- Tăng khả năng chịu lỗi.

Tuy nhiên, cần quản lý cẩn thận các thông điệp để tránh việc một dịch vụ xử lý sai dữ liệu.

---

## Core Microservice

Core Microservice chịu trách nhiệm quản lý các thành phần nền tảng của hệ thống.

Bao gồm:

- Amazon S3 lưu trữ dữ liệu.
- Amazon DynamoDB quản lý metadata.
- AWS Lambda xử lý dữ liệu.
- Amazon SNS làm trung tâm truyền thông điệp.

Thiết kế này giúp đảm bảo dữ liệu luôn được ghi theo cùng một quy trình và hạn chế truy cập trực tiếp vào Data Lake.

---

## Front Door Microservice

Đây là điểm tiếp nhận yêu cầu từ bên ngoài thông qua Amazon API Gateway.

Các chức năng chính gồm:

- Xác thực người dùng bằng Amazon Cognito.
- Kiểm tra quyền truy cập.
- Kiểm tra dữ liệu trùng lặp.
- Chuyển dữ liệu đến các dịch vụ phía sau.

---

## Staging Microservice

Microservice này tiếp nhận dữ liệu HL7 và chuyển đổi sang định dạng JSON.

Quá trình xử lý sử dụng:

- AWS Lambda
- AWS Step Functions
- Amazon SNS

Sau khi hoàn thành, dữ liệu sẽ được gửi tiếp đến các thành phần khác để lưu trữ hoặc phân tích.

---

## Kết luận

Việc áp dụng kiến trúc Microservices giúp hệ thống Healthcare Data Lake trở nên linh hoạt, dễ mở rộng và dễ bảo trì hơn so với mô hình nguyên khối.

Kết hợp cùng các dịch vụ như Amazon S3, Lambda, SNS, DynamoDB và API Gateway, AWS cung cấp một nền tảng mạnh mẽ để xây dựng các hệ thống xử lý dữ liệu y tế hiện đại, an toàn và có khả năng mở rộng trong tương lai.