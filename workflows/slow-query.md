# Slow Query Investigation Workflow

When analyzing a slow query:

1. Understand the query goal.
   - What is the query trying to do?
   - Read?
   - Aggregation?
   - Reporting?
   - Filtering?

2. Inspect the query.
   Check:
   - SELECT
   - WHERE
   - JOIN
   - GROUP BY
   - ORDER BY
   - LIMIT

3. Analyze execution behavior.
   Use:
   - EXPLAIN
   - EXPLAIN ANALYZE

4. Detect performance issues.

   Look for:
   - Sequential scans
   - Missing indexes
   - Large joins
   - Sorting bottlenecks
   - High row counts
   - Inefficient filters

5. Review indexing strategy.

   Check:
   - missing indexes
   - redundant indexes
   - composite index opportunities

6. Suggest improvements.

   Possible actions:
   - query rewrite
   - better indexes
   - schema adjustment
   - partitioning
   - caching

7. Explain tradeoffs.

   Mention:
   - performance impact
   - write overhead
   - maintainability
   - scalability
