# sql-challenge

**Project Name: Employee Database Management**

**Description:**
The Employee Database Management project involves designing a database schema to store employee data from CSV files, importing the data into a SQL database, and performing various data analysis queries. The project aims to gain insights into employees hired during the 1980s and 1990s, their departments, salaries, and other related information.

**Table Schema Creation:**
1. **departments** table:
   - dept_no (VARCHAR(4)) - Primary Key
   - dept_name (VARCHAR(100))

2. **dept_manager** table:
   - dept_no (VARCHAR(4)) - Foreign Key to departments.dept_no
   - emp_no (INT) - Foreign Key to employees.emp_no

3. **dept_emp** table:
   - emp_no (INT) - Foreign Key to employees.emp_no
   - dept_no (VARCHAR(4)) - Foreign Key to departments.dept_no

4. **employees** table:
   - emp_no (INT) - Primary Key
   - emp_title_id (VARCHAR(10)) - Foreign Key to titles.title_id
   - birth_date (DATE)
   - first_name (VARCHAR(50))
   - last_name (VARCHAR(50))
   - sex (CHAR(1))
   - hire_date (DATE)

5. **titles** table:
   - title_id (VARCHAR(10)) - Primary Key
   - title (VARCHAR(100))

6. **salaries** table:
   - emp_no (INT) - Foreign Key to employees.emp_no
   - salary (INT)

**Uploading CSV Files:**
1. Import the 'departments.csv' file into the departments table.
2. Import the 'dept_manager.csv' file into the dept_manager table.
3. Import the 'dept_emp.csv' file into the dept_emp table.
4. Import the 'employees.csv' file into the employees table, converting the date format to match SQL date format (YYYY-MM-DD).
5. Import the 'titles.csv' file into the titles table.
6. Import the 'salaries.csv' file into the salaries table.

**Modifying Date in employees.csv:**
To match the date format with SQL date format, follow these steps:
1. Open the employees.csv file in a text editor or spreadsheet application.
2. Locate the 'birth_date' and 'hire_date' columns.
3. Rearrange the dates in the format "YYYY-MM-DD." For example, change "7/25/1953" to "1953-07-25."
4. Save the modified CSV file.

**Querying the Questions Provided:**
1--List the employee number, last name, first name, sex, and salary of each employee.

SELECT
    e.emp_no AS employee_number,
    e.last_name,
    e.first_name,
    e.sex,
    s.salary
FROM
    employees AS e
JOIN
    salaries AS s ON e.emp_no = s.emp_no;

2--List the first name, last name, and hire date for the employees who were hired in 1986.

SELECT
    first_name,
    last_name,
    hire_date
FROM
    employees
WHERE
    hire_date >= '1986-01-01' AND hire_date <= '1986-12-31';

3--List the manager of each department along with their department number, department name, employee number, last name, and first name.

SELECT
    d.dept_no AS department_number,
    d.dept_name AS department_name,
    dm.emp_no AS employee_number,
    e.last_name,
    e.first_name
FROM
    departments d
JOIN
    dept_manager AS dm ON d.dept_no = dm.dept_no
JOIN
    employees AS e ON dm.emp_no = e.emp_no;

4--List the department number for each employee along with that employee’s employee number, last name, first name, and department name.

SELECT
    de.dept_no AS department_number,
    e.emp_no AS employee_number,
    e.last_name,
    e.first_name,
    d.dept_name AS department_name
FROM
    employees AS e
JOIN
    dept_emp AS de ON e.emp_no = de.emp_no
JOIN
    departments AS d ON de.dept_no = d.dept_no;

5--List first name, last name, and sex of each employee whose first name is Hercules and whose last name begins with the letter B.

SELECT
    first_name,
    last_name,
    sex
FROM
    employees
WHERE
    first_name = 'Hercules' AND last_name LIKE 'B%';


6--List each employee in the Sales department, including their employee number, last name, and first name.

SELECT
    e.emp_no AS employee_number,
    e.last_name,
    e.first_name
FROM
    employees AS e
JOIN
    dept_emp AS de ON e.emp_no = de.emp_no
JOIN
    departments AS d ON de.dept_no = d.dept_no
WHERE
    d.dept_name = 'Sales';


7--List each employee in the Sales and Development departments, including their employee number, last name, first name, and department name.

SELECT
    e.emp_no AS employee_number,
    e.last_name,
    e.first_name,
    d.dept_name AS department_name
FROM
    employees AS e
JOIN
    dept_emp AS de ON e.emp_no = de.emp_no
JOIN
    departments AS d ON de.dept_no = d.dept_no
WHERE
    d.dept_name IN ('Sales', 'Development');


8--List the frequency counts, in descending order, of all the employee last names (that is, how many employees share each last name).

SELECT
    last_name,
    COUNT(*) AS frequency
FROM
    employees
GROUP BY
    last_name
ORDER BY
    frequency DESC;

**refrences**
1. SQL Syntax and Concepts:
https://www.w3schools.com/sql/
 https://www.postgresql.org/docs/current/functions-datetime.html
 https://app.quickdatabasediagrams.com
 https://mode.com/sql-tutorial/
  https://www.postgresql.org/docs/current/functions-datetime.html
  