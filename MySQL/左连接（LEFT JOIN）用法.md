左连接（LEFT JOIN）是SQL中的一种连接方式，用于从两个表中返回匹配的行。当在左表中找到匹配的行时，它会返回右表中的匹配行，如果没有找到匹配的行，则返回NULL值。左侧的表会完全显示。

示例：

假设有两个表，一个是员工表（employees），另一个是部门表（departments）。通过department_id、id关联。

employees表：

| id   | name1 | department_id |
| ---- | ----- | ------------- |
| 1    | 张三  | 1             |
| 2    | 李四  | 2             |
| 3    | 王五  | 3             |
| 4    | 赵六  | 4             |

CREATE TABLE employees(id INT,name1 VARCHAR(32),department_id INT);

INSERT INTO employees VALUES(1,'张三',1),(2,'李四',2),(3,'王五',3),(4,'赵六',4);

SELECT * FROM employees;

departments表：

| id   | name2  |
| ---- | ------ |
| 1    | 人事部 |
| 2    | 财务部 |
| 3    | 技术部 |
| 5    | 实施部 |

CREATE TABLE departments(id INT,name2 VARCHAR(32));

INSERT INTO departments VALUES(1,'人事部'),(2,'财务部'),(3,'技术部'),(5,'实施部');

SELECT * FROM departments;

现在我们想要查询每个员工所在的部门名称，可以使用左连接实现：

```sql
SELECT employees.id,employees.name1, departments.name2
FROM employees
LEFT JOIN departments ON employees.department_id = departments.id;
```

查询结果：

| id   | name1 | name2  |
| ---- | ----- | ------ |
| 1    | 张三  | 人事部 |
| 2    | 李四  | 财务部 |
| 3    | 王五  | 技术部 |
| 4    | 赵六  | NULL   |

--------------------------



右连接(RIGHT JOIN):当在右表中找到匹配的行时，它会返回左表中的匹配行，如果没有找到匹配的行，则返回NULL值。右侧的表会完全显示。



SELECT
	departments.id,
	employees.name1,
	departments.name2 
FROM
	employees
	RIGHT JOIN departments ON employees.department_id = departments.id;



| id   | name1 | name2  |
| ---- | ----- | ------ |
| 1    | 张三  | 人事部 |
| 2    | 李四  | 财务部 |
| 3    | 王五  | 技术部 |
| 5    | NULL  | 实施部 |







返回NULL的示例：

假设我们有一个学生表（students）和一个课程表（courses），现在我们想要查询每个学生选修的课程名称，但是有些学生可能没有选修任何课程。

students表：

| id   | name |
| ---- | ---- |
| 1    | 小明 |
| 2    | 小红 |
| 3    | 小刚 |

courses表：

| id   | name | student_id |
| ---- | ---- | ---------- |
| 1    | 数学 | 1          |
| 2    | 英语 | 2          |

现在我们想要查询每个学生选修的课程名称，可以使用左连接实现：

```sql
SELECT students.name, courses.name
FROM students
LEFT JOIN courses ON students.id = courses.student_id;
```

查询结果：

| name | name |
| ---- | ---- |
| 小明 | 数学 |
| 小红 | 英语 |
| 小刚 | NULL |