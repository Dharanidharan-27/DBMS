# Ex No: 5 - Procedures & Functions

## Procedure

```sql
SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE Sum (a IN NUMBER, b IN NUMBER) IS
    c NUMBER;
BEGIN
    c := a + b;
    DBMS_OUTPUT.PUT_LINE('Sum of two nos = ' || c);
END Sum;
/
```

**Output:**
```
Enter value for x: 10
Enter value for y: 20
Sum of two nos = 30
PL/SQL procedure successfully created.
```

## Function

```sql
SET SERVEROUTPUT ON;

CREATE OR REPLACE FUNCTION Sum (a IN NUMBER, b IN NUMBER)
RETURN NUMBER IS
    c NUMBER;
BEGIN
    c := a + b;
    RETURN c;
END;
/
```

**Output:**
```
Enter value for no1: 5
Enter value for no2: 5
Sum of two nos = 10
PL/SQL procedure successfully created.
```
