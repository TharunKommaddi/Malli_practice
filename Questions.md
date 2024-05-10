# GROUP BY

Let's expand the example to include a wider range of aggregate functions on a relational database schema that now includes a `salaries` table. This will allow us to use `SUM`, `AVG`, `MAX`, and `MIN` aggregate functions in addition to `COUNT`.

### Expanded Table Creation and Data Insertion

#### 1. Employee Table
This table stores employee details.

**Table Creation Code:**
```sql
CREATE TABLE employees (
    employee_id INT,
    name VARCHAR(50),
    dept_id INT,
    city VARCHAR(50)
);
```

**Data Insertion Code:**
```sql
INSERT INTO employees (employee_id, name, dept_id, city) VALUES
(1, 'John Doe', 1, 'Boston'),
(2, 'Jane Smith', 1, 'Denver'),
(3, 'Alice Johnson', 2, 'Boston'),
(4, 'Chris Lee', 2, 'Denver'),
(5, 'Mike Brown', 3, 'Boston'),
(6, 'Sarah Davis', 3, 'Seattle');
```

#### 2. Department Table
This table lists departments.

**Table Creation Code:**
```sql
CREATE TABLE departments (
    dept_id INT,
    dept_name VARCHAR(50)
);
```

**Data Insertion Code:**
```sql
INSERT INTO departments (dept_id, dept_name) VALUES
(1, 'Sales'),
(2, 'Human Resources'),
(3, 'Information Technology');
```

#### 3. Salaries Table
This table stores employee salaries, linking them by `employee_id`.

**Table Creation Code:**
```sql
CREATE TABLE salaries (
    employee_id INT,
    salary INT
);
```

**Data Insertion Code:**
```sql
INSERT INTO salaries (employee_id, salary) VALUES
(1, 50000),
(2, 60000),
(3, 45000),
(4, 50000),
(5, 75000),
(6, 80000);
```

### Using Aggregate Functions

Now let's use the various SQL aggregate functions to gather insights from this data.

#### Query Using SUM, AVG, MAX, MIN, and COUNT
To use these functions, we need to join the `employees` table with the `salaries` table and then perform aggregation based on the `dept_id` which corresponds to departments.

**Query:**
```sql
SELECT d.dept_name,
       COUNT(e.employee_id) AS num_employees,
       SUM(s.salary) AS total_salaries,
       AVG(s.salary) AS average_salary,
       MAX(s.salary) AS max_salary,
       MIN(s.salary) AS min_salary
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id
JOIN salaries s ON e.employee_id = s.employee_id
GROUP BY d.dept_name;
```

**Expected Output:**
| dept_name              | num_employees | total_salaries | average_salary | max_salary | min_salary |
|------------------------|---------------|----------------|----------------|------------|------------|
| Sales                  | 2             | 110000         | 55000          | 60000      | 50000      |
| Human Resources        | 2             | 95000          | 47500          | 50000      | 45000      |
| Information Technology | 2             | 155000         | 77500          | 80000      | 75000      |


### Explanation:

- **COUNT(e.employee_id)**: Counts the number of employees in each department.
- **SUM(s.salary)**: Sums up the salaries for each department.
- **AVG(s.salary)**: Calculates the average salary within each department.
- **MAX(s.salary)**: Finds the maximum salary in each department.
- **MIN(s.salary)**: Identifies the minimum salary in each department.

These aggregate functions provide various dimensions of data analysis such as total expenditure on salaries per department, identifying departments with the highest and lowest earners, and understanding salary distributions within departments.

# ORDER BY, LIMIT, OFFSET 

### SQL Queries and Outputs

#### **1. ORDER BY DESC (Descending Order)**
This query sorts employees by their salary in descending order, so you can see the highest earners first. It's useful for quickly identifying top-paid employees.

**Query:**
```sql
SELECT e.name, s.salary
FROM employees e
JOIN salaries s ON e.employee_id = s.employee_id
ORDER BY s.salary DESC;
```

**Expected Output:**
```markdown
| name          | salary |
|---------------|--------|
| Sarah Davis   | 80000  |
| Mike Brown    | 75000  |
| Jane Smith    | 60000  |
| John Doe      | 50000  |
| Chris Lee     | 50000  |
| Alice Johnson | 45000  |
```

#### **2. ORDER BY ASC (Ascending Order)**
This query sorts employees by their salary in ascending order, which helps in identifying the lowest earners within the company. It's especially useful for HR and payroll analyses.

**Query:**
```sql
SELECT e.name, s.salary
FROM employees e
JOIN salaries s ON e.employee_id = s.employee_id
ORDER BY s.salary ASC;
```

**Expected Output:**
```markdown
| name          | salary |
|---------------|--------|
| Alice Johnson | 45000  |
| John Doe      | 50000  |
| Chris Lee     | 50000  |
| Jane Smith    | 60000  |
| Mike Brown    | 75000  |
| Sarah Davis   | 80000  |
```

#### **3. LIMIT with ORDER BY DESC**
This query is used to retrieve only the top 3 highest salaries from the database, ordered from the highest to lowest. This kind of query is useful for reports that need to highlight the top earners, such as executive summaries or financial reports.

**Query:**
```sql
SELECT e.name, s.salary
FROM employees e
JOIN salaries s ON e.employee_id = s.employee_id
ORDER BY s.salary DESC
LIMIT 3;
```

**Expected Output:**
```markdown
| name          | salary |
|---------------|--------|
| Sarah Davis   | 80000  |
| Mike Brown    | 75000  |
| Jane Smith    | 60000  |
```

#### **4. OFFSET with ORDER BY DESC and LIMIT**
This query demonstrates how to skip the top 3 highest salaries and then pick the next 3 in the list. It's particularly useful for pagination or when you need to display salary data in chunks, such as on different pages of a web application.

**Query:**
```sql
SELECT e.name, s.salary
FROM employees e
JOIN salaries s ON e.employee_id = s.employee_id
ORDER BY s.salary DESC
LIMIT 3 OFFSET 3;
```

**Expected Output:**
```markdown
| name          | salary |
|---------------|--------|
| John Doe      | 50000  |
| Chris Lee     | 50000  |
| Alice Johnson | 45000  |
```

### Explanation of Each Concept
- **ORDER BY DESC and ASC**: These queries provide a straightforward way to view salaries from highest to lowest and vice versa. They are crucial for financial analysis and employee management.
- **LIMIT**: It limits the number of rows returned by the query, which is essential when you only need to see a subset of the data, such as the top performers.
- **OFFSET**: It skips a specified number of records. When combined with `LIMIT`, it allows for advanced data slicing, which is crucial for creating paginated views in applications. 
