# Amazon DynamoDB (amazon-dynamodb)
Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability, allowing you to store and retrieve any amount of data and serve any level of request traffic using key-value and document data models.

**URL:** [Visit APIs.json URL](https://aws.amazon.com/dynamodb/)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - AWS, Database, Document Store, Key-Value, NoSQL, Serverless

## Timestamps

- **Created:** 2024-01-15
- **Modified:** 2026-04-19

## APIs

### Amazon DynamoDB API
Core API for managing Amazon DynamoDB tables, items, indexes, and performing data plane operations including single-item actions, queries, scans, batch operations, and transactions.

**Human URL:** [https://aws.amazon.com/dynamodb/](https://aws.amazon.com/dynamodb/)

#### Tags:

 - AWS, Database, Document Store, Key-Value, NoSQL

#### Properties

- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/)
- [OpenAPI](openapi/amazon-dynamodb-openapi.yml)
- [OpenAPI](https://api.apis.guru/v2/specs/amazonaws.com/dynamodb/2012-08-10/openapi.yaml)
- [JSONSchema](json-schema/amazon-dynamodb-table-schema.json)
- [JSONLD](json-ld/amazon-dynamodb-context.jsonld)
- [Pricing](https://aws.amazon.com/dynamodb/pricing/)
- [GettingStarted](https://aws.amazon.com/dynamodb/getting-started/)
- [FAQ](https://aws.amazon.com/dynamodb/faqs/)
- [TermsOfService](https://aws.amazon.com/dynamodb/sla/)
- [Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/)
- [APIReference](https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/)
- [Documentation](https://docs.aws.amazon.com/cli/latest/reference/dynamodb/)
- [Security](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/security.html)
- [JSONStructure](json-structure/amazon-dynamodb-table-structure.json)
- [Example](examples/amazon-dynamodb-table-example.json)

## Common Properties

- [Portal](https://aws.amazon.com/)
- [DeveloperPortal](https://aws.amazon.com/dynamodb/)
- [Documentation](https://docs.aws.amazon.com/dynamodb/)
- [TermsOfService](https://aws.amazon.com/service-terms/)
- [PrivacyPolicy](https://aws.amazon.com/privacy/)
- [Support](https://aws.amazon.com/premiumsupport/)
- [Blog](https://aws.amazon.com/blogs/database/)
- [GitHubOrganization](https://github.com/aws)
- [Console](https://console.aws.amazon.com/dynamodbv2/)
- [SignUp](https://signin.aws.amazon.com/signup?request_type=register)
- [Login](https://aws.amazon.com/console/)
- [StatusPage](https://health.aws.amazon.com/health/status)
- [KnowledgeCenter](https://repost.aws/knowledge-center)
- [YouTube](https://www.youtube.com/user/AmazonWebServices)
- [StackOverflow](https://stackoverflow.com/questions/tagged/amazon-dynamodb)
- [Contact](https://aws.amazon.com/contact-us/)
- [Security](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/security.html)
- [Compliance](https://aws.amazon.com/compliance/)
- [SpectralRules](rules/amazon-dynamodb-spectral-rules.yml)
- [Vocabulary](vocabulary/amazon-dynamodb-vocabulary.yaml)
- [NaftikoCapability](capabilities/dynamodb-management.yaml)

## Features

| Name | Description |
|------|-------------|
| Serverless Architecture | Fully managed, no server provisioning, patching, or capacity management required. |
| Single-Digit Millisecond Performance | Consistent performance at any scale with single-digit millisecond response times. |
| Global Tables | Multi-Region, active-active replication with up to 99.999% availability and zero RPO. |
| Automatic Scaling | On-demand mode automatically adapts to application throughput without capacity planning. |
| Transactions | ACID transactions across multiple items and tables with conditional operations. |
| Streams | DynamoDB Streams captures a time-ordered sequence of changes to items for event-driven architectures. |
| Point-in-Time Recovery | Enables continuous backups with point-in-time recovery to any second over the last 35 days. |
| TTL | Time to Live automatically deletes expired items to reduce storage costs. |

## Use Cases

| Name | Description |
|------|-------------|
| Financial Services | Fraud detection, digital onboarding, and regulatory compliance workloads requiring consistent low latency. |
| Gaming Applications | Player profiles, leaderboards, session state, and game data with high-throughput requirements. |
| E-Commerce | Shopping carts, inventory tracking, order management, and customer data platforms. |
| IoT Data Storage | High-volume telemetry data ingestion and time-series storage from IoT devices. |
| Content Management | Metadata storage and content indexing for media streaming and publishing platforms. |

## Integrations

| Name | Description |
|------|-------------|
| AWS Lambda | Event-driven processing of DynamoDB Streams with Lambda functions for real-time workflows. |
| Amazon CloudWatch | Monitor DynamoDB table metrics, set alarms, and view consumption and performance data. |
| AWS IAM | Fine-grained access control for tables, items, and attributes using IAM policies. |
| Amazon Kinesis Data Streams | Export DynamoDB changes to Kinesis for real-time analytics and archiving. |
| AWS Glue | Export DynamoDB data to S3 for analysis with Athena, Redshift Spectrum, or SageMaker. |

## Artifacts

Machine-readable API specifications organized by format.

### OpenAPI

- [Amazon Dynamodb](openapi/amazon-dynamodb-openapi.yml)

### JSON Schema

- [Amazon Dynamodb Table](json-schema/amazon-dynamodb-table-schema.json)
- [Dynamodb Openapi Attribute Definition](json-schema/dynamodb-openapi-attribute-definition-schema.json)
- [Dynamodb Openapi Attribute Value](json-schema/dynamodb-openapi-attribute-value-schema.json)
- [Dynamodb Openapi Batch Get Item Input](json-schema/dynamodb-openapi-batch-get-item-input-schema.json)
- [Dynamodb Openapi Batch Get Item Output](json-schema/dynamodb-openapi-batch-get-item-output-schema.json)
- [Dynamodb Openapi Batch Write Item Input](json-schema/dynamodb-openapi-batch-write-item-input-schema.json)
- [Dynamodb Openapi Batch Write Item Output](json-schema/dynamodb-openapi-batch-write-item-output-schema.json)
- [Dynamodb Openapi Create Table Input](json-schema/dynamodb-openapi-create-table-input-schema.json)
- [Dynamodb Openapi Create Table Output](json-schema/dynamodb-openapi-create-table-output-schema.json)
- [Dynamodb Openapi Delete Item Input](json-schema/dynamodb-openapi-delete-item-input-schema.json)
- *...and 25 more*

### JSON Structure

- [Amazon Dynamodb Table](json-structure/amazon-dynamodb-table-structure.json)
- [Dynamodb Openapi Attribute Definition](json-structure/dynamodb-openapi-attribute-definition-structure.json)
- [Dynamodb Openapi Attribute Value](json-structure/dynamodb-openapi-attribute-value-structure.json)
- [Dynamodb Openapi Batch Get Item Input](json-structure/dynamodb-openapi-batch-get-item-input-structure.json)
- [Dynamodb Openapi Batch Get Item Output](json-structure/dynamodb-openapi-batch-get-item-output-structure.json)
- [Dynamodb Openapi Batch Write Item Input](json-structure/dynamodb-openapi-batch-write-item-input-structure.json)
- [Dynamodb Openapi Batch Write Item Output](json-structure/dynamodb-openapi-batch-write-item-output-structure.json)
- [Dynamodb Openapi Create Table Input](json-structure/dynamodb-openapi-create-table-input-structure.json)
- [Dynamodb Openapi Create Table Output](json-structure/dynamodb-openapi-create-table-output-structure.json)
- [Dynamodb Openapi Delete Item Input](json-structure/dynamodb-openapi-delete-item-input-structure.json)
- *...and 25 more*

### JSON-LD

- [Amazon Dynamodb](json-ld/amazon-dynamodb-context.jsonld)

## Capabilities

Naftiko capabilities organized as shared per-API definitions composed into customer-facing workflows.

### Shared Per-API Definitions

- [Dynamodb](capabilities/shared/dynamodb.yaml) — 43 operations

### Workflow Capabilities

| Workflow | Tools | Persona |
|----------|-------|---------|
| [Dynamodb Management](capabilities/dynamodb-management.yaml) | 10 | managing DynamoDB tables, items, queries, and transactions for application developers and data engineers |

## Vocabulary

- [Amazon DynamoDB Vocabulary](vocabulary/amazon-dynamodb-vocabulary.yaml) — Unified taxonomy mapping 14 resources, 11 actions, 1 workflows, and 1 personas across operational (OpenAPI) and capability (Naftiko) dimensions

## Rules

- [Amazon Dynamodb Spectral Rules](rules/amazon-dynamodb-spectral-rules.yml) — 28 rules enforcing Amazon DynamoDB API conventions

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com