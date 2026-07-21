---
title: "Blog 2"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---



# Bắt đầu với Healthcare Data Lakes: Sử dụng Microservices

Các data lake giúp các bệnh viện và cơ sở y tế chuyển đổi dữ liệu thành những thông tin có giá trị cho hoạt động kinh doanh, đồng thời đảm bảo tính liên tục của dịch vụ và bảo vệ quyền riêng tư của bệnh nhân. **Data lake** là một kho lưu trữ tập trung, được quản lý và bảo mật, cho phép lưu trữ dữ liệu ở cả dạng thô và đã xử lý để phục vụ việc phân tích. Với data lake, doanh nghiệp có thể kết hợp nhiều nguồn dữ liệu và nhiều phương pháp phân tích nhằm đưa ra quyết định chính xác hơn.

Bài viết này là một phần trong chuỗi bài hướng dẫn xây dựng Healthcare Data Lake trên AWS. Trong bài viết trước *"Getting Started with Healthcare Data Lakes: Diving into Amazon Cognito"*, tác giả đã trình bày cách sử dụng Amazon Cognito cùng với Attribute Based Access Control (ABAC) để xác thực và phân quyền người dùng. Ở bài viết này, tác giả tập trung vào việc cải tiến kiến trúc hệ thống bằng cách áp dụng mô hình **microservices**, đồng thời giới thiệu các quyết định thiết kế và những tính năng mới được bổ sung.

---

## Hướng dẫn kiến trúc

Thay đổi lớn nhất của kiến trúc là việc chia một hệ thống đơn thành nhiều **microservices** nhỏ nhằm tăng khả năng bảo trì và mở rộng. Mỗi microservice đảm nhận một chức năng riêng biệt và giao tiếp với nhau thông qua cơ chế **publish/subscribe**, giúp việc phát triển và cập nhật từng thành phần trở nên dễ dàng hơn.

Giải pháp hiện tại vẫn tập trung vào việc tiếp nhận và xử lý các **HL7v2 messages** theo chuẩn **ER7** thông qua giao diện REST.

---

## Đặc điểm của Microservices

Một hệ thống microservices thường có các đặc điểm sau:

- Kích thước nhỏ, hoạt động độc lập.
- Liên kết lỏng (Loose Coupling).
- Giao tiếp thông qua các API hoặc message được định nghĩa rõ ràng.
- Mỗi service chỉ đảm nhiệm một chức năng duy nhất.
- Thường được triển khai theo mô hình **Event-Driven Architecture**.

Khi thiết kế microservices cần xem xét:

- Công nghệ sử dụng.
- Hiệu năng và khả năng mở rộng.
- Khả năng tái sử dụng.
- Khả năng quản lý và phân chia công việc giữa các nhóm phát triển.

---

## Công nghệ được sử dụng

| Phạm vi giao tiếp | Công nghệ |
| ----------------- | --------- |
| Trong một microservice | Amazon SQS, AWS Step Functions |
| Giữa các microservices | AWS CloudFormation Cross-stack References, Amazon SNS |
| Giữa các dịch vụ | Amazon EventBridge, AWS Cloud Map, Amazon API Gateway |

---

## Pub/Sub Hub

Giải pháp sử dụng mô hình **Hub-and-Spoke** với **Amazon SNS** làm trung tâm truyền thông.

Ưu điểm:

- Các microservices không phụ thuộc trực tiếp vào nhau.
- Giảm số lượng lời gọi đồng bộ (Synchronous Calls).
- Dễ dàng mở rộng hoặc bổ sung service mới.

Tuy nhiên, hệ thống cần có cơ chế giám sát để đảm bảo mỗi microservice chỉ xử lý đúng loại message của mình.

---

## Core Microservice

Core Microservice đóng vai trò là nền tảng của toàn bộ hệ thống, bao gồm:

- Amazon S3 lưu trữ dữ liệu.
- Amazon DynamoDB quản lý Data Catalog.
- AWS Lambda xử lý và ghi dữ liệu.
- Amazon SNS làm Publish/Subscribe Hub.
- Amazon S3 lưu trữ mã nguồn Lambda và các artifacts.

Việc ghi dữ liệu vào Data Lake chỉ được thực hiện thông qua Lambda nhằm đảm bảo tính nhất quán.

---

## Front Door Microservice

Front Door Microservice chịu trách nhiệm:

- Cung cấp REST API thông qua Amazon API Gateway.
- Xác thực và phân quyền bằng Amazon Cognito.
- Quản lý cơ chế chống trùng lặp (Deduplication) bằng DynamoDB thay vì SNS FIFO.

Lý do lựa chọn DynamoDB:

1. SNS FIFO chỉ lưu thông tin chống trùng trong 5 phút.
2. SNS FIFO yêu cầu sử dụng SQS FIFO.
3. Có thể chủ động thông báo khi phát hiện message bị trùng.

---

## Staging ER7 Microservice

Service này thực hiện:

- Nhận message từ Pub/Sub Hub.
- Chuyển đổi dữ liệu ER7 sang JSON bằng AWS Step Functions.
- Chuẩn hóa định dạng ER7.
- Phân tích (Parsing) dữ liệu.
- Gửi kết quả hoặc lỗi trở lại Pub/Sub Hub.

---

## Tính năng mới

### AWS CloudFormation Cross-stack References

Ví dụ cấu hình Outputs của Core Microservice:

```yaml
Outputs:
  Bucket:
    Value: !Ref Bucket
    Export:
      Name: !Sub ${AWS::StackName}-Bucket
  ArtifactBucket:
    Value: !Ref ArtifactBucket
    Export:
      Name: !Sub ${AWS::StackName}-ArtifactBucket
  Topic:
    Value: !Ref Topic
    Export:
      Name: !Sub ${AWS::StackName}-Topic
  Catalog:
    Value: !Ref Catalog
    Export:
      Name: !Sub ${AWS::StackName}-Catalog
  CatalogArn:
    Value: !GetAtt Catalog.Arn
    Export:
      Name: !Sub ${AWS::StackName}-CatalogArn