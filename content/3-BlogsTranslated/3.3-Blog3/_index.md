---
title: "Blog 3"
date: 2026-07-11
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---



# Getting Started with Healthcare Data Lakes: Using Microservices

Data lakes can help hospitals and healthcare organizations transform data into valuable business insights while maintaining business continuity and protecting patient privacy. A **data lake** is a centralized, managed, and secure repository that stores all your data, both in its raw and processed forms for analytics. Data lakes allow organizations to eliminate data silos, combine different analytical approaches, gain deeper insights, and make better business decisions.

This blog post is part of a broader series on setting up healthcare data lakes. In the previous article, *"Getting Started with Healthcare Data Lakes: Diving into Amazon Cognito"*, I focused on using Amazon Cognito together with Attribute-Based Access Control (ABAC) to authenticate and authorize users within the healthcare data lake solution. In this article, I explain how the solution evolved at the architectural level, discuss the design decisions that were made, and introduce several additional AWS features used throughout the implementation. The complete source code for this solution is also available in the corresponding Git repository for reference.

---

## Architecture Guidance

The most significant architectural change since the previous version is the decomposition of a monolithic service into multiple independent microservices. This improves maintainability, scalability, and overall flexibility.

Healthcare environments often integrate data from many different systems and formats. By packaging each connector as an independent microservice, developers can add, modify, or replace individual connectors without affecting the rest of the application. These loosely coupled services communicate asynchronously through a centralized publish/subscribe messaging system called the **Pub/Sub Hub**.

The current implementation focuses on ingesting and parsing **HL7v2 messages** encoded using **Encoding Rules 7 (ER7)** through REST APIs.

**The updated solution architecture is shown below:**

> *Figure 1. Overall solution architecture illustrating independent microservices.*

---

Although the definition of **microservices** varies across organizations, they generally share several common characteristics:

- Small, autonomous, and loosely coupled services
- Reusable components communicating through well-defined interfaces
- Each service focuses on a single responsibility
- Commonly implemented using an **event-driven architecture**

When defining the boundaries between microservices, several aspects should be considered:

- **Technical:** technologies used, performance, reliability, and scalability
- **Business:** service dependencies, frequency of change, and reusability
- **Organizational:** team ownership and cognitive load

---

## Technology Choices and Communication Scope

| Communication Scope | AWS Services / Technologies |
| ------------------- | --------------------------- |
| Within a microservice | Amazon Simple Queue Service (Amazon SQS), AWS Step Functions |
| Between microservices within a service | AWS CloudFormation Cross-Stack References, Amazon Simple Notification Service (Amazon SNS) |
| Between independent services | Amazon EventBridge, AWS Cloud Map, Amazon API Gateway |

---

## The Pub/Sub Hub

The **Hub-and-Spoke** architecture (also known as a message broker architecture) works effectively for a relatively small number of closely related microservices.

Its primary advantages include:

- Each microservice communicates only with the central hub.
- Communication between services is limited to published message content.
- Asynchronous publish/subscribe messaging significantly reduces synchronous API calls.

One drawback is that additional coordination and monitoring are required to ensure that each microservice processes only the messages intended for it.

---

## Core Microservice

The Core Microservice provides the foundational storage and communication layer of the solution, including:

- **Amazon S3** bucket for healthcare data storage
- **Amazon DynamoDB** for maintaining the data catalog
- **AWS Lambda** functions that write messages into the data lake and metadata catalog
- **Amazon SNS** topic acting as the central messaging hub
- **Amazon S3** bucket for deployment artifacts such as Lambda packages

> Write access to the data lake is only allowed through Lambda functions to ensure centralized control and data consistency.

---

## Front Door Microservice

The Front Door Microservice provides the external entry point into the system.

Its main responsibilities include:

- Exposing REST APIs through Amazon API Gateway
- Authentication and authorization using **OIDC** with **Amazon Cognito**
- Implementing a custom deduplication mechanism with DynamoDB instead of SNS FIFO because:

1. SNS deduplication records expire after only five minutes.
2. SNS FIFO requires SQS FIFO queues.
3. The application can immediately notify the sender when duplicate messages are detected.

---

## Staging ER7 Microservice

The Staging ER7 Microservice processes incoming HL7v2 messages before they are stored.

Its workflow includes:

- Lambda triggers subscribed to the Pub/Sub Hub using message attributes
- AWS Step Functions Express Workflow for converting ER7 messages into JSON
- A Lambda function that corrects ER7 formatting (newline and carriage return characters)
- A Lambda function responsible for parsing HL7 messages
- Publishing either the processed output or any detected errors back to the Pub/Sub Hub

---

## New Features in the Solution

### 1. AWS CloudFormation Cross-Stack References

Example **Outputs** exported from the Core Microservice:

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
```