---
name: Write and read a DynamoDB item without losing data
description: Put, get, update and delete single items with the two things the API does not give you for free — replay protection and read-your-write consistency.
api: openapi/amazon-dynamodb-items-api-openapi.yml
operations: [putItem, getItem, updateItem, deleteItem]
generated: '2026-09-18'
method: generated
source: openapi/amazon-dynamodb-items-api-openapi.yml + conventions/amazon-dynamodb-conventions.yml + errors/amazon-dynamodb-problem-types.yml
---

# Write and read a DynamoDB item without losing data

## The two defaults that bite

1. **Writes are not idempotent.** `putItem`, `updateItem` and `deleteItem` accept
   no idempotency token — only `TransactWriteItems` and `ExecuteTransaction` do
   (10-minute window). A retried `putItem` whose first attempt actually
   succeeded will overwrite.
2. **Reads are eventually consistent by default.** A `getItem` issued right after
   a `putItem` may legitimately return the previous value.

## Steps

1. **Write with a condition.** `putItem` with
   `ConditionExpression: attribute_not_exists(pk)` to make a create exclusive, or
   `#v = :expected` against a version attribute for optimistic locking. This is
   DynamoDB's replacement for `If-Match`; there is no ETag.
2. **Handle the conditional failure as information, not an error.**
   `ConditionalCheckFailedException` (HTTP 400) means your precondition did not
   hold. Set `ReturnValuesOnConditionCheckFailure: ALL_OLD` to get the item that
   blocked you back in the error, then decide. Never blind-retry it.
3. **Read back with `ConsistentRead: true`** when the read must observe the write
   you just made. It costs twice an eventual read.
4. **Update in place.** `updateItem` with an `UpdateExpression` (`SET`, `REMOVE`,
   `ADD`, `DELETE`) rather than re-putting the whole item — a full `putItem`
   silently drops attributes another writer added.
5. **Delete.** `deleteItem`, with a condition if the delete must only apply to a
   known state. There is no undo for this call: the only recovery is a
   point-in-time restore of the whole table to a new table name, and only if PITR
   was already enabled.

## Shapes and errors

- Attributes are **type-tagged**: `{"S":"text"}`, `{"N":"42"}` — numbers travel as
  strings. Use a document client (`@aws-sdk/lib-dynamodb`, the boto3 resource
  API, the Java enhanced client) rather than hand-building these.
- Items are capped at **400 KB** including attribute names.
- `ProvisionedThroughputExceededException` is retryable with exponential backoff;
  read its `ThrottlingReason` to tell a table-level throttle from a hot key.
- Every client error, throttles included, is **HTTP 400**. Branch on the `__type`
  field, never on the status code.
