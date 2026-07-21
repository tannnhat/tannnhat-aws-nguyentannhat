---
title: "Blog 2"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---



# Getting Started with Healthcare Data Lakes: Using Microservices

Data lakes can help hospitals and healthcare facilities transform raw data into valuable business insights while ensuring business continuity and protecting patient privacy. A **data lake** is a centralized, secure, and managed repository that stores both raw and processed data for analytics. By integrating multiple data sources, organizations can gain deeper insights and make better business decisions.

This blog post is part of a broader series about building a healthcare data lake on AWS. In the previous article, *"Getting Started with Healthcare Data Lakes: Diving into Amazon Cognito"*, the focus was on implementing authentication and authorization using Amazon Cognito together with Attribute-Based Access Control (ABAC). In this article, the focus shifts to the architectural evolution of the solution, highlighting the adoption of a **microservices architecture**, key design decisions, and additional AWS services used to improve scalability and maintainability.

---

## Architecture Guidance

The most significant architectural improvement is the decomposition of a monolithic application into multiple **microservices**. This approach increases flexibility, maintainability, and scalability. Since healthcare systems often need to process many different data formats, each connector can be implemented as an independent microservice, allowing it to be updated or replaced without affecting the rest of the system.

The services communicate through a centralized **publish/subscribe (Pub/Sub) hub**, enabling loose coupling and asynchronous communication.

The current solution is still focused on ingesting and parsing **HL7v2** messages formatted according to **Encoding Rules 7 (ER7)** through a REST API.

> **Figure 1.** Overall solution architecture with independent microservices.

---

## Characteristics of Microservices

A microservices architecture typically has the following characteristics:

- Small and independent services.
- Loosely coupled components.
- Communication through well-defined APIs or messaging.
- Each service performs a single responsibility.
- Frequently implemented using an **event-driven architecture**.

When designing microservices, developers should consider:

- Technology stack.
- Performance and scalability.
- Reusability.
- Team ownership and maintainability.

---

## Technology Choices and Communication Scope

| Communication Scope | AWS Services |
| ------------------- | ------------ |
| Within a microservice | Amazon SQS, AWS Step Functions |
| Between microservices | AWS CloudFormation Cross-Stack References, Amazon SNS |
| Between services | Amazon EventBridge, AWS Cloud Map, Amazon API Gateway |

---

## The Pub/Sub Hub

The solution adopts a **Hub-and-Spoke** messaging architecture using **Amazon SNS**.

Advantages include:

- Microservices remain independent from one another.
- Communication is based on published events.
- Fewer synchronous API calls.
- Easier system expansion and maintenance.

However, proper monitoring is required to ensure each microservice processes only the intended messages.

---

## Core Microservice

The Core Microservice provides the foundation of the platform, including:

- Amazon S3 for data storage.
- Amazon DynamoDB for the data catalog.
- AWS Lambda for processing and storing messages.
- Amazon SNS as the communication hub.
- Amazon S3 for Lambda deployment artifacts.

All write operations to the data lake are performed through AWS Lambda to ensure consistency and centralized control.

---

## Front Door Microservice

The Front Door Microservice is responsible for:

- Providing REST APIs through Amazon API Gateway.
- User authentication and authorization using Amazon Cognito.
- Implementing a custom deduplication mechanism with DynamoDB instead of SNS FIFO.

DynamoDB was selected because:

1. SNS FIFO deduplication expires after only five minutes.
2. SNS FIFO requires SQS FIFO queues.
3. The system can immediately notify senders when duplicate messages are detected.

---

## Staging ER7 Microservice

This microservice performs the following tasks:

- Receives messages from the Pub/Sub Hub.
- Converts ER7 messages into JSON using AWS Step Functions.
- Standardizes ER7 formatting.
- Parses healthcare data.
- Publishes processing results or errors back to the Pub/Sub Hub.

---

## New Feature

### AWS CloudFormation Cross-Stack References

Example Outputs from the Core Microservice:

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