---
name: sql-core
description: Use when working with SQL queries, database schema design, or query optimization. Covers database-agnostic SQL principles including JOINs, GROUP BY, filtering, and execution thinking.
---

# SQL Core Principles (DATABASE-AGNOSTIC)

## Universal Concepts

- SELECT filtering logic
- JOIN types and behavior
- GROUP BY and aggregation cost
- ORDER BY performance impact
- Subquery vs join tradeoffs
- NULL handling differences
- Cardinality importance

## Performance Rules

- Always reduce dataset early (WHERE pushdown)
- Avoid unnecessary full scans
- Prefer indexed filtering when possible
- Minimize row explosion in joins

## Execution Thinking

Think in terms of:

- rows flowing through pipeline
- filter reduction stages
- join expansion cost
- sorting cost