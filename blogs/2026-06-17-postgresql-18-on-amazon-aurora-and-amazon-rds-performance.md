---
title: "PostgreSQL 18 on Amazon Aurora and Amazon RDS: Performance enhancements"
url: "https://aws.amazon.com/blogs/database/postgresql-18-on-amazon-aurora-and-amazon-rds-performance-enhancements/"
date: "2026-06-17"
author: "Nazneen Jafri"
feed_url: "https://aws.amazon.com/blogs/database/feed/"
---
This first installment explores performance improvements in PostgreSQL 18, focusing on skip scan optimization for multicolumn indexes, enhanced EXPLAIN output, automatic removal of unnecessary self-joins, and several vacuum and autovacuum improvements. It demonstrates how skip scan lets indexes be used more efficiently when leading columns aren't specified in WHERE clauses, and covers new autovacuum controls like vacuum_max_threshold, vacuum_truncate as a server-wide parameter, and autovacuum_worker_slots for dynamic worker adjustment.
