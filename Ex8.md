# Ex No: 8 - Pre-defined & User-defined Exceptions

## Pre-defined Exceptions

```sql
DECLARE
    c_id   customer.id%TYPE := 5;
    c_name customer.name%TYPE;
    c_addr customer.address%TYPE;
BEGIN
    SELECT name, address
    INTO c_name, c_addr
    FROM customer
    WHERE id = c_id;

    DBMS_OUTPUT.PUT_LINE('name: ' || c_name);
    DBMS_OUTPUT.PUT_LINE('address: ' || c_addr);
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('no such customer!');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('error!');
END;
/
```

**Output:**
```
SQL> SET SERVEROUTPUT ON;
SQL> /
no such customer!
PL/SQL procedure successfully completed.
```

## User-defined Exceptions

```sql
DECLARE
    c_id   customers.id%TYPE := &cc_id;
    c_name customers.name%TYPE;
    c_addr customers.address%TYPE;
    ex_invalid_id EXCEPTION;
BEGIN
    IF c_id <= 0 THEN
        RAISE ex_invalid_id;
    ELSE
        SELECT name, address
        INTO c_name, c_addr
        FROM customers
        WHERE id = c_id;

        DBMS_OUTPUT.PUT_LINE('Name: ' || c_name);
        DBMS_OUTPUT.PUT_LINE('Address: ' || c_addr);
    END IF;
EXCEPTION
    WHEN ex_invalid_id THEN
        DBMS_OUTPUT.PUT_LINE('ID must be greater than zero!');
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No such customer!');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error!');
END;
/
```

**Output (invalid ID):**
```
Enter value for cc_id: -6
ID must be greater than zero!
PL/SQL procedure successfully completed.
```

**Output (valid customer ID):**
```
Enter value for cc_id: 1
Name: <customer name>
Address: <customer address>
PL/SQL procedure successfully completed.
```
