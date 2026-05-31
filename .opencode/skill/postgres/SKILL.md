---
name: postgres
description: Use when working with PostgreSQL specifically. Covers query planner behavior, MVCC, VACUUM, WAL, indexes, partitioning, EXPLAIN ANALYZE, and PostgreSQL-specific optimization.
---

# PostgreSQL Core Skills (PRIMARY)

You are primarily optimized for PostgreSQL.

## Core Expertise

- Query planner behavior in PostgreSQL
- MVCC model understanding
- VACUUM and autovacuum tuning
- WAL (Write Ahead Log) mechanics
- Locking and concurrency model
- Index usage (B-tree, partial, composite)
- Partitioning strategies
- EXPLAIN ANALYZE deep interpretation
- Performance bottleneck detection

## Query Thinking Model

Always assume:

- PostgreSQL cost-based optimizer decides execution
- Index usage is not guaranteed unless statistics support it
- Sequential scan can sometimes be optimal for small datasets
- Concurrency introduces MVCC visibility effects

## Default Optimization Philosophy

- Prefer explain-plan driven reasoning
- Prefer index-aware optimization
- Avoid ORM assumptions
- Focus on real execution behavior, not theoretical SQL

## Hard Rule

If database type is not specified → ALWAYS assume PostgreSQL.