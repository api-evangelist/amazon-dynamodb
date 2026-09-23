---
name: Provision a DynamoDB table safely
description: Create a table, wait for it to become ACTIVE, and turn on the one setting that makes a later mistake reversible — before anything writes to it.
api: openapi/amazon-dynamodb-tables-api-openapi.yml
operations: [createTable, describeTable, listTables]
generated: '2026-09-18'
method: generated
source: openapi/amazon-dynamodb-tables-api-openapi.yml + smithy/dynamodb-2012-08-10.json + conventions/amazon-dynamodb-conventions.yml + plans/amazon-dynamodb-plans-pricing.yml
---

# Provision a DynamoDB table safely

## Call shape

Every DynamoDB call is `POST /` with the operation in a header. There is no
`/tables` resource.

```
POST https://dynamodb.us-east-1.amazonaws.com/
X-Amz-Target: DynamoDB_20120810.CreateTable
Content-Type: application/x-amz-json-1.0
Authorization: AWS4-HMAC-SHA256 ...
```

## Steps

1. **Create the table.** `createTable` with `TableName`, `AttributeDefinitions`
   for the key attributes only, `KeySchema` (`HASH`, optionally `RANGE`), and
   `BillingMode`. Prefer `PAY_PER_REQUEST` unless you know the traffic shape —
   but know that on-demand request units carry **no free allowance**
   (`plans/amazon-dynamodb-plans-pricing.yml`), while 25 provisioned RCU and 25
   WCU do.
2. **Wait for ACTIVE.** `describeTable` until `Table.TableStatus` is `ACTIVE`.
   A write issued before that returns `ResourceNotFoundException`, which reads
   like "wrong table name" and is not.
3. **Turn on point-in-time recovery immediately.** `UpdateContinuousBackups`
   with `PointInTimeRecoveryEnabled: true`. This is the step that decides
   whether anything you do later can be undone: with PITR on, a `DeleteTable`
   writes a system backup retained **35 days**, and a bad write can be restored
   to any point in the configured 1–35 day window. With PITR off, both are
   permanent. See the `reversibility` block in
   `conventions/amazon-dynamodb-conventions.yml`.
4. **Confirm it exists.** `listTables`, or `describeTable` again.

## Rules that apply to every call here

- **Do not declare non-key attributes.** `AttributeDefinitions` carries key
  attributes only; declaring anything else returns `ValidationException`.
- **`ResourceInUseException`** means the table is still `CREATING`/`UPDATING` —
  wait, do not retry harder.
- **Control-plane calls throttle** with `ThrottlingException` (HTTP 400, not
  429). Back off; do not parallelise table creation loops.
- **Local secondary indexes can only be created here** and can never be removed.
  A GSI can be added later; an LSI cannot.
