---
name: Write a DynamoDB transaction that can be safely retried
description: Use TransactWriteItems for all-or-nothing writes across items and tables — the one place this API gives you a real idempotency token.
api: openapi/amazon-dynamodb-transactions-api-openapi.yml
operations: [transactWriteItems, transactGetItems]
generated: '2026-09-18'
method: generated
source: openapi/amazon-dynamodb-transactions-api-openapi.yml + smithy/dynamodb-2012-08-10.json + conventions/amazon-dynamodb-conventions.yml
---

# Write a DynamoDB transaction that can be safely retried

## Why an agent reaches for this

`TransactWriteItems` is the only write surface on DynamoDB that accepts a
`ClientRequestToken`. If retry safety matters more than throughput, wrapping even
a single write in a transaction is a legitimate reason to use it.

## Steps

1. **Generate a `ClientRequestToken` yourself** — any unique string — and reuse
   the *same* token for every retry of the *same* logical write.
2. **Send `transactWriteItems`** with up to 100 actions, each exactly one of
   `Put`, `Update`, `Delete` or `ConditionCheck`, across one or more tables in
   one Region.
3. **Retry with the same token on a transient failure.** Within the **10-minute**
   window a repeat of the identical request has the effect of the single original
   call.
4. **Read back atomically** with `transactGetItems` when the read must see a
   consistent snapshot across items.

## Errors that mean specific things

- **`TransactionCanceledException`** — read `CancellationReasons`: one entry per
  action, saying which failed and why (`ConditionalCheckFailed`,
  `TransactionConflict`, `ThrottlingError`, `ItemCollectionSizeLimitExceeded`,
  `ValidationError`). Retry only conflict and throttling reasons.
- **`IdempotentParameterMismatchException`** — you reused the token with a
  *different* payload inside the window. Send the identical payload, or a new
  token.
- **`TransactionInProgressException`** — the same token is still executing. Wait
  and poll the outcome; do not resubmit.

## Costs and limits

- A transactional write costs **twice** a standard write; a transactional read
  costs twice a strongly consistent read.
- 100 actions and 4 MB per transaction, and no two actions may target the same
  item.
- Transactions do not cross Regions.
