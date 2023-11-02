# 数据定义

```sql
CREATE DATABASE test;
CREATE LOGIN user1 WITH PASSWORD='123456',DEFAULT_DATABASE=test; -- 创建用户,并指定默认数据库,密码
CREATE USER user1 FOR LOGIN user1; -- 为用户指定登录名
```

```sql
CREATE SCHEMA 模式名 AUTHORIZATION 用户名
-- 
CREATE SCHEMA "S-T" AUTHORIZATION wang
```



### 创建表+插入数据操作

```SQL
-- 创建表
CREATE TABLE table_name
(
  column1 datatype constraints,
  column2 datatype constraints,
  ...
);
-- CREATE TABLE 用于创建表。表名（table_name）指定要创建的表的名称。在括号中，每一行代表表的一个列。每个列由列名（column1）、数据类型（datatype），以及约束（constraints）组成。约束包括主键约束（PRIMARY KEY）、非空约束（NOT NULL）和外键约束（FOREIGN KEY）等。

-- 向表中插入数据操作
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);

```

### 修改基本表操作

修改基本表通常包括添加、删除、更新列或更改列的数据类型等操作。以下是一些常见的修改基本表的操作：

**添加列**：

```sql
ALTER TABLE table_name
ADD new_column_name data_type;
```

例如，要向名为 "Employees" 的表中添加一个 "Email" 列，可以执行以下命令：
```sql
ALTER TABLE Employees
ADD Email VARCHAR(100);
```

**删除列**：
```sql
ALTER TABLE table_name
DROP column_name;
```

例如，要从名为 "Customers" 的表中删除 "Phone" 列，可以执行以下命令：
```sql
ALTER TABLE Customers
DROP Phone;
```

**更改列的数据类型**：
```sql
ALTER TABLE table_name
ALTER COLUMN column_name new_data_type;
```

例如，要将 "Salary" 列的数据类型从 INT 更改为 DECIMAL，可以执行以下命令：
```sql
ALTER TABLE Employees
ALTER COLUMN Salary DECIMAL(10, 2);
```

**更改列名**：
```sql
EXEC sp_rename 'table_name.old_column_name', 'new_column_name', 'COLUMN';
```

例如，要将 "Address" 列的名称更改为 "StreetAddress"，可以执行以下命令：
```sql
EXEC sp_rename 'Customers.Address', 'StreetAddress', 'COLUMN';
```

**删除表**：
```sql
DROP TABLE table_name;
```

谨慎使用，因为这将删除整个表及其数据。执行前请确保你的数据已备份。

**重命名表**：
```sql
EXEC sp_rename 'old_table_name', 'new_table_name';
```

例如，要将名为 "Products" 的表更名为 "Inventory"，可以执行以下命令：
```sql
EXEC sp_rename 'Products', 'Inventory';
```

**约束的添加和删除**：
你可以使用 `ALTER TABLE` 命令添加和删除表的约束，如主键、外键和唯一约束

```sql
-- 主键
ALTER TABLE table_name
ADD CONSTRAINT PK_TableName PRIMARY KEY (column_name);
-- 外键
ALTER TABLE table_name
ADD CONSTRAINT FK_TableName FOREIGN KEY (column_name)
REFERENCES reference_table (reference_column);
-- 删除主键
ALTER TABLE table_name
DROP CONSTRAINT PK_TableName;

```

### 索引的建立与删除

1. 每个表**只能有一个聚簇索引**，并且通常选择一个具有唯一性的列作为聚簇索引的键。
2. 多列索引对于满足多列条件的查询（按多个条件进行过滤）非常有用

```sql
-- 有聚簇索引和非聚簇索引之分；也有唯一索引与非唯一索引之分
-- 建立单列唯一索引
CREATE UNIQUE  INDEX 索引名 ON table_name (column_name);
-- 建立多列唯一索引
CREATE UNIQUE  INDEX 索引名 ON table_name (column1, column2);
-- 建立单列聚簇唯一索引
CREATE UNIQUE CLUSTER INDEX index_name ON table_name (column_name); -- CLUSTER 表示聚簇索引
-- 每个列名后面可以跟ASC/DESC（升序/降序）制定排列次序，默认是升序

-- 修改
ALTER INDEX 旧索引名 RENAME TO 新索引名;
-- 删除
DROP INDEX 索引名
-- 检索指定表的索引信息
EXEC sp_helpindex 表名 ;
```

# 数据查询

## SELECT语句

```sql
SELECT ALL|DISTINCT 目标列表达式 -- 目标列表达式可以是算术式也可以是字符串、函数等
INTO 表名
FROM 表名或视图名
WHERE condition
GROUP BY 列名1 HAVING 条件表达式
ORDER BY 列名2 ASC|DESC ;
-- 根据WHERE子句的条件表达式从FROM子句指定的基本表、视图或派生表中找出满足条件的元组，再按SELECT子句中的目标列表达式选出元组中的属性值形成结果表
-- 若有GROUP BY 子句，则将结果按照 列1 的值进行分组；若带HAVING，只有满足指定条件的组才可以输出。带ORDER，结果还要按照 列2 的值升序或降序排序 ASC是升序 DESC 是降序
-- INTO 表示把查询的结果放入新的表中
```

```sql
-- 通过以下操作，可实现创建一个结构和student相同，但没有所含数据的新表
SELECT *
INTO new_table
FROM student
where 3>6;
```

## 单表查询

### GROUP BY子句

`GROUP BY` 子句是 SQL 查询中用于**对结果集进行分组**的重要部分。它允许你按照一个或多个列的值对结果集进行分组，并且通常与聚合函数一起使用，以对每个分组执行聚合操作，如计数、求和、平均值等。

基本的 `GROUP BY` 子句的语法如下：

```sql
SELECT column1, column2, aggregate_function(column3)
FROM table
GROUP BY column1, column2;
```

以下是关于 `GROUP BY` 子句的一些关键概念：

1. **分组列（Grouping Columns）：** 在 `GROUP BY` 子句中列出的列将用于分组。结果集中的数据将按照这些列中的唯一值进行分组。

2. **聚合函数（Aggregate Functions）：** 通常与 `GROUP BY` 一起使用的聚合函数包括 `COUNT`、`SUM`、`AVG`、`MAX`、`MIN` 等。这些函数对每个分组执行计算，生成一个值作为每个分组的汇总。

下面是一个示例，假设你有一个学生成绩表 `scores`，并想按照学生所在的班级分组，并计算每个班级的平均分数：

```sql
SELECT class, AVG(score) as avg_score
FROM scores
GROUP BY class;
```

上述查询会将结果按班级分组，并计算每个班级的平均分数。

注意：

- `GROUP BY` 子句中的列通常**必须是 `SELECT` 子句中列出的列**，或者是可以从这些列派生的表达式。
- `HAVING` 子句可用于对分组应用筛选条件，类似于 `WHERE` 子句用于对单行应用筛选条件。

### `*`的使用

```sql
SELECT COUNT(*)
FROM student;

-- 查询这个表的总行数
```

### TOP关键词

```sql
-- 在 SQL Server ，可以使用 TOP 关键词来限制返回的行数，如下所示：
SELECT TOP 10 *
FROM TableName;
-- 这将返回表 TableName 中的前 10 行。
```

```sql
-- 查询选修C1课程的成绩最高的学生的学号与成绩
SELECT TOP 1 WITH TIES Sno, Grade -- WITH TISE -> 返回所有具有相同排序列值的行。如果有多名学生获得相同的最高成绩，也会将它们全部列出。仅对TOP 1 有用
FROM SC
WHERE cno = '1'
ORDER BY Grade DESC;

-- 或者
SELECT Sno, Grade
FROM SC
WHERE cno = '1' AND Grade = (SELECT MAX(Grade) FROM SC WHERE cno = '1');
```

### `LIKE`使用

`LIKE` 是 SQL 查询中的一个操作符，用于在**字符串**字段中进行模糊**匹配**。它通常与通配符结合使用，以搜索与指定模式匹配的文本。

```sql
SELECT column1, column2, ...
FROM table_name
WHERE column LIKE pattern;
```

#### 通配符：

1. `%`：代表零个、一个或多个字符。在模糊搜索中，它可以匹配任何字符或字符序列。

   - 例如，`'a%'` 匹配以字母 'a' 开头的任何值。

   - `'%or'` 匹配以字母 'or' 结尾的任何值。

   - `'%or%'` 匹配任何位置包含字母序列 'or' 的任何值。

     ```sql
     -- 查询姓张且名字中有%的同学
     SELECT sname,sno,sdept
     FROM student
     WHERE sname LIKE '张%[%]%'
     ```

     

2. `_`：代表**单一字符**。（<u>注意NCHAR类型，它中的一个字符有两个字节产生。用NCHAR时必须用空格补齐后面的空位</u>）它用于匹配单个字符，而不是一个字符序列。

   - 例如，`'_r%'` 匹配以 'r' 作为第二个字符的任何值。

     ```sql
     -- 查询姓氏为张的两字同学(姓名用 char[6]存放)
     SELECT *
     FROM student
     WHERE name LIKE '张_';
     -- 查询姓氏为张的两字同学(姓名用 nchar[6]存放)
     ```

     

3. `[]`：用于匹配**括号内任何**单个字符。

   - 例如，`'[aeiou]'` 匹配任何元音字母。
   - `'[0-9]'` 匹配任何数字。
   - `'[A-Z]'` 匹配任何大写字母。

4. `[^]`：用于排除指定字符之外的任何字符。

   - 例如，`'[^0-9]'` 匹配不是数字的任何字符。

1. 

```sql
SELECT *
FROM student
WHERE LEN(name) = 3;
-- 查询三字姓名的同学
```

### IN与NOT IN

- `IN` 运算符用于筛选列中的值是否包含在指定的值集合内。
- `NOT IN` 运算符用于筛选列中的值是否不包含在指定的值集合内。

```sql
-- 使用 IN 运算符
SELECT column1, column2
FROM table
WHERE column3 IN (value1, value2, value3);

-- 使用 NOT IN 运算符
SELECT column1, column2
FROM table
WHERE column3 NOT IN (value1, value2, value3);
```

```sql
SELECT Sname, Sno
FROM SC
WHERE Sno IN ('1', '2', '3');
```

### 聚集函数

<u>WHERE子句中不允许使用聚集函数</u>

聚集函数是 SQL 中用于对数据集执行聚合操作的函数。这些函数将多个行的值合并成一个单一的值，并常用于统计或计算数据的总和、平均值、计数等。

以下是一些常见的 SQL 聚集函数：

1. **COUNT()**: 用于计算数据行的数量。可以用于表格中任何列或者用 `*` 表示计算所有行的数量。

    ```sql
    SELECT COUNT(*) FROM employees;
    ```

2. **SUM()**: 用于计算数值列的总和。

    ```sql
    SELECT SUM(salary) FROM employees;
    ```

3. **AVG()**: 用于计算数值列的平均值。

    ```sql
    SELECT AVG(age) FROM students;
    ```

4. **MIN()**: 用于找到数值列中的最小值。

    ```sql
    SELECT MIN(price) FROM products;
    ```

5. **MAX()**: 用于找到数值列中的最大值。

    ```sql
    SELECT MAX(score) FROM exam_results;
    ```

这些聚集函数**通常与 SQL 的 `GROUP BY` 子句结合使用**，以便对数据进行**分组和聚合操作**。例如，你可以使用 `GROUP BY` 按部门对员工的工资进行总和计算：

```sql
SELECT department, SUM(salary)
FROM employees
GROUP BY department;
```

这将返回每个部门的总工资。

```sql
-- 查询有多少学生选课了
SELECT COUNT(DISTINCT sno) -- DISTINCT 是 SQL 查询中用于去除结果集中重复行的关键字。
FROM SC
```

```sql
SELECT cno , COUNT(*) 人数
FROM SC
GROUP BY cno
ORDER BY 人数;
-- 
SELECT cno , COUNT(*) 人数
FROM SC
GROUP BY cno  HAVING COUNT(*) = 6
-- 
SELECT sno , AVG(grade) 平均成绩
FROM SC 
GROUP BY sno
HAVING AVG(grade) >= 80;
-- 
SELECT *
FROM SC
WHERE grade BETWEEN 80 AND 90;
```

## 多表查询

### 外连接

最常见的包括 **INNER JOIN**、**LEFT JOIN**、**RIGHT JOIN**和 **FULL JOIN**。

1. INNER JOIN：
   - INNER JOIN 用于将两个表中的数据根据关联条件连接在一起。它仅返回满足条件的行。
   - 语法：
     ```sql
     SELECT columns
     FROM table1
     INNER JOIN table2 ON table1.column = table2.column;
     ```

2. LEFT JOIN（或 LEFT OUTER JOIN）：
   - LEFT JOIN 用于从左边的表中返回所有行，以及与右边表中满足条件的行。
   - 语法：
     ```sql
     SELECT columns
     FROM table1
     LEFT JOIN table2 ON table1.column = table2.column;
     ```

3. RIGHT JOIN（或 RIGHT OUTER JOIN）：
   - RIGHT JOIN 类似于 LEFT JOIN，但它从右边的表返回所有行，以及与左边表中满足条件的行。

4. FULL JOIN（或 FULL OUTER JOIN）：
   - FULL JOIN 返回两个表中的所有行，无论是否满足条件。如果没有匹配的行，则返回 NULL 值。
   - 语法：
     ```sql
     SELECT columns
     FROM table1
     FULL JOIN table2 ON table1.column = table2.column;
     ```

### 自身连接

自身连接查询中使用的关键是表的自连接，**即使用相同的表多次**，并**使用别名**来区分这些不同的表引用。

假设我们有一个名为 `employees` 的表，其中包含员工的信息和每个员工的直接经理是其他员工的ID。表结构如下：

```sql
CREATE TABLE employees (
  employee_id INT PRIMARY KEY,
  employee_name VARCHAR(50),
  manager_id INT
);
-- 示例数据
INSERT INTO employees (employee_id, employee_name, manager_id)
VALUES
  (1, 'John', NULL),    -- John 是顶级经理
  (2, 'Alice', 1),      -- Alice 的直接经理是 John
  (3, 'Bob', 1),        -- Bob 的直接经理是 John
  (4, 'Carol', 2),      -- Carol 的直接经理是 Alice
  (5, 'David', 2);      -- David 的直接经理是 Alice
```

现在，我们要查询每个员工的姓名和他们的直接经理的姓名。

```sql
SELECT e1.employee_name AS employee, e2.employee_name AS manager
FROM employees e1
LEFT JOIN employees e2 ON e1.manager_id = e2.employee_id;
```

这个查询使用了两次 `employees` 表的引用，分别表示员工和他们的直接经理。我们使用 `LEFT JOIN` 来确保即使某些员工没有直接经理（例如，顶级经理 John），他们的记录也会被包括在结果中。结果将显示每个员工的姓名以及他们的直接经理的姓名。

```sql
-- 其他例子
SELECT k1.课程号 , k2.先行课号
FROM kc k1 , kc k2
WHERE k2.课程号 = k1.先行课号 AND k2.先行课号 IS NOT NULL;
```

### 多表连接

```sql
SELECT student.Sno , Sname, Cname, Grade
FROM SC, Course, Student
WHERE student.Sno = SC.Sno AND SC.Cno = Course.Cno;
```

## 嵌套查询

### 不相关子查询

是嵌套在主查询中的子查询，它独立于主查询并**不依赖于主查询的结果**。不相关子查询通常在主查询**中执行一次**，然后其结果用于主查询的比较或筛选。

```sql
SELECT student_name
FROM students
WHERE student_id NOT IN (SELECT enrolled_student_id FROM enrollments WHERE semester = 'Fall 2022');
```

在这个示例中，主查询从名为"students"的表中选择不在"enrollments"表中的学生。不相关子查询 `(SELECT enrolled_student_id FROM enrollments WHERE semester = 'Fall 2022')` 返回在秋季学期注册的学生的ID列表。主查询将这个列表与学生表中的学生ID进行比较，以找到不在列表中的学生。

不相关子查询通常用于对主查询的结果进行进一步筛选或过滤，而不是在多个表之间进行关联操作。这使得不相关子查询**适用于需要从一个表中筛选出另一个表中的值的情况。**

### 相关子查询

它**依赖于主查询的结果**。相关子查询**通常在主查询的每一行中执行一次**，以便在每次执行中获取不同的结果，然后将这些结果用于主查询的比较、筛选或排序。

```sql
-- 查询每个同学课程成绩高于他自己的平均成绩，输出学号，课程号，成绩
SELECT cj.学号, cj.课程号, cj.成绩
FROM cj
WHERE cj.成绩 > 
            (
                SELECT AVG(cj2.成绩) 
                FROM cj cj2 
                WHERE cj2.学号 = cj.学号
            ); -- 使用别名,是为了使用父查询中的学号，而不是子查询中的学号
            
-- 每门课取得其中学生的最高分，并输出课程号，学号，成绩
SELECT cj.课程号, cj.学号, cj.成绩
FROM cj
WHERE cj.成绩 = 
            (
                SELECT MAX(cj2.成绩) 
                FROM cj cj2 
                WHERE cj2.课程号 = cj.课程号
            );
```

相关子查询通常用于执行复杂的过滤、排序或比较操作，以便根据主查询的结果来获取更精确的数据。它们是 SQL 查询中的重要工具，允许在查询中使用更多的逻辑和条件。

### 带有ANY 和ALL 的子查询

1. **ANY 子查询**：`ANY`用于比较主查询结果和子查询结果集中的**任何一个值**。主查询条件只要与子查询结果中的任何一个匹配，条件就被视为真。

    ```sql
    SELECT student_name
    FROM students
    WHERE student_id = ANY (SELECT enrolled_student_id FROM enrollments WHERE course_id = 'C101');
    
    -- 查询其他系中比计科某一学生年龄小的学生年龄和姓名
    SELECT sname, sage
    FROM Student 
    WHERE sage < 
    			(
                    SELECT MAX(sage)
                    FROM Student
                    WHERE sdept = 'CS'
                )AND sdept <> 'CS';
    ```
    这将选择在课程'C101'中注册的任何学生。

2. **ALL 子查询**：`ALL`用于比较主查询结果和子查询结果集中的**所有值**。主查询条件必须与子查询结果中的所有值匹配，条件才被视为真。

    ```sql
    SELECT student_name
    FROM students
    WHERE student_id = ALL (SELECT enrolled_student_id FROM enrollments WHERE course_id = 'C101');
    ```
    这将选择只有在课程'C101'中注册的所有学生。

`ANY`和`ALL`子查询通常用于复杂的条件和筛选逻辑，以确定主查询结果与子查询结果的关系。它们允许你进行更精细的条件筛选，以满足特定需求。

### 带有EXISTS谓词的子查询——都是相关子查询

带有`EXISTS`谓词的子查询用于检查子查询是否返回结果，如果子查询返回至少一行记录，则条件为真，否则为假。这允许你在主查询中根据子查询的存在与否来选择数据。

通常，`EXISTS`子查询的目的是确定是否有满足特定条件的记录存在于子查询中。

```sql
-- 找出在成绩表中至少有一条记录的学生。
SELECT student_name
FROM students
WHERE EXISTS (SELECT 1 FROM grades WHERE grades.student_id = students.student_id);
```

上面的查询将返回在成绩表中至少有一条记录的学生的名字。`EXISTS`子查询中的`SELECT 1`实际上不需要返回任何特定的列，只要子查询返回结果行即可。

总结一下，`EXISTS`谓词用于检查子查询是否至少返回一行记录，如果返回，主查询中的条件被认为是真的。这对于筛选或关联满足某些条件的数据非常有用。

#### 使用`EXISTS`来模拟"除法"操作的一般步骤：

1. 编写外部查询，以获取希望从中筛选元组的主关系（通常称为被除关系）。
2. 使用子查询来查找第二个关系（通常称为除数关系）中与主关系相关联的元组。
3. 在主查询中使用`EXISTS`谓词，检查是否存在与除数关系中所有元组都有关联的元组。

```sql
-- 使用 EXISTS 谓词查找选修了所有课程的学生
SELECT StudentID, StudentName
FROM Students S
WHERE NOT EXISTS (
    SELECT CourseID
    FROM Courses C
    WHERE NOT EXISTS (
        SELECT 1
        FROM StudentCourses SC
        WHERE SC.StudentID = S.StudentID
        AND SC.CourseID = C.CourseID
    )
);
-- 即显示不存在未选修课程的学生会在结果中显示


-- 查询所有学生都选了的课的课程号和课程名
SELECT kc.课程号, kc.课程名
FROM kc
WHERE NOT EXISTS
            (
                SELECT *
                FROM xs
                WHERE NOT EXISTS
                            (
                                SELECT *
                                FROM cj
                                WHERE cj.学号 = xs.学号 AND cj.课程号 = kc.课程号
                            )
            );
```

## 集合查询

常见的集合查询操作包括并集（UNION）、交集（INTERSECT）、差集（EXCEPT）等。这些操作允许您从不同的查询中获取数据，并合并它们以生成一个新的结果集

1. **UNION（并集）**：UNION操作用于合并两个或多个查询的结果集，并去除重复的行。例如，如果您有两个查询，一个获取所有男性学生，另一个获取所有女性学生，您可以使用UNION将它们合并为一个包含所有学生的结果集。

   ```sql
   SELECT StudentName FROM Students WHERE Gender = 'Male'
   UNION
   SELECT StudentName FROM Students WHERE Gender = 'Female';
   ```

3. **INTERSECT（交集）**：INTERSECT操作用于查找两个或多个查询的结果集之间的共同行。例如，如果您想找到同时选修了课程A和课程B的学生，可以使用INTERSECT。

   ```sql
   SELECT StudentName FROM StudentCourses WHERE CourseName = 'Course A'
   INTERSECT
   SELECT StudentName FROM StudentCourses WHERE CourseName = 'Course B';
   ```

4. **EXCEPT（差集）**：EXCEPT操作用于从第一个查询的结果集中移除出现在第二个查询结果集中的行。例如，如果您想找到没有选修课程A的学生，可以使用EXCEPT。

   ```sql
   SELECT StudentName FROM Students
   EXCEPT
   SELECT StudentName FROM StudentCourses WHERE CourseName = 'Course A';
   ```

## 基于派生表的查询

在查询中使用子查询或派生表来生成一个临时的结果集，然后在该结果集上执行进一步的查询操作。临时表在FROM中

```sql
-- 查找所有年龄大于20岁的学生的平均成绩
SELECT AVG(Grade) AS AverageGrade
FROM (
    SELECT Grade
    FROM Students
    WHERE Age > 20
) AS Subquery;
```



## case when

`CASE WHEN` 是 SQL 中的条件表达式，它允许您根据不同的条件来选择不同的值。这在查询和数据处理中非常有用。下面是一个使用 `CASE WHEN` 的简单示例：

```sql
SELECT
  student_name,
  CASE
    WHEN age < 18 THEN '未成年'
    WHEN age >= 18 AND age < 30 THEN '青年'
    WHEN age >= 30 THEN '中年或以上'
    ELSE '未知'
  END AS age_group
FROM students;
```

上面的查询会根据学生的年龄将他们划分为不同的年龄组。`CASE WHEN` 表达式首先检查第一个条件，如果条件成立，则返回相应的值。如果条件不成立，则继续检查下一个条件，以此类推。最后的 `ELSE` 子句是可选的，用于处理未匹配任何条件的情况。

```sql
-- 查询每个专业的男生人数和女生人数，输出为：专业、男生数、女生数
SELECT 专业, SUM(CASE WHEN 性别 = '男' THEN 1 ELSE 0 END) AS 男生数, SUM(CASE WHEN 性别 = '女' THEN 1 ELSE 0 END) AS 女生数
FROM xs
GROUP BY 专业;
```

`CASE WHEN` 还可以用于在 `UPDATE` 语句中进行条件更新，或在 `ORDER BY` 子句中进行条件排序等多种情况。这使得它在处理数据库中的数据时非常灵活和有用。

# 数据更新

## 插入数据

### 插入元组

```sql
INSERT
	INTO <表名> [(<属性列1>[，<属性列2 >…)]
	VALUES (<常量1> [，<常量2>]    …           )
-- 例
INSERT INTO students (student_id, first_name, last_name, age, major)
VALUES
  (2, 'Alice', 'Smith', 22, 'Mathematics'),
  (3, 'Bob', 'Johnson', 21, 'History');
                
```

若需要插入的属性列中有一列是出生年月（即需要插入date/datetime类型的数据）

```sql
INSERT INTO students (student_id, first_name, last_name, date_of_birth, major)
VALUES (1, 'John', 'Doe', '1995-05-15', 'Computer Science');
-- 注意有单引号
```

#### date与datetime区别

1. `DATE` 数据类型：
   - `DATE` 数据类型仅存储日期信息，不包含时间。
   - 它通常以 "YYYY-MM-DD"（年-月-日）的格式表示，不包括小时、分钟和秒。
2. `DATETIME` 数据类型：
   - `DATETIME` 数据类型存储日期和时间信息，包括年、月、日、小时、分钟和秒。
   - 它通常以 "YYYY-MM-DD HH:MM:SS"（年-月-日 时:分:秒）的格式表示。

<u>**若子句中只指出了表名，没有指出属性列，则需要后续插入的当中都指定值，次序同（若值为空，也得写上`NULL`）**</u>

```sql
INSERT INTO students
VALUES
  (2, 'Alice', 'Smith', NULL, NULL);
```

### 插入子查询结果

在 SQL 中，你可以使用插入语句结合子查询来将子查询的结果插入到目标表中。这在需要将另一个表中的数据复制到目标表中或者根据查询结果生成新的数据行时非常有用。

假设你有两个表：`source_table` 和 `target_table`，并且你想将 `source_table` 中的某些数据插入到 `target_table` 中。

```sql
INSERT INTO target_table (column1, column2, ...) -- 指定你要插入数据的目标表。
SELECT source_column1, source_column2, ...       -- 列出目标表中你要插入数据的列。
FROM source_table                                -- 选择从 `source_table` 中提取的数据列。
WHERE some_condition; 						   -- 如果需要添加筛选条件
```

假设你有一个 `orders` 表和一个 `archived_orders` 表，你想将所有订单状态为 "已完成" 的订单从 `orders` 表中复制到 `archived_orders` 表中：

```sql
INSERT INTO archived_orders (order_id, order_date, customer_id)
SELECT order_id, order_date, customer_id
FROM orders
WHERE order_status = '已完成';
```

这将从 `orders` 表中选择所有已完成的订单，并将它们插入到 `archived_orders` 表中，只复制了 `order_id`、`order_date` 和 `customer_id` 列的数据。

## 修改数据

```sql
UPDATE  <表名>
SET  <列名>=<表达式>[，<列名>=<表达式>]…
[WHERE <条件>]； -- 修改指定表中满足WHERE子句条件的元组

-- 例
UPDATE students
SET age = 21
WHERE name = 'John';
-- 带子查询的数据修改语句
UPDATE employees
SET salary = salary * 1.10
WHERE employee_id IN (SELECT employee_id FROM salaries WHERE salary_type = 'base');
```

## 删除数据

**删除整个表中的数据：**

```sql
DELETE FROM table_name;
```

这将删除指定表中的所有行，但保留表的结构。

**删除特定条件下的行：**

```sql
DELETE FROM table_name
WHERE condition;
```

在 `WHERE` 子句中，你可以指定要删除哪些行。例如，如果你有一个名为 `employees` 的表，并且你想删除工资低于 30000 的员工，你可以执行以下操作：

```sql
DELETE FROM employees
WHERE salary < 30000;
```

**删除指定行数的数据：**

```sql
DELETE TOP(n) FROM table_name;
```

这将删除指定表中的前 n 行数据。

**注意**：请小心使用 `DELETE` 命令，因为它将永久性地删除数据。

```sql
-- 带子查询的
DELETE FROM orders
WHERE order_id IN (SELECT order_id FROM order_details WHERE total_amount < 100);
```

# 视图

视图（View）是一种**虚拟**的数据库对象，它是一个基于一个或多个表的查询结果的可视化表示。视图允许你以某种特定方式查看表中的数据，而**不实际更改表的结构或数据**。视图通常用于隐藏表的复杂性、提供数据安全性、简化查询以及重用查询逻辑。

以下是视图的一些关键特点和用途：

1. **数据过滤和筛选**：视图可以用于筛选数据，只显示满足某些条件的行。这可以帮助用户更容易地访问所需的数据。

2. **简化复杂查询**：通过在视图上执行复杂查询，用户可以避免编写冗长的SQL语句，尤其是当需要频繁执行相同查询时。

3. **安全性**：视图可用于限制用户对数据的访问，只允许他们查看他们有权限查看的数据，而不是整个表。

4. **重用查询逻辑**：将复杂查询的逻辑封装在视图中，可以在多个查询中重用它，减少了代码的复制和维护成本。

5. **减少数据冗余**：通过视图，可以将表的数据重组并按照需要展示，而不需要在数据库中存储冗余数据。

## 视图定义

### 视图建立

```sql
 CREATE  VIEW  <视图名>  [(<列名>  [，<列名>]…)]
 AS  <子查询>
 [WITH  CHECK  OPTION]；
```

```sql
CREATE VIEW SalesSummary AS
SELECT ProductName, SUM(Quantity) AS TotalQuantity, SUM(Revenue) AS TotalRevenue
FROM Sales
GROUP BY ProductName;
```

1. **<u>组成视图的属性列名：全部省略或全部指定</u>**
2. <u>**子查询不允许含有ORDER BY子句和DISTINCT短语**</u>
3. <u>**执行CREATE VIEW语句时只是把视图定义存入数据字典，并不执行其中的SELECT语句。**</u>

```sql
-- 基于多个基表的视图
        CREATE VIEW IS_S1(Sno，Sname，Grade)
        AS 
        SELECT Student.Sno，Sname，Grade
        FROM  Student，SC
        WHERE  Sdept= 'IS' AND
                       Student.Sno=SC.Sno AND
                       SC.Cno= '1'；
```

```sql
-- 基于视图的视图
        CREATE VIEW IS_S2
        AS
        SELECT Sno，Sname，Grade
        FROM  IS_S1
        WHERE  Grade>=90；
```



### 删除视图

```sql
DROP  VIEW  <视图名>；
```

1. 该语句从数据字典中删除指定的视图定义
2. 如果**该视图上还导出了其他视图**(例如：上面的IS_S1和IS_S2)，先删S2再删S1
3. 删除基表时，由该基表导出的所有视图定义都必须显式地使用DROP VIEW语句删除 

## 查询视图

## 更新视图

























