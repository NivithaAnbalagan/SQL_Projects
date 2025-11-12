# Academic Data Management System-SQL_Projects
## Description
Developed a SQL-based system to efficiently store, manage, and analyze academic data including student records, attendance, grades, enrollments, and feedback. Implemented data cleaning, validation, and analytical queries to ensure data integrity and generate actionable academic insights.
# Creating Database
Query
``` sql
         CREATE DATABASE ACADEMICDATA;
         USE ACADEMICDATA;
```
# Data Cleaning in attendance
Query
```` sql
SELECT COUNT(*) AS NULL_VALUE FROM ATTENDANCE
           WHERE ATTENDANCEID IS NULL or
							   STUDENTID IS NULL or
                 COURSEID IS NULL or
                 DATE IS NULL or
                 ATTENDANCESTATUS IS NULL;
````
            <img width="116" height="49" alt="image" src="https://github.com/user-attachments/assets/6029a7a0-2922-4b87-812a-d1bd140662ce" />

         
                      

