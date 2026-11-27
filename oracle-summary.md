# Oracle Database Summary

This file is a topic-wide review of Oracle Database concepts. It complements the course roadmap with a compact mental model for architecture, SQL, PL/SQL, application development, and operations.

## Scope and version baseline

These notes use Oracle AI Database 26ai, Release 26, as the primary baseline. Oracle Database 19c remains common in existing systems, and older releases may still be encountered; their support status varies. Syntax and behavior can vary by release, release update, edition, deployment, initialization parameters, and licensed options. Treat version-sensitive features as conditional and check the actual server before relying on them.

The SQL and PL/SQL languages have distinct reference rules. SQL statements operate on database objects and data. PL/SQL adds procedural constructs that can call SQL and run inside the database. SQL*Plus, SQLcl, SQL Developer, and application drivers are clients; they are not the database engine.

## 1. The Oracle database mental model

A relational database stores related facts in tables. A row represents one record and a column represents one attribute. Keys and constraints express identity and relationships. SQL describes data operations, while the database optimizer chooses an execution plan.

An Oracle database server has a database and at least one database instance:

- The database is the persistent set of files that hold data and metadata.
- The instance is the memory structures and processes that manage access to the database.
- The System Global Area (SGA) contains shared memory such as the database buffer cache, shared pool, and redo log buffer.
- A server process handles work for a database session. Background processes perform work such as writing modified blocks, writing redo, and recovering transactions.
- The Program Global Area (PGA) holds private memory for an individual server process.

In a multitenant configuration, a container database (CDB) contains a root container and one or more pluggable databases (PDBs). The root stores common Oracle metadata and common users. A PDB contains application data and objects and is the normal connection target for application work. Starting with Oracle Database 21c, the multitenant architecture is the only supported architecture. Do not assume that a PDB is a separate physical server or that connecting to the root is appropriate for application queries.

## 2. Physical and logical storage

Oracle separates logical storage concepts from physical files:

- Data files store database blocks.
- A tablespace is a logical container for segments and is backed by one or more data files.
- A segment belongs to a space-consuming object such as a table, index, or undo segment.
- Extents are groups of blocks allocated to a segment.
- A data block is the smallest logical unit of Oracle database storage.
- Control files record database structure and status information.
- Online redo logs record changes needed for instance recovery. Archived redo logs preserve completed redo for recovery and standby use.
- Undo records support rollback, read consistency, and some Flashback operations.
- Temporary tablespaces hold transient work data such as sorts and hash operations.

A schema is a logical collection of objects owned by a database user. A schema is not a tablespace. Objects in one schema can occupy different tablespaces, and a tablespace can contain objects belonging to different schemas.

## 3. Connections and client tools

A client connects through a listener to a database service. A service identifies a workload or PDB destination. A SID identifies an instance and is not interchangeable with a service name. Local connection methods and cloud services can use different connection details.

Common tools have different roles:

- SQL Developer is a graphical client for browsing objects, writing SQL, and managing connections.
- SQLcl is a modern command-line client with scripting and developer workflows.
- SQL*Plus is a long-standing command-line client and scripting environment.
- Application drivers such as JDBC, python-oracledb, node-oracledb, and OCI connect application code to a database.

Store credentials in a wallet, secret manager, or an interactive credential prompt. Avoid passwords in source files, committed scripts, shell history, or connection strings visible to other processes. Use the least privileged account that can complete the task.

## 4. Schema design and data types

Choose types that represent the domain and expected range:

- NUMBER stores decimal numeric values with optional precision and scale. Pick precision and scale deliberately for money and measured quantities.
- VARCHAR2 stores variable-length character data. Choose a meaningful maximum length and understand byte versus character semantics.
- CHAR stores fixed-length character values and can add padding behavior.
- DATE stores year, month, day, hour, minute, and second, but no time-zone offset.
- TIMESTAMP provides fractional seconds. The time-zone variants carry or normalize time-zone information according to their type.
- CLOB and NCLOB store large character data; BLOB stores binary data.
- RAW stores small binary values.
- Oracle AI Database 26ai includes a native JSON data type, but JSON support and SQL behavior depend on the target release.

Define a primary key for row identity. Use foreign keys for relationships, NOT NULL for required values, UNIQUE for alternate uniqueness, and CHECK for row-level rules. Avoid encoding business rules only in application code if the database can enforce them safely.

Oracle currently treats a zero-length character string as NULL. This behavior is a compatibility detail that application code should not silently assume will remain unchanged forever. NULL means unknown or absent, not zero or an empty ordinary value. Comparisons with NULL use three-valued logic; use IS NULL or IS NOT NULL rather than = NULL.

## 5. SQL query shape

A SELECT query describes the requested result. The optimizer chooses access paths and join order based on query structure, constraints, indexes, statistics, and the available system resources.

A common query sequence is:

1. FROM and JOIN identify row sources.
2. WHERE filters individual rows.
3. GROUP BY forms groups.
4. HAVING filters groups.
5. SELECT computes output expressions.
6. ORDER BY sorts the result.
7. A row-limiting clause limits rows after ordering.

The textual order of clauses does not mean the server executes them in that same sequence. Use explicit join conditions, qualify ambiguous column names, prefer meaningful aliases, and use bind variables for application values. A query that limits rows without a deterministic ORDER BY can return different rows between executions.

Useful predicates include equality and inequality, IN, BETWEEN, LIKE, EXISTS, and NULL checks. Use parentheses when combining AND and OR conditions. Remember that a NULL comparison is neither TRUE nor FALSE, and it can cause a row to be filtered out.

Set operators compose compatible query results. UNION removes duplicate rows; UNION ALL preserves them and usually avoids duplicate elimination work. INTERSECT returns common rows, and MINUS returns rows present in the first result but not the second. Corresponding select-list expressions need compatible data types and positions.

## 6. DML, transactions, and consistency

INSERT adds rows, UPDATE changes rows, DELETE removes rows, and MERGE combines conditional insert and update behavior. A data-changing statement is a transaction until it is committed or rolled back. A savepoint marks a point within the transaction to which part of the work can be undone.

Oracle provides statement-level atomicity and read consistency. Under the default READ COMMITTED isolation level, each query sees a consistent view of committed data as of that query's start. A reader generally does not block a writer, and a writer generally does not block a reader, though locks and resource contention still matter. SELECT FOR UPDATE requests row locks for workflows that must protect rows before changing them.

COMMIT makes transaction changes durable and releases transaction locks. ROLLBACK cancels uncommitted changes. DDL statements perform implicit commits, so keep schema changes separate from uncommitted business transactions. Never add a COMMIT to an application routine without understanding the transaction boundary owned by its caller.

Example transaction:

~~~sql
INSERT INTO departments (department_id, department_name)
VALUES (50, 'Research');

SAVEPOINT after_department;

INSERT INTO employees (employee_id, last_name, department_id)
VALUES (9001, 'Example', 50);

ROLLBACK TO after_department;
COMMIT;
~~~

The department row is committed; the employee insert is undone before the final commit. Use this pattern only in a disposable learning schema.

## 7. PL/SQL

PL/SQL is Oracle's procedural extension for server-side programs. An anonymous block has an optional declaration section, a required executable section, and an optional exception section. Stored procedures, functions, packages, and triggers use the same language with additional rules.

A PL/SQL program can reduce network round trips by sending a unit of work to the server. It can also make logic harder to test or deploy if business rules are scattered across triggers and packages. Keep interfaces deliberate, document transaction ownership, and make error handling meaningful.

A block can include:

- Variables, constants, records, and collection types.
- IF, CASE, LOOP, WHILE, and FOR control structures.
- Static SQL and parameterized dynamic SQL.
- Explicit or implicit cursors.
- Exceptions, including predefined and application-defined errors.
- Procedures, functions, packages, and triggers.

Prefer static SQL when the statement shape is known at compile time. Use bind variables in dynamic SQL for values. Object names cannot generally be supplied as bind variables, so validate any dynamic identifier against a strict allowlist. Bulk operations such as BULK COLLECT and FORALL can reduce PL/SQL-to-SQL context switching when used with appropriate memory limits and error handling.

## 8. JSON and newer application features

Oracle AI Database supports relational data and JSON capabilities in the same system. SQL/JSON functions can query, construct, and transform JSON values. A native JSON type, JSON collections, and JSON-relational duality views are version-sensitive features.

A JSON-relational duality view presents related relational rows as a JSON document while the relational tables remain the underlying stored data. Applications can use a document-shaped representation without creating a separate duplicated source of truth. The design still depends on keys, table relationships, view rules, permissions, and release-specific functionality.

Oracle AI Database 26ai includes AI Vector Search and Select AI capabilities. Vector search uses embeddings and vector indexes for semantic similarity workloads. Select AI can use natural-language interfaces with supported providers and configurations. These features require careful control of data access, model/provider configuration, latency, cost, and result validation. They are not substitutes for ordinary SQL, access control, or domain-specific correctness checks.

## 9. Application development

A connection pool reuses database sessions and helps control connection creation overhead. Configure pool size, timeouts, validation, session state, and transaction boundaries for the application workload. A pooled session can retain state between borrowers unless the driver or application resets it appropriately.

Use bind variables for values. They separate data from SQL syntax, reduce parsing work, and defend against SQL injection. Bind variables do not replace authorization checks and do not parameterize arbitrary table or column names.

Application code should handle database errors intentionally. Distinguish a retryable transient error from a constraint violation, invalid input, permission failure, or programming bug. Keep a request's related changes within a clear transaction and avoid committing each row independently unless that behavior is required.

## 10. Performance and diagnosis

The cost-based optimizer estimates the work of candidate plans using query structure, object metadata, and statistics. An index can reduce work for selective access, but it adds storage and write maintenance. More indexes are not automatically better.

A disciplined investigation is:

1. Capture the exact SQL, bind values or representative bind distributions, schema, and server release.
2. Check row counts, constraints, indexes, and optimizer statistics.
3. Inspect the plan and actual runtime row counts where permitted.
4. Find the step that performs unexpected work, such as a large scan, repeated lookup, expensive sort, or cardinality estimate error.
5. Change one relevant factor at a time and compare on representative data.
6. Confirm that the change preserves correct results and does not degrade other workloads.

Do not tune from a single elapsed-time measurement. Caching, concurrency, bind values, statistics, and client fetch behavior can all change observed performance. Avoid hints until the plan problem is understood and the hint has a documented reason.

## 11. Security

Oracle security combines authentication, authorization, object privileges, system privileges, roles, profiles, network controls, auditing, and optional encryption features. A user should have only the rights needed for their role. Prefer granting object privileges through carefully designed roles for interactive use, and understand the role rules that apply to stored code.

Use definer-rights and invoker-rights PL/SQL deliberately. Validate user input, bind values, restrict dynamic identifiers, avoid exposing detailed internal errors to untrusted callers, and protect credentials. Security options, default configurations, and license requirements vary by deployment.

## 12. Data movement, recovery, and availability

Logical data movement and physical recovery solve different problems:

- Data Pump exports and imports logical database objects and data.
- External tables and loading tools provide controlled access to files.
- RMAN protects and restores database files and can recover a database using backups and archived redo.
- Flashback features can recover selected data or objects within the available undo and retention configuration.
- Data Guard maintains standby databases for disaster recovery and availability scenarios.
- Oracle Real Application Clusters (RAC) allows multiple instances to work with a shared database, subject to platform and configuration requirements.
- GoldenGate provides replication and integration options with its own configuration and licensing considerations.

A backup is useful only if it can be restored. Define recovery objectives, protect backup copies, monitor jobs, and rehearse recovery. A replica is not a substitute for a backup because unwanted changes can be replicated too.

## 13. Quick reference patterns

A constrained table:

~~~sql
CREATE TABLE departments (
    department_id   NUMBER GENERATED BY DEFAULT AS IDENTITY,
    department_name VARCHAR2(100 CHAR) NOT NULL,
    active_flag     CHAR(1 CHAR) DEFAULT 'Y' NOT NULL,
    CONSTRAINT departments_pk PRIMARY KEY (department_id),
    CONSTRAINT departments_name_uq UNIQUE (department_name),
    CONSTRAINT departments_active_ck CHECK (active_flag IN ('Y', 'N'))
);
~~~

A predictable query with a bind variable:

~~~sql
SELECT department_id, department_name
FROM departments
WHERE active_flag = :active_flag
ORDER BY department_name, department_id
FETCH FIRST 20 ROWS ONLY;
~~~

An anonymous PL/SQL block:

~~~sql
BEGIN
    DBMS_OUTPUT.PUT_LINE('Oracle learning notes');
EXCEPTION
    WHEN OTHERS THEN
        RAISE;
END;
/
~~~

The slash on its own line is a client command used by SQL*Plus and SQLcl to submit the buffered PL/SQL block. It is not part of the PL/SQL language statement itself. In SQL Developer, execution behavior depends on whether you run a statement or a script.

## 14. Common mistakes to avoid

- Confusing a database service, an instance SID, a database, a CDB, and a PDB.
- Connecting an application to CDB$ROOT instead of the intended PDB service.
- Treating DATE as date-only when it also stores time through seconds.
- Comparing a value with NULL by using an equality operator.
- Assuming empty character strings are distinct from NULL in Oracle SQL.
- Forgetting that DDL can commit an open transaction.
- Using SELECT without a stable ordering when pagination or top-N behavior matters.
- Building SQL by concatenating untrusted values.
- Adding indexes without checking actual plans and write costs.
- Assuming a feature, option, or AI capability is available in every edition or deployment.
- Calling a dump file or standby database a complete backup strategy without restoration drills.
- Reporting a query as tuned based only on an estimated plan or a single timing.

## 15. Compact checklist

Before writing SQL, identify the target schema, expected rows, NULL behavior, and required order. Before changing data, verify the predicate and transaction boundary. Before publishing an API, use bind variables and least privilege. Before tuning, inspect representative execution evidence. Before an upgrade or recovery task, confirm version compatibility, backups, and a tested plan.

These notes are a learning guide, not an operational runbook for a production database. Follow the approved architecture, security controls, support policy, and recovery procedures for the environment being managed.