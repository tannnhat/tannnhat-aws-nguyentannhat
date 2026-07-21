---
title: "Blog 1"
date: 2026-04-22
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---



# Getting Started with Healthcare Data Lakes: Using Microservices

Data lakes can help hospitals and healthcare organizations transform data into valuable business insights while ensuring business continuity and protecting patient privacy. A **data lake** is a centralized, managed, and secure repository that stores all types of data, both raw and processed, for analytics. It enables organizations to break down data silos, combine different analytical approaches, and make better business decisions.

This blog post is part of a larger series about building healthcare data lakes. In the previous article, *"Getting Started with Healthcare Data Lakes: Diving into Amazon Cognito"*, I explained how Amazon Cognito and Attribute-Based Access Control (ABAC) can be used to authenticate and authorize users. In this article, I describe the evolution of the solution architecture, the design decisions made, and the additional AWS services that improve scalability and maintainability.

---

## Architecture Overview

The biggest architectural improvement is breaking a monolithic application into multiple **microservices**. Healthcare systems usually process many different data formats, so each connector can be implemented as an independent microservice. This design allows developers to update or replace one service without affecting the others.

Communication between services is handled through a centralized **Publish/Subscribe (Pub/Sub) Hub**, creating a loosely coupled and highly scalable architecture.

The current implementation focuses on importing and parsing **HL7v2** messages encoded in **ER7 (Encoding Rules Version 7)** through a REST API.

---

## Characteristics of Microservices

Microservices generally have the following characteristics:

- Small and independent
- Loosely coupled
- Reusable through well-defined APIs
- Designed to perform a single responsibility
- Commonly deployed using an **event-driven architecture**

When defining microservice boundaries, consider:

- **Technical factors:** performance, reliability, scalability, technologies used
- **Business factors:** dependencies, frequency of change, reusability
- **Team factors:** ownership and cognitive load

---

## Communication Technologies

| Communication Scope | AWS Services |
| ------------------- | ------------ |
| Within one microservice | Amazon SQS, AWS Step Functions |
| Between microservices | AWS CloudFormation Cross-Stack References, Amazon SNS |
| Between different services | Amazon EventBridge, AWS Cloud Map, Amazon API Gateway |

---

## The Pub/Sub Hub

The **Hub-and-Spoke** architecture works well when several microservices need to exchange events.

Benefits include:

- Each microservice communicates only with the hub.
- Services remain loosely coupled.
- Asynchronous messaging reduces synchronous API calls.
- Easier to extend the system by adding new subscribers.

A limitation is that event routing must be monitored carefully to prevent incorrect message processing.

---

## Core Microservice

The Core Microservice provides the foundation of the system, including:

- Amazon S3 bucket for storing data
- Amazon DynamoDB for the metadata catalog
- AWS Lambda functions for processing data
- Amazon SNS topic acting as the central messaging hub
- Amazon S3 bucket for deployment artifacts

Only Lambda functions are allowed to write data into the data lake, ensuring consistency and centralized validation.

---

## Front Door Microservice

The Front Door Microservice provides external REST APIs through Amazon API Gateway.

Authentication and authorization are implemented using **Amazon Cognito** with **OpenID Connect (OIDC)**.

Instead of using SNS FIFO deduplication, DynamoDB is used because:

1. SNS deduplication lasts only five minutes.
2. SNS FIFO requires SQS FIFO.
3. Duplicate requests can be detected and reported immediately.

---

## Staging ER7 Microservice

This microservice processes incoming HL7 ER7 messages.

Workflow:

- A Lambda trigger subscribes to SNS events.
- AWS Step Functions orchestrate the workflow.
- One Lambda normalizes ER7 formatting.
- Another Lambda parses ER7 into JSON.
- Results are published back to the Pub/Sub Hub.

---

## New Feature: AWS CloudFormation Cross-Stack References

Cross-stack references allow infrastructure resources to be shared between multiple CloudFormation stacks.

Example:

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