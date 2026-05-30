# DB Execution Workflow

1. Receive db-architect output.

2. Understand schema design:
   - tables
   - relations
   - constraints
   - indexes

3. Convert design into SQL:
   - CREATE TABLE
   - ALTER TABLE
   - INDEX creation

4. Create migration scripts:
   - up migration
   - down migration (if needed)

5. Validate:
   - PostgreSQL compatibility
   - relation integrity
   - constraint correctness

6. Optimize:
   - index efficiency
   - query performance assumptions

7. Output final SQL implementation.
