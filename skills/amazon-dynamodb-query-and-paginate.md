---
name: Query and paginate a DynamoDB table completely
description: Follow LastEvaluatedKey to the end of a Query or Scan, and know why Limit is not the number of results you get back.
api: openapi/amazon-dynamodb-queries-api-openapi.yml
operations: [query, scan]
generated: '2026-09-18'
method: generated
source: openapi/amazon-dynamodb-queries-api-openapi.yml + conventions/amazon-dynamodb-conventions.yml
---

# Query and paginate a DynamoDB table completely

## Steps

1. **Prefer `query` to `scan`.** `query` reads one partition by key and bills for
   what it reads; `scan` reads the whole table and bills for all of it. A `scan`
   on a large table is the most expensive mistake available on this API.
2. **Issue the first page.** `query` with `KeyConditionExpression`, optional
   `FilterExpression`, and `Limit` if you want smaller pages.
3. **Follow the cursor until it is gone.** If the response carries
   `LastEvaluatedKey`, send it back as `ExclusiveStartKey` and call again. The
   scan or query is finished only when `LastEvaluatedKey` is **absent**.
4. **Do not stop on an empty page.** A response with zero `Items` and a
   `LastEvaluatedKey` present is normal — `FilterExpression` is applied *after*
   the read, so a page can filter down to nothing while more data remains.

## Rules

- `Limit` caps **items examined**, not items returned, and every response is
  capped at **1 MB** regardless of `Limit`.
- `FilterExpression` does not reduce the capacity you pay for. Filtering happens
  after the read; design a key or an index instead.
- Add `ReturnConsumedCapacity: TOTAL` to see what a page actually cost — it is
  the only budget signal this API emits, and it is opt-in. There are no
  rate-limit response headers (`rate-limits/amazon-dynamodb-rate-limits.yml`).
- Set `ConsistentRead: true` only where you need it, and never on a global
  secondary index — GSIs are eventually consistent and the parameter is rejected.
