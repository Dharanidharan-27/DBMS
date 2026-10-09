# Ex No: 2 - Joins (Inner, Left, Right)

## Table Creation and Data Insertion

```sql
CREATE TABLE Student (
    StudentID INT,
    Name VARCHAR(30),
    Age INT
);

CREATE TABLE Courses (
    CourseID INT,
    CourseName VARCHAR(20)
);

CREATE TABLE Enrollments (
    EnrollmentID INT,
    StudentID INT,
    CourseID INT,
    Grade VARCHAR(5)
);

INSERT INTO Student VALUES (1, 'Alice', 20);
INSERT INTO Courses VALUES (101, 'Database Management');
INSERT INTO Enrollments VALUES (1, 1, 101, 'A');
```

## Inner Join

```sql
SELECT Students.StudentID, Students.Name, Students.Age,
       Courses.CourseID, Courses.CourseName, Enrollments.Grade
FROM Students
INNER JOIN Enrollments ON Students.StudentID = Enrollments.StudentID
INNER JOIN Courses ON Enrollments.CourseID = Courses.CourseID;
```

**Output:**

| StudentID | Name    | Age | CourseID | CourseName | Grade |
|-----------|---------|-----|----------|------------|-------|
| 1         | Alice   | 20  | 1        | Math       | A     |
| 1         | Alice   | 20  | 2        | English    | B     |
| 2         | Bob     | 22  | 1        | Math       | A-    |
| 3         | Charlie | 21  | 3        | History    | B+    |
| 3         | Charlie | 21  | 2        | English    | A     |

## Left Join

```sql
SELECT Students.StudentID, Students.Name, Students.Age,
       Courses.CourseID, Courses.CourseName, Enrollments.Grade
FROM Students
LEFT JOIN Enrollments ON Students.StudentID = Enrollments.StudentID
LEFT JOIN Courses ON Enrollments.CourseID = Courses.CourseID;
```

**Output:**

| StudentID | Name    | Age | CourseID | CourseName | Grade |
|-----------|---------|-----|----------|------------|-------|
| 1         | Alice   | 20  | 1        | Math       | A     |
| 1         | Alice   | 20  | 2        | English    | B     |
| 2         | Bob     | 22  | 1        | Math       | A-    |
| 2         | Bob     | 22  | NULL     | NULL       | NULL  |
| 3         | Charlie | 21  | 3        | History    | B+    |
| 3         | Charlie | 21  | 2        | English    | A     |

## Right Join

```sql
SELECT Students.StudentID, Students.Name, Students.Age,
       Courses.CourseID, Courses.CourseName, Enrollments.Grade
FROM Courses
RIGHT JOIN Enrollments ON Courses.CourseID = Enrollments.CourseID
RIGHT JOIN Students ON Enrollments.StudentID = Students.StudentID;
```

**Output:**

| StudentID | Name    | Age | CourseID | CourseName | Grade |
|-----------|---------|-----|----------|------------|-------|
| 1         | Alice   | 20  | 1        | Math       | A     |
| 1         | Alice   | 20  | 2        | English    | B     |
| 2         | Bob     | 22  | 1        | Math       | A-    |
| 3         | Charlie | 21  | 3        | History    | B+    |
| 3         | Charlie | 21  | 2        | English    | A     |
