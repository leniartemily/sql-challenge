# SQL_Challenge
* [General info](#general-info)
* [Technologies](#technologies)
* [Results](#results)


## General info
This challenge was to utilize 6 different csv files in PosgreSQL13. First I used quickdatabasediagrams.com to generate an ERD. After creating 6 tables in the ERD, I imported them and their appropriate the csv files into PostgreSQL13. I used the information from the tables in the Query Editor to answer the questions fround in [Results](#results).

## Technologies
* GitBash
* PostgreSQL13
* https://www.quickdatabasediagrams.com/

## Results
1. List the following details of each employee: employee number, last name, first name, sex, and salary.

--Query employees table
SELECT * FROM employees
--Query salaries table
SELECT * FROM salaries

--List the following details of each employee: employee number, last name, first name, sex, and salary.
SELECT employees.emp_no, employees.last_name, employees.first_name, employees.sex, salaries.salary
FROM employees
JOIN salaries on employees.emp_no = salaries.emp_no;

2. List first name, last name, and hire date for employees who were hired in 1986.
--Query employees table
SELECT * FROM employees

--Query to display hiring dates in 1986
SELECT first_name, last_name, hire_date
FROM employees
WHERE
hire_date >= '1986-01-01'
AND hire_date <= '1986-12-31';

3. List the manager of each department with the following information: department number, department name, the manager's employee number, last name, first name.
--Query departments table
SELECT * FROM departments
--Query department manager table
SELECT * FROM dept_manager
--Query employees table
SELECT * FROM employees
--List the manager of each department with the following information:
--department number, department name, the manager's employee number, last name, first name.
SELECT departments.dept_no, departments.dept_name, dept_manager.emp_no, employees.last_name, employees.first_name
FROM departments
JOIN dept_manager ON departments.dept_no = dept_manager.dept_no
JOIN employees ON dept_manager.emp_no = employees.emp_no;


4. List the department of each employee with the following information: employee number, last name, first name, and department name.
----Query dept_emp table
SELECT * FROM dept_emp
--Query employees table
SELECT * FROM employees
--Query departments table
SELECT * FROM departments
--List the department of each employee 
SELECT dept_emp.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees ON dept_emp.emp_no = employees.emp_no
JOIN departments ON dept_emp.dept_no = departments.dept_no;

5. List first name, last name, and sex for employees whose first name is "Hercules" and last names begin with "B."
--Query employees table
SELECT * FROM employees

--List first name, last name, and sex for employees whose first name is "Hercules" and last names begin with "B."
SELECT first_name, last_name, sex
FROM employees
WHERE
first_name = 'Hercules'
AND last_name LIKE 'B%';

6. List all employees in the Sales department, including their employee number, last name, first name, and department name.
----Query dept_emp table
SELECT * FROM dept_emp
--Query employees table
SELECT * FROM employees
--Query departments table
SELECT * FROM departments

--List all employees in the Sales department, including their employee number, last name, first name, and department name.
SELECT dept_emp.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees ON dept_emp.emp_no = employees.emp_no
JOIN departments ON dept_emp.dept_no = departments.dept_no
WHERE departments.dept_name = 'Sales';

7. List all employees in the Sales and Development departments, including their employee number, last name, first name, and department name.
----Query dept_emp table
SELECT * FROM dept_emp
--Query employees table
SELECT * FROM employees
--Query departments table
SELECT * FROM departments

--List all employees in the Sales and Development departments, including their employee number, last name, first name, and department name.
SELECT dept_emp.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees ON dept_emp.emp_no = employees.emp_no
JOIN departments ON dept_emp.dept_no = departments.dept_no
WHERE
departments.dept_name = 'Sales'
OR departments.dept_name = 'Development';

8. In descending order, list the frequency count of employee last names, i.e., how many employees share each last name.
--Query employees table
SELECT * FROM employees

--In descending order, list the frequency count of employee last names, i.e., how many employees share each last name.
SELECT last_name, COUNT (last_name) AS "frequency"
FROM employees
GROUP BY last_name
ORDER BY "frequency" DESC;
