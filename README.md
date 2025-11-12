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
   ```   <img width="136" height="59" alt="image" src="https://github.com/user-attachments/assets/cdeebd69-fb1c-4690-a663-deb643f4d3f9" /> ```

# Data Cleaning in Courses
Query
``` sql
SELECT COUNT(*) AS NULL_VALUE FROM COURSES WHERE COURSEID IS NULL or
							   COURSENAME IS NULL or
                               DEPARTMENT IS NULL or
                               CREDITS IS NULL or
                               INSTRUCTOR IS NULL;
```

# Data Cleaning in Enrollments
Query
``` sql
SELECT COUNT(*) AS NULL_VALUE FROM ENROLLMENTS WHERE ENROLLMENTID IS NULL or
							   STUDENTID IS NULL or
                               COURSEID IS NULL or
                               SEMESTER IS NULL or
                               YEAR IS NULL or
                               GRADE IS NULL;
```



# Data Cleaning in Feedback
Query
``` sql
SELECT COUNT(*) AS NULL_VALUE FROM FEEDBACK WHERE FEEDBACKID IS NULL or
							   STUDENTID IS NULL or
                               FEEDBACKDATE IS NULL or
                               FEEDBACKTEXT IS NULL;
```                  

# Data Cleaning in Grades
Query
``` sql
SELECT COUNT(*) AS NULL_VALUE FROM GRADES WHERE GRADEID IS NULL or
							   STUDENTID IS NULL or
                               COURSEID IS NULL or
                               ASSIGNMENTTYPE IS NULL or
                               SCORE IS NULL or
                               DATE IS NULL;
```
# Data Cleaning in Students
Query
``` sql
SELECT COUNT(*) AS NULL_VALUE FROM STUDENTS WHERE STUDENTID IS NULL or
							   FIRSTNAME IS NULL or
                               LASTNAME IS NULL or
                               GENDER IS NULL or
                               DATEOFBIRTH IS NULL or
                               MAJOR IS NULL or
                               GPA IS NULL;
```
