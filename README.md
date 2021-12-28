# Pewlett-Hackard-Analysis
Migrate an employee database previously on Excel and VBA to SQL for Pewlett Hackard, a technology company and applying data  modelling, engineering, analysis skills on the database to handle an upcoming silver tsunami.

## Overview of the Pewlett-Hackard-Analysis
Bobby is an HR Analyst in Pewlett-Hackard. As baby boomers are retiring at a rapid pace so we need to help Bobby and his manager in the following tasks.
* Migrate data in CSV format into SQL tables
* Determine number of employees retiring per title so that the position can be filled soon.
* Determine if a mentorship program can be launched where experienced and successful employees stepping back into a part-time role instead of retiring completely. Their new role in the company would be as a mentor to the newly hired folks. 
* Look into the current employees to determine if some of them qualify for a mentoring program.

## Resources
* Data Source: [departents.csv](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/departments.csv), [dept_emp.csv](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/dept_emp.csv), [dept_manager.csv](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/dept_manager.csv), [employees.csv](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/employees.csv), [salaries.csv](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/salaries.csv), [titles.csv](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/titles.csv)
* Software: Postgresql -x64-11, pgAdmin 4 - version5.7

## Pewlett-Hackard-Analysis Results:
### retirement_titles table 
* A retirement_titles table is created to find the total retiring employees by title -by joining employees and titles tables retrieving  the emp_no, first_name, and last_name columns from the employees table and title, from_date, and to_date columns from the titles table and joining them both such that only the employees about to retire that i.e. employees who are born between January 1, 1952 and December 31, 1955 are included and exported as [retirement_titles.csv](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/retirement_titles.csv)

The first few elements of the queries can be found in![retirement_titles](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/retirement_titles.png?raw=true)

### unique_titles table 
* A unique_titles table is created to find the the unique employees with their most recent title-retrieving the employee number, first and last name, and title columns from the Retirement Titles table using  DISTINCT ON statement to retrieve the first occurrence of the employee number after sorting the table in ascending  order by the employee number and descending order by the last date (i.e., to_date) of the most recent title and exported as [unique_titles.csv](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/unique_titles.csv) 

The first few elements of the queries can be found in![unique_titles](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/unique_titles.png?raw=true)

### retiring_titles table
* A retiring_titles table is created to find the number of employees retiring with a certain title such that titles having maximum retirees comes first - retrieve the number of titles from the Unique Titles table.Group the table by title, then sort the count column in descending order and exported as [retiring_titles.csv](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/retiring_titles.csv)

The first few elements of the queries can be found in 
![retiring_titles](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/retiring_titles.png?raw=true)

### mentorship_eligibilty table
* A mentorship_eligibilty table is created to find the number of unique employees whose birth dates are between January 1, 1965 and December 31, 1965, and retireve their emp_no, first_name, last_name, and birth_date columns from the employees table. Retrieve the from_date and to_date columns from the dept_emp table. Retrieve the title column from the titles table.
by performing a join with employee, dept_emp and titles table after filtering the data on the to_date column to all the current employees, ordering by employee numberand and exporting table as [mentorship_eligibilty.csv](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/mentorship_eligibility.csv) 
![mentorship_eligibilty](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/mentorship_eligibilty.png?raw=true)

The queries executed above and below can be found in [Employee_Database_challenge](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Queries/Employee_Database_challenge.sql)

## Pewlett-Hackard-Analysis Summary:
#### A big part of the anlaysis is future-proofing the company by determining how many people will be retiring and, of those employees, who is eligible for a retirement package. 

Looking at the retiring_titles table we can say that the total number of people born between 1952 and 1955 are : 90398 

![total_retirees](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/total_retirees.png?raw=true)

But many of them have already left So, they will not account for roles to be filled. So the people still working and about to retire are : 72458

* A emp_to_retire_still_working table is created to find the number of unique employees whose birth dates are between January 1, 1965 and December 31, 1965, still working for PH i.e. to_date = '9999-01-01' and retrieve their emp_no, first_name, last_name, title, to_date columns from the retirement_titles table, order by emp_no and exporting table as [emp_to_retire_still_working.csv](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/emp_to_retire_still_working.csv) 

The details of the query can be found in ![emp_to_retire_still_working](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/emp_to_retire_still_working.png?raw=true)

If we count the number of employees in this table we see that the total employees about to retire are : 72458

![total_employees_about_to_retire](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/total_employees_about_to_retire.png?raw=true)


* An employees_currently_working table is created to find the number of unique employees who are still working for PH i.e. to_date = '9999-01-01' and retrieve their emp_no, birth_date, first_name, last_name, gender, hire_date from employees table and to_date columns from the dept_emp table, and joining them, ordering by emp_no order by emp_no and exporting table as [employees_currently_working.csv](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/employees_currently_working.csv) 

The first few elements of the queries can be found in ![employees_currently_working](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/employees_currently_working.png?raw=true)

Now, the total number of employees working currently in Pewlett-Hackard are: 240124

![total_employees_currently_working](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/total_employees_currently_working.png?raw=true)


So, 72458 employees out of 240124 are born between 1952 and 1955 and may retire soon that is 30% of the workforce. That is huge so to know how many roles need to be filled as the "silver tsunami" begins to make an impact. 

#### There is a talk about  a new mentoring program for employees getting ready to retire.  Instead of having a large chunk of their workforce retiring, Pewlett-Hackard wants to introduce a mentoring program: experienced and successful employees stepping back into a part-time role instead of retiring completely. So lets find out are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees.

* A retiring_titles_still_working table is created to find the  employee count for each title who will retire soon and may want to be a mentor and retrieve the count of people soon to retire, title from the emp_to_retire_still_working table, grouping them by title, ordering by emp_no descending and exporting table as [retiring_titles_still_working.csv](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/retiring_titles_still_working.csv) 

Total employee count for each title who will retire soon and may want to be a mentor and enjoy stepping back into a part-time role instead of retiring completely to mentor chosen employees who will take their place.

The details of the query can be found in ![retiring_titles_still_working](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/retiring_titles_still_working.png?raw=true)

#### The dept head of Sales and Developement showed special interest in knowing how many people in the departments they would need top pitch this idea.

* A emp_to_retire_still_working_bydept table is created to find the number of unique employees still working  with their titles and department names whose birth dates are between January 1, 1965 and December 31, 1965, and retireve their emp_no, first_name, last_name, title from the emp_to_retire_still_working table. Retrieve the dept_no from the dept_emp table. Retrieve the dept_name column from the department table.
by performing a join with emp_to_retire_still_working, dept_emp and department table after ordering by employee number and exporting table as [emp_to_retire_still_working_bydept.csv](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/emp_to_retire_still_working_bydept.csv) 

The first few elements of the queries can be found in ![emp_to_retire_still_working_bydept](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/emp_to_retire_still_working_bydept.png?raw=true)

To find exactly the employee count by title as well as department as Sales or Development
* An emp_to_retire_sales_dev table is created to find the  employee count for each title with their department name as Sales or Development who will retire soon and may want to be a mentor and retrieve the count of people soon to retire, title, dept_name from the emp_to_retire_still_working_bydept table, grouping them by dept_name, title, ordering by department name and emp_no descending and exporting table as [emp_to_retire_sales_dev.csv](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/emp_to_retire_sales_dev.csv) 


The details of the query can be found in ![emp_to_retire_sales_dev](https://github.com/sucharita1/Pewlett-Hackard-Analysis/blob/d9058c288f1e4e441e1b0147c8bf9894291c553e/Data/emp_to_retire_sales_dev.png?raw=true)







