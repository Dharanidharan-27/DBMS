# Ex No: 6 - Triggers (Update, Delete, Insert)

## Trigger for Update

```sql
CREATE OR REPLACE TRIGGER up_classd
BEFORE UPDATE ON customer
FOR EACH ROW
DECLARE
BEGIN
    IF UPDATING THEN
        DBMS_OUTPUT.PUT_LINE('new value is ' || :NEW.stotal);
        DBMS_OUTPUT.PUT_LINE('old value is ' || :OLD.stotal);
    END IF;
END;
/
```

**Output:**
```
new value is 500
old value is 300
```

## Trigger for Deletion

```sql
CREATE OR REPLACE TRIGGER del_classb
BEFORE DELETE ON customer
FOR EACH ROW
DECLARE
BEGIN
    IF DELETING THEN
        DBMS_OUTPUT.PUT_LINE('row deleted');
    END IF;
END;
/
```

**Output:**
```
row deleted
1 row deleted.
```

## Trigger for Insertion

```sql
CREATE OR REPLACE TRIGGER ins_classb
BEFORE INSERT ON classb
FOR EACH ROW
DECLARE
    InvTot EXCEPTION;
BEGIN
    IF INSERTING THEN
        IF :NEW.stotal > 1000 THEN
            RAISE InvTot;
        END IF;
    END IF;
EXCEPTION
    WHEN InvTot THEN
        RAISE_APPLICATION_ERROR(-20000, 'Total not valid');
END;
/
```

**Output (on invalid insert):**
```
insert into classb values('6','jana','it','20000','a')
ERROR at line 1:
ORA-20000: Total not valid
ORA-06512: at "SCOTT.INS_CLASSB", line 11
ORA-04088: error during execution of trigger 'SCOTT.INS_CLASSB'
```
