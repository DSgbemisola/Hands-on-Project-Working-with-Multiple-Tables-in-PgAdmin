# Hands-on-Project-Working-with-Multiple-Tables-in-PgAdmin

In this hands-on Project, I delved into Working with Multiple Tables in PgAdmin.

# Software Used in this Lab

PgAdmin 4 (PostgreSQL 15)

# Database Used in this Lab

The database used in this lab is an internal database belonging to IBM; a sample HR database. This is an HR database schema that consists of 5 tables called EMPLOYEES, JOB_HISTORY, JOBS, DEPARTMENTS and LOCATIONS. Each table has a few rows of sample data. The following diagram shows the tables for the HR database:

![image](https://github.com/user-attachments/assets/067a7925-0c1d-4a68-a62f-6f9879919301)

# Objectives

The objectives of this project were to:

1. Write SQL queries that access more than one table

2. Compose queries that access multiple tables using a nested statement in the WHERE clause

4. Build queries with multiple tables in the FROM clause

5. Write Implicit Join queries with join criteria specified in the WHERE clause

6. Specify aliases for table names and qualify column names with table aliases

# Highlights

- How does an Implicit version of CROSS JOIN (also known as Cartesian Join) statement syntax look?

  SELECT column_name(s)
  FROM table1, table2;

 - How does an Implicit version of INNER JOIN statement syntax look?

   SELECT column_name(s)
   FROM table1, table2
   WHERE table1.column_name = table2.column_name;

# Task A: Creating tables using SQL scripts

In this task, I created my new database named "HR DB" in PgAdmin and then executed the script containing the CREATE TABLE commands for all the tables rather than create each table manually by typing the DDL commands in the SQL editor.

The HR_Database_Create_Tables_Script.sql is available here: https://drive.google.com/file/d/1DOUzVXi-jsWBHR6CLNhAFQYUXdPjKFf7/view?usp=sharing

I downloaded the script file to my computer and uploaded it on my query editor of the HR DB I have initially created.

![image](https://github.com/user-attachments/assets/ebfef8e5-dbae-400c-a72f-260e281a6c94)

# Task B: Loading data into tables

In this task, I loaded all the data into the HR DB Database from .CSV files.

I downloaded the 5 .csv files below to my local computer:

Departments.csv - file is available here: https://drive.google.com/file/d/16srI4TCFh_O8VGfrhd3q-msbFp_472zu/view?usp=sharing

Employees.csv - file is available here: https://drive.google.com/file/d/1LLGie9dXrR9WiFYE7t0vyD0eVCRajRtI/view?usp=sharing

Jobs.csv - file is available here: https://drive.google.com/file/d/1qLTJiiOUfgZ9sk8RIFV_6PlSM66pjUTR/view?usp=sharing

Locations.csv - file is available here: https://drive.google.com/file/d/1WHQja5oaxKn7EqWB0sOSD1sHGZnagSBh/view?usp=sharing

JobsHistory.csv - file is available here: https://drive.google.com/file/d/1-IZUPqwPlkU3BdMV5EW2zZl0tg7jZs7C/view?usp=sharing

To load each table, I did the following steps.

I right-clicked on each table and selected Import tab.

Chose the csv file and clicked on OK to load the csv file.

# Task C: Exploring the Tables

To explore each table in the database, I right-clicked on each table and selected view/edit data to view "All Rows" 

1. Dapartment Table

   ![image](https://github.com/user-attachments/assets/f35245c5-9a25-4c18-a06a-333e9a4fadd8)

2. Employees Table

   ![image](https://github.com/user-attachments/assets/f83d2120-5fb2-486f-857b-9c27353832b2)

3. Jobs Table

   ![image](https://github.com/user-attachments/assets/a9e3931b-0fdd-4949-834c-4297808923d3)

4. Locations Table

   ![image](https://github.com/user-attachments/assets/f75e89be-93ec-4b7d-ac16-63b5368bd9e7)

5. JobsHistory Table

   ![image](https://github.com/user-attachments/assets/5bcc6784-ba60-4089-b2b9-21a45554683c)

# Task D: Accessing Multiple Tables with Sub-Queries

1. Retrieve only the EMPLOYEES records that correspond to jobs in the JOBS table.

   In solving this problem, I used the following SQL statement:

   SELECT * FROM employees 
   WHERE job_id IN (SELECT job_ident FROM jobs);

   ![image](https://github.com/user-attachments/assets/c1bf8b2d-dbac-4fbb-9053-4b0247990812)

2. Retrieve only the list of employees whose JOB_TITLE is Jr. Designer.

   In solving this problem, I used the following SQL statement:

   SELECT * FROM employees 
   WHERE job_id IN (SELECT job_ident FROM jobs
                     WHERE job_title = 'Jr.Designer');

   ![image](https://github.com/user-attachments/assets/250f01de-b4a6-4b48-a533-fc39380271ed)

3. Retrieve JOB information and who earn more than $70,000.

   In solving this problem, I used the following SQL statement:

   SELECT * FROM jobs 
   WHERE job_ident IN (SELECT job_id FROM employees
                     WHERE  salary > 70000);

   ![image](https://github.com/user-attachments/assets/7fa5296f-c902-4e80-ad5d-eb85f83a22e3)
   
4. Retrieve JOB information and list of employees whose birth year is after 1976.

   In solving this problem, I used the following SQL statement:

   SELECT * FROM jobs 
   WHERE job_ident IN (SELECT job_id FROM employees
                     WHERE EXTRACT(YEAR FROM b_date) > 1976);

  ![image](https://github.com/user-attachments/assets/b7f8f1de-816a-4be2-af21-8ce669137f2b)

5. Retrieve JOB information and list of female employees whose birth year is after 1976.

   In solving this problem, I used the following SQL statement:
   
   SELECT * FROM jobs 
   WHERE job_ident IN (SELECT job_id FROM employees
                     WHERE EXTRACT(YEAR FROM b_date) > 1976 AND sex = 'F');

   ![image](https://github.com/user-attachments/assets/da093978-c329-4a71-91a7-4df20655235e)

# Task E: Accessing Multiple Tables with Implicit Joins

1. Perform an implicit cartesian/cross join between EMPLOYEES and JOBS tables.

   In solving this problem, I used the following SQL statement:

   SELECT * FROM employees, jobs;

   ![image](https://github.com/user-attachments/assets/0882e9f4-064a-4f6c-9a75-46f15df6d991)

3. Retrieve only the EMPLOYEES records that correspond to jobs in the JOBS table.

   In solving this problem, I used the following SQL statement:

   SELECT * FROM employees E, jobs J
   WHERE E.job_id = J.job_ident;

   ![image](https://github.com/user-attachments/assets/62d209d2-04ce-404f-ab7d-b6147f144055)
