Database normalisation is the process of structuring a relational database to reduce redundancy  and improve data integrity.

A. **First Normal Form (1NF) - Remove Repeating Groups**
	-- Each column should contain atomic indivisible 
	-- Each row should be unique
	
**Unnormalized Table (UNF):**

|StudentID|StudentName|Courses|
|---|---|---|
|1|Alice|Math, Physics|
|2|Bob|Chemistry, Math|

**1NF:**

|StudentID|StudentName|Course|
|---|---|---|
|1|Alice|Math|
|1|Alice|Physics|
|2|Bob|Chemistry|
|2|Bob|Math|

B. **Second Normal Form (2NF) - Remove Partial Dependency**
Should be in 1NF
	-- Non-key attributes depend on the whole primary key (also if pk is composite).
	-- No non-key column should depend on only part of a composite key.
	**1NF Table:**

| StudentID | CourseID | StudentName | CourseName |
| --------- | -------- | ----------- | ---------- |
| 1         | 101      | Alice       | Math       |
| 1         | 102      | Alice       | Physics    |
| 2         | 101      | Bob         | Math       |
see here studentName only depends on studentid and courseName on courseId
so this should be split into more tables as shown below:
**Students Table:**

|StudentID|StudentName|
|---|---|
|1|Alice|
|2|Bob|

**Courses Table:**

|CourseID|CourseName|
|---|---|
|101|Math|
|102|Physics|

**Enrollment Table:**

|StudentID|CourseID|
|---|---|
|1|101|
|1|102|
|2|101|
C. **Third Normal Form (3NF) - Remove transitive Dependency**
	-- Non-key attributes depend only on the primary key, not on other non-key attributes.
	-- No transitive dependency (A->B->C)


**2NF Table:**

| StudentID | DeptID | DeptName |
| --------- | ------ | -------- |
| 1         | D1     | Science  |
| 2         | D2     | Arts     |
Here if you see DeptName depends directly on DeptId
**3NF Solution:**

**Students Table:**

|StudentID|DeptID|
|---|---|
|1|D1|
|2|D2|

**Departments Table:**

| DeptID | DeptName |
| ------ | -------- |
| D1     | Science  |
| D2     | Arts     |