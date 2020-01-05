## Table of Contents
- [Procedures](#procedures)
- [Functions](#functions)
- [Triggers](#triggers)
- [Views](#views)
- [Sequences](#sequences)
- [Transactions](#transactions)

## Procedures
```sql
CREATE OR REPLACE PROCEDURE procedureName(arguments)
LANGUAGE plpgsql
AS $procedureName$

DECLARE
    variableOne VARCHAR(64);
DECLARE
    variableTwo VARCHAR(64);

BEGIN
    -- Query
END
$procedureName$;
```

## Functions
```sql
CREATE OR REPLACE FUNCTION functionName(arguments)
RETURNS [dataType]
LANGUAGE plpgsql
AS $functionName$

DECLARE
    variableOne VARCHAR(64);
DECLARE
    variableTwo VARCHAR(64);

BEGIN
    -- Query
END
$functionName$;
```

## Triggers
```sql
CREATE OR REPLACE FUNCTION triggerFunction()
RETURNS TRIGGER
LANGUAGE plpgsql
AS $triggerFunction$
-- Declarations
BEGIN
    -- Do Logic Here

    /*
     * OLD => Contém row com informações antigas.
     *        Podemos aceder a OLD.ColumnName
     * NEW => Contém row com informações novas.
     *        Podemos aceder a NEW.ColumnName
     */

    RETURN [OLD|NEW];
    /*
     * @return OLD => trigger é "cancelado",
     *                uma vez que retornamos a row com dados antigos.
     * @return NEW => trigger é "consumado",
     *                uma vez que retornamos a row com dados novos.
     */
END
$triggerFuntion$;
```
```sql
DROP TRIGGER IF EXISTS triggerName;

CREATE TRIGGER triggerName
    [BEFORE|AFTER|INSTEAD OF] [INSERT|DELETE|UPDATE|TRUNCATE]
    ON tableName
    FOR EACH ROW
    EXECUTE FUNCTION triggerFunction();
```

## Views
### Normal View
```sql
CREATE OR REPLACE VIEW viewName
AS
SELECT [*|columns]
FROM tableName
WHERE [condition];

SELECT * FROM viewName;
```
### Materialized View
```sql
CREATE OR REPLACE MATERIALIZED VIEW viewName
AS
SELECT [*|columns]
FROM tableName
WHERE [condition]
WITH [NO] DATA;


REFRESH MATERIALIZED VIEW viewName;
REFRESH MATERIALIZED VIEW CONCURRENTLY viewName;
SELECT * from viewName;
```

## Sequences
```sql
DROP SEQUENCE IF EXISTS sequenceName;

CREATE SEQUENCE sequenceName
    [AS [SMALLINT|INT|BIGINT]]
    INCREMENT [BY] 1
    [MINVALUE 1]
    [MAXVALUE 100]
    [START [WITH] 1];

INSERT INTO tableName (id, column1, ...)
VALUES (nextval(('sequenceName')), ...);
```

## Transactions
```sql
BEGIN TRANSACTION
    -- Do Logic Here
[COMMIT|ROLLBACK];
```