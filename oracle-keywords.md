# Oracle Database Keywords and Concepts

A categorized index for Oracle SQL and PL/SQL, using Oracle AI Database 26ai, Release 26, as the reference baseline. Oracle uses the words reserved, keyword, predefined identifier, built-in function, pseudo-column, data type, and client command for different things. Do not treat them as interchangeable.

## 1. How Oracle classifies words

### SQL reserved words

Oracle SQL reserved words have special parser meaning and cannot be used as ordinary unquoted identifiers. Quoted identifiers can sometimes use reserved words, but this is discouraged because it harms readability and can create compatibility problems. The SQL reference marks some words as ANSI reserved as well.

### SQL keywords

Oracle SQL keywords have special meaning in specific SQL contexts but are not necessarily reserved. Oracle warns that using them as object names can make statements harder to read and may lead to unpredictable results. The exact classification is available in the version's V$RESERVED_WORDS view. A word can have flags for always-reserved, context-specific, attribute, or other usage.

### PL/SQL reserved words and keywords

PL/SQL reserved words cannot be used as ordinary identifiers. PL/SQL keywords have special meaning but can technically be used as identifiers; avoid doing so. Some PL/SQL words also have SQL meaning. Quoted identifiers are possible in limited situations but are not a good naming strategy.

### Other Oracle terms

A built-in function, package name, data type, pseudo-column, SQL*Plus command, SQL clause, and object name are not automatically reserved words. For example, NVL is a SQL function, DBMS_OUTPUT is a package, DATE is a data type and a reserved word, ROWID is a pseudo-column and a reserved word, and DUAL is a table name. Classification depends on the language and release.

SQL and PL/SQL are case-insensitive for reserved words and keywords. Ordinary unquoted identifiers are normalized according to Oracle naming rules. Text literals and quoted identifiers are case-sensitive.

## 2. Oracle SQL reserved words

The following list is the Oracle SQL reserved-word list in the 26ai SQL Language Reference. An asterisk means Oracle also identifies the word as ANSI-reserved. COLUMN_VALUE and NESTED_TABLE_ID have special attribute-name notes. ROWID has special naming restrictions.

~~~text
ACCESS  ADD  ALL*  ALTER*  AND*  ANY*  AS*  ASC  AUDIT
BETWEEN*  BY*  CHAR*  CHECK*  CLUSTER  COLUMN*
COLUMN_VALUE  COMMENT  COMPRESS  CONNECT*  CREATE*  CURRENT*
DATE*  DECIMAL*  DEFAULT*  DELETE*  DESC  DISTINCT*
DROP*  ELSE*  EXCLUSIVE  EXISTS*  FILE  FLOAT*
FOR*  FROM*  GRANT*  GROUP*  HAVING*  IDENTIFIED  IMMEDIATE
IN*  INCREMENT  INDEX  INITIAL  INSERT*  INTEGER*
INTERSECT*  INTO*  IS*  LEVEL  LIKE*  LOCK  LONG
MAXEXTENTS  MINUS  MLSLABEL  MODE  MODIFY  NESTED_TABLE_ID
NOAUDIT  NOCOMPRESS  NOT*  NOWAIT  NULL*  NUMBER
OF*  OFFLINE  ON*  ONLINE  OPTION  OR*  ORDER*
PCTFREE  PRIOR  PUBLIC  RAW  RENAME  RESOURCE  REVOKE*
ROW*  ROWID  ROWNUM  ROWS*  SELECT*  SESSION  SET*
SHARE  SIZE  SMALLINT*  START*  SUCCESSFUL  SYNONYM  SYSDATE
TABLE*  THEN*  TO*  TRIGGER*  UID  UNION*  UNIQUE*
UPDATE*  USER*  VALIDATE  VALUES*  VARCHAR*  VARCHAR2
VIEW  WHENEVER*  WHERE*  WITH*
~~~

The SQL keyword catalog is broader than this reserved list. Do not use a remembered list from another database product as an Oracle classification. Query the exact server release when the distinction matters.

## 3. PL/SQL reserved words

These are the PL/SQL reserved words listed in the 26ai PL/SQL Language Reference. Some also have SQL meaning.

| Begins with | Reserved words |
|---|---|
| A | ALL, ALTER, AND, ANY, AS, ASC, AT |
| B | BEGIN, BETWEEN, BY |
| C | CASE, CHECK, CLUSTERS, CLUSTER, COLAUTH, COLUMNS, COMPRESS, CONNECT, CRASH, CREATE, CURSOR |
| D | DECLARE, DEFAULT, DESC, DISTINCT, DROP |
| E | ELSE, END, EXCEPTION, EXCLUSIVE |
| F | FETCH, FOR, FROM, FUNCTION |
| G | GOTO, GRANT, GROUP |
| H | HAVING |
| I | IDENTIFIED, IF, IN, INDEX, INDEXES, INSERT, INTERSECT, INTO, IS |
| L | LIKE, LOCK |
| M | MINUS, MODE |
| N | NOCOMPRESS, NOT, NOWAIT, NULL |
| O | OF, ON, OPTION, OR, ORDER, OVERLAPS |
| P | PROCEDURE, PUBLIC |
| R | RESOURCE, REVOKE |
| S | SELECT, SHARE, SIZE, SQL, START, SUBTYPE |
| T | TABAUTH, TABLE, THEN, TO, TYPE |
| U | UNION, UNIQUE, UPDATE |
| V | VALUES, VIEW, VIEWS |
| W | WHEN, WHERE, WITH |

## 4. PL/SQL keywords

PL/SQL keywords have special meaning but, unlike reserved words, Oracle permits them as identifiers. Avoid keyword identifiers anyway. This is the PL/SQL keyword list in the 26ai reference.

| Begins with | Keywords |
|---|---|
| A | A, ADD, ACCESSIBLE, AGENT, AGGREGATE, ARRAY, ATTRIBUTE, AUTHID, AVG |
| B | BFILE_BASE, BINARY, BLOB_BASE, BLOCK, BODY, BOTH, BOUND, BULK, BYTE |
| C | C, CALL, CALLING, CASCADE, CHAR, CHAR_BASE, CHARACTER, CHARSET, CHARSETFORM, CHARSETID, CLOB_BASE, CLONE, CLOSE, COLLECT, COMMENT, COMMIT, COMMITTED, COMPILED, CONSTANT, CONSTRUCTOR, CONTEXT, CONTINUE, CONVERT, COUNT, CREDENTIAL, CURRENT, CUSTOMDATUM |
| D | DANGLING, DATA, DATE, DATE_BASE, DAY, DEFINE, DELETE, DETERMINISTIC, DIRECTORY, DOUBLE, DURATION |
| E | ELEMENT, ELSIF, EMPTY, ESCAPE, EXCEPT, EXCEPTIONS, EXECUTE, EXISTS, EXIT, EXTERNAL |
| F | FINAL, FIRST, FIXED, FLOAT, FORALL, FORCE |
| G | GENERAL |
| H | HASH, HEAP, HIDDEN, HOUR |
| I | IMMEDIATE, IMMUTABLE, INCLUDING, INDICATOR, INDICES, INFINITE, INSTANTIABLE, INT, INTERFACE, INTERVAL, INVALIDATE, ISOLATION |
| J | JAVA |
| L | LANGUAGE, LARGE, LEADING, LENGTH, LEVEL, LIBRARY, LIKE2, LIKE4, LIKEC, LIMIT, LIMITED, LOCAL, LONG, LOOP |
| M | MAP, MAX, MAXLEN, MEMBER, MERGE, MIN, MINUTE, MOD, MODIFY, MONTH, MULTISET, MUTABLE |
| N | NAME, NAN, NATIONAL, NATIVE, NCHAR, NEW, NOCOPY, NUMBER_BASE |
| O | OBJECT, OCICOLL, OCIDATE, OCIDATETIME, OCIDURATION, OCIINTERVAL, OCILOBLOCATOR, OCINUMBER, OCIRAW, OCIREF, OCIREFCURSOR, OCIROWID, OCISTRING, OCITYPE, OLD, ONLY, OPAQUE, OPEN, OPERATOR, ORACLE, ORADATA, ORGANIZATION, ORLANY, ORLVARY, OTHERS, OUT, OVERRIDING |
| P | PACKAGE, PARALLEL_ENABLE, PARAMETER, PARAMETERS, PARENT, PARTITION, PASCAL, PERSISTABLE, PIPE, PIPELINED, PLUGGABLE, POLYMORPHIC, PRAGMA, PRECISION, PRIOR, PRIVATE |
| R | RAISE, RANGE, RAW, READ, RECORD, REF, REFERENCE, RELIES_ON, REM, REMAINDER, RENAME, RESULT, RESULT_CACHE, RETURN, RETURNING, REVERSE, ROLLBACK, ROW |
| S | SAMPLE, SAVE, SAVEPOINT, SB1, SB2, SB4, SECOND, SEGMENT, SELF, SEPARATE, SEQUENCE, SERIALIZABLE, SET, SHORT, SIZE_T, SOME, SPARSE, SQLCODE, SQLDATA, SQLNAME, SQLSTATE, STANDARD, STATIC, STDDEV, STORED, STRING, STRUCT, STYLE, SUBMULTISET, SUBPARTITION, SUBSTITUTABLE, SUM, SYNONYM |
| T | TDO, THE, TIME, TIMESTAMP, TIMEZONE_ABBR, TIMEZONE_HOUR, TIMEZONE_MINUTE, TIMEZONE_REGION, TRAILING, TRANSACTION, TRANSACTIONAL, TRUSTED |
| U | UB1, UB2, UB4, UNDER, UNPLUG, UNSIGNED, UNTRUSTED, USE, USING |
| V | VALIST, VALUE, VARIABLE, VARIANCE, VARRAY, VARYING, VOID |
| W | WHILE, WORK, WRAPPED, WRITE |
| Y | YEAR |
| Z | ZONE |

## 5. SQL statement words and clauses

### Query clauses

- SELECT chooses expressions and output columns.
- FROM identifies tables, views, inline views, and other row sources.
- JOIN combines row sources. Oracle supports ANSI join syntax and Oracle-specific legacy outer-join syntax; prefer explicit ANSI joins in new work.
- WHERE filters rows before grouping.
- GROUP BY forms groups for aggregate expressions.
- HAVING filters groups.
- ORDER BY orders the final result.
- FETCH FIRST or FETCH NEXT limits returned rows in supported releases.
- WITH defines common table expressions; recursive subquery factoring is version-sensitive.

### Data and schema statements

- SELECT reads rows.
- INSERT adds rows.
- UPDATE changes rows.
- DELETE removes rows.
- MERGE conditionally inserts, updates, and may delete rows according to its clauses.
- CREATE, ALTER, and DROP define, modify, or remove schema objects.
- GRANT and REVOKE assign or remove privileges.
- COMMIT and ROLLBACK complete or cancel transaction work.
- SAVEPOINT marks a rollback point within a transaction.

### Predicates and conditions

- Comparison: =, <>, !=, <, <=, >, >=
- Logical: AND, OR, NOT
- Membership: IN and NOT IN
- Ranges: BETWEEN and NOT BETWEEN
- Pattern matching: LIKE and ESCAPE; regular-expression conditions use REGEXP_LIKE
- Existence: EXISTS and NOT EXISTS
- Null checks: IS NULL and IS NOT NULL
- Row and document conditions: IS OF TYPE, IS JSON, and release-specific JSON conditions

A NULL comparison does not evaluate to TRUE. Use IS NULL rather than = NULL. Be careful with NOT IN when the subquery or list may contain NULL.

### Set and hierarchy terms

- UNION removes duplicate rows; UNION ALL preserves them.
- INTERSECT returns rows present in both query results.
- MINUS returns rows present in the first result but not the second.
- CONNECT BY and START WITH express Oracle hierarchical queries.
- PRIOR refers to a parent-row expression in a hierarchical query.
- LEVEL reports the depth of a row in a hierarchical query.
- Recursive WITH is an alternative for some tree and graph-like traversals.

## 6. Data types and type-related terms

| Type or term | Meaning |
|---|---|
| NUMBER | Decimal numeric values with optional precision and scale |
| BINARY_FLOAT, BINARY_DOUBLE | Binary floating-point types |
| VARCHAR2 | Variable-length character data |
| CHAR | Fixed-length character data |
| NCHAR, NVARCHAR2 | National character set types |
| DATE | Date and time through seconds, without a time-zone offset |
| TIMESTAMP | Date and time with fractional seconds |
| TIMESTAMP WITH TIME ZONE | Timestamp that carries time-zone information |
| TIMESTAMP WITH LOCAL TIME ZONE | Timestamp normalized for storage and presented in the session time zone |
| INTERVAL YEAR TO MONTH, INTERVAL DAY TO SECOND | Duration types |
| RAW | Small binary values |
| BLOB | Large binary object |
| CLOB, NCLOB | Large character objects |
| BFILE | External binary file locator |
| JSON | Native JSON data type in supported Oracle AI Database releases, including 26ai |

Type conversions can be implicit or explicit. Prefer explicit conversion functions such as CAST, TO_CHAR, TO_DATE, and TO_TIMESTAMP when the expected format and type need to be clear. Avoid relying on session NLS settings for application input and output.

## 7. SQL functions and expressions

These are built-ins or expression forms, not a list of reserved words.

| Family | Examples |
|---|---|
| Numeric | ABS, CEIL, FLOOR, MOD, POWER, ROUND, TRUNC |
| Character | CONCAT, INSTR, LENGTH, LOWER, LPAD, LTRIM, REPLACE, RPAD, RTRIM, SUBSTR, TRIM, UPPER |
| Null and conditional | CASE, COALESCE, DECODE, NVL, NVL2, NULLIF |
| Conversion and formatting | CAST, TO_CHAR, TO_DATE, TO_NUMBER, TO_TIMESTAMP |
| Date and time | ADD_MONTHS, CURRENT_DATE, CURRENT_TIMESTAMP, EXTRACT, LAST_DAY, MONTHS_BETWEEN, SYSTIMESTAMP, SYSDATE |
| Aggregate | AVG, COUNT, LISTAGG, MAX, MIN, SUM |
| Analytic | DENSE_RANK, FIRST_VALUE, LAG, LAST_VALUE, LEAD, RANK, ROW_NUMBER |
| JSON | JSON_ARRAY, JSON_ARRAYAGG, JSON_EXISTS, JSON_OBJECT, JSON_OBJECTAGG, JSON_QUERY, JSON_SERIALIZE, JSON_TABLE, JSON_VALUE |
| AI and vector | VECTOR_DISTANCE and vector indexing or embedding operations, subject to release and configuration |

Check function signatures, return types, collation behavior, null behavior, and release support in the target server's SQL reference.

## 8. Pseudo-columns and special values

A pseudo-column behaves like a column in some SQL expressions but is not an ordinary stored table column.

- ROWID identifies a row's physical location in many heap-table contexts; it is not a durable business key.
- ROWNUM numbers rows as Oracle selects them and is not the same as ROW_NUMBER().
- LEVEL reports hierarchical-query depth.
- CONNECT_BY_ISLEAF and CONNECT_BY_ISCYCLE provide hierarchical-query information.
- ORA_ROWSCN exposes a system change number at a configured granularity; it is not a general-purpose exact audit timestamp.
- Sequence_name.NEXTVAL and sequence_name.CURRVAL return sequence values under their usage rules.
- SYSDATE and SYSTIMESTAMP return system date-time values; they are functions, not values to hard-code into an application.

USER, CURRENT_USER, SESSION_USER, and SYS_CONTEXT are context functions or expressions. They are not substitutes for authorization checks.

## 9. PL/SQL syntax and language elements

| Term | Purpose |
|---|---|
| DECLARE | Starts the optional declaration section of an anonymous block |
| BEGIN | Starts the executable section |
| EXCEPTION | Starts the optional exception-handling section |
| END | Ends a block or compound construct |
| IF, ELSIF, ELSE | Conditional execution |
| CASE | Conditional expression or statement |
| LOOP, WHILE, FOR | Iteration |
| EXIT, CONTINUE | Leave or skip an iteration |
| RETURN | Return from a function or exit a procedure |
| RAISE | Raise an exception |
| PRAGMA | Compiler directive such as EXCEPTION_INIT |
| %TYPE | Derive a declaration type from a table column or variable |
| %ROWTYPE | Derive a record type from a table row or cursor |
| BULK COLLECT | Fetch many rows into collections |
| FORALL | Send collection-driven DML efficiently to SQL |
| EXECUTE IMMEDIATE | Execute dynamic SQL or PL/SQL |
| AUTHID DEFINER, AUTHID CURRENT_USER | Select stored-program rights model |

Common declaration types and constructs include BOOLEAN, NUMBER, VARCHAR2, RECORD, associative arrays, nested tables, VARRAYs, cursors, constants, exceptions, and subtypes. SQL and PL/SQL data type capabilities are related but not identical in every release or context.

## 10. Built-in packages and predefined identifiers

Packages organize procedures, functions, types, and state. They are APIs, not language keywords.

- DBMS_OUTPUT writes diagnostic text for an enabled client.
- DBMS_LOB provides LOB operations.
- DBMS_SQL supports dynamic SQL with runtime-defined statement shapes.
- DBMS_METADATA retrieves object metadata.
- DBMS_SCHEDULER manages scheduled jobs.
- DBMS_STATS manages optimizer statistics.
- DBMS_XPLAN formats execution plan information.
- UTL_FILE accesses server-side files subject to directory objects and privileges.
- STANDARD declares many predefined PL/SQL types, functions, and exceptions.
- SQLCODE and SQLERRM report information about the current exception.
- SQL%ROWCOUNT, SQL%FOUND, and SQL%NOTFOUND are implicit cursor attributes.
- SQLCODE, SQLERRM, and cursor attributes are not reserved words merely because PL/SQL gives them a predefined meaning.

Use only the package APIs needed for a task. Many packages require privileges or have security and operational implications.

## 11. Dictionary and performance views

Oracle exposes metadata at different visibility levels:

- USER_OBJECTS and USER_TABLES show objects owned by the current user.
- ALL_OBJECTS and ALL_TABLES show objects accessible to the current user.
- DBA_OBJECTS and DBA_TABLES provide database-wide metadata and require elevated access.
- USER_TAB_COLUMNS, ALL_TAB_COLUMNS, and DBA_TAB_COLUMNS describe columns at their respective visibility levels.
- USER_CONSTRAINTS and USER_CONS_COLUMNS describe constraints.
- USER_INDEXES and USER_IND_COLUMNS describe indexes.
- V$ views expose dynamic performance information.
- CDB_ views expose multitenant metadata, subject to container and privilege rules.
- V$RESERVED_WORDS reports SQL token classification for the current server version.

A diagnostic query for reserved-word metadata:

~~~sql
SELECT keyword, reserved, res_type, res_attr, res_semi
FROM v$reserved_words
ORDER BY keyword;
~~~

Access to dynamic performance and DBA views is privilege-controlled. Do not grant broad dictionary access merely to make a learning query run.

## 12. Client commands are separate from SQL

SQL*Plus and SQLcl provide commands that control the client or script runner. Examples include CONNECT, DESCRIBE, SET SERVEROUTPUT ON, SPOOL, and RUN. A client command may not be valid when sent through JDBC or copied into a SQL worksheet as if it were a server SQL statement. Client behavior can also vary by tool.

A semicolon terminates many SQL statements in these clients. A slash on a line by itself submits a PL/SQL block held in the client buffer. The slash is a client command, not a PL/SQL token.

## 13. Naming and practical guidance

- Use clear, stable names for tables, columns, constraints, indexes, procedures, and packages.
- Avoid SQL reserved words, PL/SQL reserved words, and terms that are likely to become confusing keywords.
- Avoid quoted identifiers for routine application objects because they create case-sensitive naming rules.
- Avoid the SYS_ prefix for user-created objects because Oracle uses it for generated names.
- Use bind variables for values and a strict allowlist for dynamic object names.
- Use explicit schema qualification where it improves clarity and avoids name resolution surprises.
- Check object names and word classifications against the database release actually used by the application.
- Do not confuse SQL syntax with client commands, functions, types, packages, pseudo-columns, or data dictionary names.

This catalog distinguishes the main Oracle vocabulary families and includes the SQL and PL/SQL reserved and keyword lists for the stated baseline. Built-in functions, packages, dictionary views, and product features continue to evolve; use the installed release's reference and metadata when exact current availability matters.