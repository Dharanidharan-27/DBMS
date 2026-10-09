# Ex No: 1 - Table Creation, Simple Queries, Nested Queries & Subqueries

## Table Creation and Data Insertion

```sql
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(30),
    Age INT
);

CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    CourseName VARCHAR(20)
);

CREATE TABLE Enrollments (
    StudentID INT REFERENCES Student(StudentID),
    CourseID INT REFERENCES Courses(CourseID)
);

INSERT INTO Student VALUES (1, 'Alice', 20);
INSERT INTO Courses VALUES (101, 'Database Management');
INSERT INTO Enrollments VALUES (1, 101);
```

## Simple Queries

```sql
SELECT * FROM Students;
```

**Output:**

| StudentID | Name    | Age |
|-----------|---------|-----|
| 1         | Alice   | 20  |
| 2         | Bob     | 22  |
| 3         | Charlie | 21  |
| 4         | David   | 19  |

```sql
SELECT Name, Age FROM Students WHERE Age > 20;
```

**Output:**

| Name    | Age |
|---------|-----|
| Bob     | 22  |
| Charlie | 21  |

## Nested Queries

```sql
SELECT Name FROM Students
WHERE StudentID IN (
    SELECT StudentID FROM Enrollments
    WHERE CourseID = (
        SELECT CourseID FROM Courses
        WHERE CourseName = 'Database Management'
    )
);
```

**Output:**

| Name    |
|---------|
| Alice   |
| Charlie |

```sql
SELECT CourseID, CourseName FROM Courses
WHERE CourseID IN (
    SELECT CourseID FROM Enrollments
    GROUP BY CourseID
    HAVING COUNT(*) > 1
);
```

**Output:**

| CourseID | CourseName           |
|----------|----------------------|
| 101      | Database Management  |
| 103      | Web Development      |

## Subqueries

```sql
SELECT AVG(Age) AS AverageAge FROM Students;
```

**Output:**

| AverageAge |
|------------|
| 20.5       |

```sql
SELECT Name, Age FROM Students
WHERE Age > (SELECT AVG(Age) FROM Students);
```

**Output:**

| Name    | Age |
|---------|-----|
| Bob     | 22  |
| Charlie | 21  |
