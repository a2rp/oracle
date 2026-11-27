# Oracle Database: Practical Learning Notes

A structured course and reference for learning Oracle Database from relational and SQL fundamentals through PL/SQL development, application integration, security, performance, and database operations. These personal notes use Oracle AI Database 26ai as the main learning baseline and explain when a feature depends on a release, release update, deployment, edition, or license.

Oracle AI Database combines relational storage and SQL with procedural programming, multitenant architecture, JSON, analytics, availability, and administration features. A useful Oracle skill set includes more than writing queries: it also requires understanding transactions, schemas, permissions, connection services, backups, execution plans, and the operational context in which an application runs.

## Learning outcomes

By following the roadmap, you will learn to:

- Explain the relational model and the difference between a database, an instance, a CDB, and a PDB.
- Connect to an Oracle service with SQL Developer, SQLcl, SQL*Plus, and application drivers.
- Design schemas, tables, keys, constraints, data types, and indexes for reliable applications.
- Write readable SQL for filtering, joins, subqueries, grouping, analytic functions, and data changes.
- Understand Oracle transaction behavior, read consistency, locks, savepoints, commits, and rollbacks.
- Build PL/SQL blocks, procedures, functions, packages, cursors, and triggers.
- Use the data dictionary, execution plans, statistics, and tuning tools to investigate behavior.
- Work with Oracle JSON features, JSON-relational duality, and AI Vector Search when the target release supports them.
- Apply least privilege, safe dynamic SQL, auditing, backup, recovery, and availability practices.
- Recognize which capabilities vary by Oracle release, release update, deployment model, edition, and license.

## Prerequisites and version notes

Basic command-line use and familiarity with relational databases are helpful, but the early chapters introduce the required SQL concepts. To follow the examples, use an Oracle Database environment that you are allowed to access, preferably Oracle AI Database 26ai Free or a learning service that provides a compatible database. Install or use a matching client such as SQL Developer, SQLcl, or SQL*Plus.

The roadmap uses Oracle AI Database 26ai as its default reference point. Oracle Database 19c and earlier supported releases remain common in existing systems, while features introduced in 23ai or 26ai may not be available there. Release updates can also change behavior. Check the server version and the exact feature prerequisites before copying version-specific syntax into another environment. Edition, service, deployment, and license terms can affect availability and permitted use.

Use a disposable learning schema for data-changing examples. Do not run administrative commands in a production account. Use bind variables for application input, grant only required privileges, and understand a transaction before committing it.

## Quick guides

- [Oracle Database summary](oracle-summary.md)
- [Oracle Database keywords and concepts](oracle-keywords.md)

## How to use these notes

1. Follow the roadmap in order. The first chapters establish the database architecture and SQL foundations used later.
2. Read a lesson for concepts, syntax, behavior, choices, and limitations.
3. Review its matching Q&A for common questions, errors, and design decisions.
4. Run the matching example only in an environment and schema prepared for that example.
5. Use the summary for review and the keywords file to locate Oracle SQL and PL/SQL terms.
6. Check the server release before using version-specific features, and review the effect of data-changing or administrative statements.
7. Treat a successful SQL statement as only one part of a reliable system; consider data integrity, privileges, error handling, performance, and recovery.

## Course roadmap

| No. | Lesson | Q&A | Example |
|:--:|---|:--:|:--:|
| 001 | [Oracle Database foundations and the relational model](lessons/001-oracle-database-foundations-and-the-relational-model.md) | [Open Q&A](qnas/001-oracle-database-foundations-and-the-relational-model.md) | [Open example](examples/001-oracle-database-foundations-and-the-relational-model.md) |
| 002 | [Oracle AI Database releases, editions, and deployment](lessons/002-oracle-ai-database-releases-editions-and-deployment.md) | [Open Q&A](qnas/002-oracle-ai-database-releases-editions-and-deployment.md) | [Open example](examples/002-oracle-ai-database-releases-editions-and-deployment.md) |
| 003 | [Installing Oracle AI Database Free and connecting locally](lessons/003-installing-oracle-ai-database-free-and-connecting-locally.md) | [Open Q&A](qnas/003-installing-oracle-ai-database-free-and-connecting-locally.md) | [Open example](examples/003-installing-oracle-ai-database-free-and-connecting-locally.md) |
| 004 | [SQL Developer, SQLcl, and SQL*Plus](lessons/004-sql-developer-sqlcl-and-sqlplus.md) | [Open Q&A](qnas/004-sql-developer-sqlcl-and-sqlplus.md) | [Open example](examples/004-sql-developer-sqlcl-and-sqlplus.md) |
| 005 | [Network services and connection descriptors](lessons/005-network-services-and-connection-descriptors.md) | [Open Q&A](qnas/005-network-services-and-connection-descriptors.md) | [Open example](examples/005-network-services-and-connection-descriptors.md) |
| 006 | [Database instance and multitenant architecture](lessons/006-database-instance-and-multitenant-architecture.md) | [Open Q&A](qnas/006-database-instance-and-multitenant-architecture.md) | [Open example](examples/006-database-instance-and-multitenant-architecture.md) |
| 007 | [CDBs, PDBs, and container management](lessons/007-cdbs-pdbs-and-container-management.md) | [Open Q&A](qnas/007-cdbs-pdbs-and-container-management.md) | [Open example](examples/007-cdbs-pdbs-and-container-management.md) |
| 008 | [Users, schemas, and the data dictionary](lessons/008-users-schemas-and-the-data-dictionary.md) | [Open Q&A](qnas/008-users-schemas-and-the-data-dictionary.md) | [Open example](examples/008-users-schemas-and-the-data-dictionary.md) |
| 009 | [Identifiers, literals, and Oracle data types](lessons/009-identifiers-literals-and-oracle-data-types.md) | [Open Q&A](qnas/009-identifiers-literals-and-oracle-data-types.md) | [Open example](examples/009-identifiers-literals-and-oracle-data-types.md) |
| 010 | [Tables, sequences, and identity columns](lessons/010-tables-sequences-and-identity-columns.md) | [Open Q&A](qnas/010-tables-sequences-and-identity-columns.md) | [Open example](examples/010-tables-sequences-and-identity-columns.md) |
| 011 | [Constraints and relational integrity](lessons/011-constraints-and-relational-integrity.md) | [Open Q&A](qnas/011-constraints-and-relational-integrity.md) | [Open example](examples/011-constraints-and-relational-integrity.md) |
| 012 | [SELECT, expressions, aliases, and built-in functions](lessons/012-select-expressions-aliases-and-built-in-functions.md) | [Open Q&A](qnas/012-select-expressions-aliases-and-built-in-functions.md) | [Open example](examples/012-select-expressions-aliases-and-built-in-functions.md) |
| 013 | [Filtering, NULL semantics, and conditions](lessons/013-filtering-null-semantics-and-conditions.md) | [Open Q&A](qnas/013-filtering-null-semantics-and-conditions.md) | [Open example](examples/013-filtering-null-semantics-and-conditions.md) |
| 014 | [Sorting, row limiting, and pagination](lessons/014-sorting-row-limiting-and-pagination.md) | [Open Q&A](qnas/014-sorting-row-limiting-and-pagination.md) | [Open example](examples/014-sorting-row-limiting-and-pagination.md) |
| 015 | [Joins and relational query design](lessons/015-joins-and-relational-query-design.md) | [Open Q&A](qnas/015-joins-and-relational-query-design.md) | [Open example](examples/015-joins-and-relational-query-design.md) |
| 016 | [Subqueries, CTEs, and hierarchical queries](lessons/016-subqueries-ctes-and-hierarchical-queries.md) | [Open Q&A](qnas/016-subqueries-ctes-and-hierarchical-queries.md) | [Open example](examples/016-subqueries-ctes-and-hierarchical-queries.md) |
| 017 | [Set operators and complex query composition](lessons/017-set-operators-and-complex-query-composition.md) | [Open Q&A](qnas/017-set-operators-and-complex-query-composition.md) | [Open example](examples/017-set-operators-and-complex-query-composition.md) |
| 018 | [Aggregation and grouping](lessons/018-aggregation-and-grouping.md) | [Open Q&A](qnas/018-aggregation-and-grouping.md) | [Open example](examples/018-aggregation-and-grouping.md) |
| 019 | [Analytic functions and window queries](lessons/019-analytic-functions-and-window-queries.md) | [Open Q&A](qnas/019-analytic-functions-and-window-queries.md) | [Open example](examples/019-analytic-functions-and-window-queries.md) |
| 020 | [INSERT, UPDATE, DELETE, MERGE, and RETURNING](lessons/020-insert-update-delete-merge-and-returning.md) | [Open Q&A](qnas/020-insert-update-delete-merge-and-returning.md) | [Open example](examples/020-insert-update-delete-merge-and-returning.md) |
| 021 | [Transactions, consistency, and locking](lessons/021-transactions-consistency-and-locking.md) | [Open Q&A](qnas/021-transactions-consistency-and-locking.md) | [Open example](examples/021-transactions-consistency-and-locking.md) |
| 022 | [Views, materialized views, and synonyms](lessons/022-views-materialized-views-and-synonyms.md) | [Open Q&A](qnas/022-views-materialized-views-and-synonyms.md) | [Open example](examples/022-views-materialized-views-and-synonyms.md) |
| 023 | [Indexes and access paths](lessons/023-indexes-and-access-paths.md) | [Open Q&A](qnas/023-indexes-and-access-paths.md) | [Open example](examples/023-indexes-and-access-paths.md) |
| 024 | [Partitioning and large-table design](lessons/024-partitioning-and-large-table-design.md) | [Open Q&A](qnas/024-partitioning-and-large-table-design.md) | [Open example](examples/024-partitioning-and-large-table-design.md) |
| 025 | [PL/SQL blocks, variables, and control flow](lessons/025-plsql-blocks-variables-and-control-flow.md) | [Open Q&A](qnas/025-plsql-blocks-variables-and-control-flow.md) | [Open example](examples/025-plsql-blocks-variables-and-control-flow.md) |
| 026 | [PL/SQL data types, records, and collections](lessons/026-plsql-data-types-records-and-collections.md) | [Open Q&A](qnas/026-plsql-data-types-records-and-collections.md) | [Open example](examples/026-plsql-data-types-records-and-collections.md) |
| 027 | [Cursors, bulk SQL, and exception handling](lessons/027-cursors-bulk-sql-and-exception-handling.md) | [Open Q&A](qnas/027-cursors-bulk-sql-and-exception-handling.md) | [Open example](examples/027-cursors-bulk-sql-and-exception-handling.md) |
| 028 | [Procedures, functions, and parameter modes](lessons/028-procedures-functions-and-parameter-modes.md) | [Open Q&A](qnas/028-procedures-functions-and-parameter-modes.md) | [Open example](examples/028-procedures-functions-and-parameter-modes.md) |
| 029 | [Packages, triggers, and compilation](lessons/029-packages-triggers-and-compilation.md) | [Open Q&A](qnas/029-packages-triggers-and-compilation.md) | [Open example](examples/029-packages-triggers-and-compilation.md) |
| 030 | [Dynamic SQL and SQL injection defense](lessons/030-dynamic-sql-and-sql-injection-defense.md) | [Open Q&A](qnas/030-dynamic-sql-and-sql-injection-defense.md) | [Open example](examples/030-dynamic-sql-and-sql-injection-defense.md) |
| 031 | [JSON data and SQL/JSON operations](lessons/031-json-data-and-sql-json-operations.md) | [Open Q&A](qnas/031-json-data-and-sql-json-operations.md) | [Open example](examples/031-json-data-and-sql-json-operations.md) |
| 032 | [JSON-relational duality and document APIs](lessons/032-json-relational-duality-and-document-apis.md) | [Open Q&A](qnas/032-json-relational-duality-and-document-apis.md) | [Open example](examples/032-json-relational-duality-and-document-apis.md) |
| 033 | [AI Vector Search and Select AI](lessons/033-ai-vector-search-and-select-ai.md) | [Open Q&A](qnas/033-ai-vector-search-and-select-ai.md) | [Open example](examples/033-ai-vector-search-and-select-ai.md) |
| 034 | [Application drivers and connection pooling](lessons/034-application-drivers-and-connection-pooling.md) | [Open Q&A](qnas/034-application-drivers-and-connection-pooling.md) | [Open example](examples/034-application-drivers-and-connection-pooling.md) |
| 035 | [Query plans, statistics, and SQL tuning](lessons/035-query-plans-statistics-and-sql-tuning.md) | [Open Q&A](qnas/035-query-plans-statistics-and-sql-tuning.md) | [Open example](examples/035-query-plans-statistics-and-sql-tuning.md) |
| 036 | [Users, roles, and privilege security](lessons/036-users-roles-and-privilege-security.md) | [Open Q&A](qnas/036-users-roles-and-privilege-security.md) | [Open example](examples/036-users-roles-and-privilege-security.md) |
| 037 | [Auditing, encryption, and secure development](lessons/037-auditing-encryption-and-secure-development.md) | [Open Q&A](qnas/037-auditing-encryption-and-secure-development.md) | [Open example](examples/037-auditing-encryption-and-secure-development.md) |
| 038 | [Import, export, and external data](lessons/038-import-export-and-external-data.md) | [Open Q&A](qnas/038-import-export-and-external-data.md) | [Open example](examples/038-import-export-and-external-data.md) |
| 039 | [Backup, recovery, and Flashback](lessons/039-backup-recovery-and-flashback.md) | [Open Q&A](qnas/039-backup-recovery-and-flashback.md) | [Open example](examples/039-backup-recovery-and-flashback.md) |
| 040 | [High availability, monitoring, and upgrades](lessons/040-high-availability-monitoring-and-upgrades.md) | [Open Q&A](qnas/040-high-availability-monitoring-and-upgrades.md) | [Open example](examples/040-high-availability-monitoring-and-upgrades.md) |

## Repository structure

- README.md
- LICENSE
- oracle-summary.md
- oracle-keywords.md
- lessons/
- qnas/
- examples/

The lesson, Q&A, and example Markdown files are scaffolded as empty files for every roadmap chapter. Their detailed content will be written in future steps, one chapter artifact at a time.

## License

These personal learning notes are available under the [MIT License](LICENSE).