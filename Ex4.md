# Ex No: 4 - Implicit & Explicit Cursors

## Implicit Cursors

```sql
DECLARE
    total_rows NUMBER(2);
BEGIN
    UPDATE customers
    SET salary = salary + 500;

    IF SQL%NOTFOUND THEN
        DBMS_OUTPUT.PUT_LINE('no customers selected');
    ELSIF SQL%FOUND THEN
        total_rows := SQL%ROWCOUNT;
        DBMS_OUTPUT.PUT_LINE(total_rows || ' customers selected');
    END IF;
END;
/
```

**Output:**
```
6 customers selected
PL/SQL procedure successfully completed.
```

## Explicit Cursors

```sql
DECLARE
    c_id   customers.id%TYPE;
    c_name customers.name%TYPE;
    c_addr customers.address%TYPE;
    CURSOR c_customers IS
        SELECT id, name, address FROM customers;
BEGIN
    OPEN c_customers;
    LOOP
        FETCH c_customers INTO c_id, c_name, c_addr;
        EXIT WHEN c_customers%NOTFOUND;
        DBMS_OUTPUT.PUT_LINE(c_id || ' ' || c_name || ' ' || c_addr);
    END LOOP;
    CLOSE c_customers;
END;
/
```

**Output:**

| ID | NAME     | ADDRESS    |
|----|----------|------------|
| 1  | Ramesh   | Ahmadabad  |
| 2  | Khilan   | Delhi      |
| 3  | Kaushik  | Kota       |
| 4  | Chaitali | Mumbai     |
