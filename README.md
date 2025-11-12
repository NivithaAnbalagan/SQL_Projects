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
# Column wise Null values
Query
``` sql
SELECT 
       SUM(CASE WHEN ENROLLMENTID IS NULL THEN 1 ELSE 0 END) AS ENROLLEMNTID,
       SUM(CASE WHEN STUDENTID IS NULL THEN 1 ELSE 0 END) AS STUDENTID,
       SUM(CASE WHEN COURSEID IS NULL THEN 1 ELSE 0 END) AS COURSEID,
       SUM(CASE WHEN SEMESTER IS NULL THEN 1 ELSE 0 END) AS SEMESTER,
       SUM(CASE WHEN YEAR IS NULL THEN 1 ELSE 0 END) AS YEAR,
       SUM(CASE WHEN GRADE IS NULL THEN 1 ELSE 0 END) AS GRADE 
       FROM ENROLLMENTS;
```
# Checking the duplicate values
Query
``` sql
SELECT ATTENDANCEID,COUNT(*) AS DUPLICATES FROM ATTENDANCE 
                             GROUP BY ATTENDANCEID
                             HAVING COUNT(*) > 1;
                             
SELECT COURSEID,COUNT(*) AS DUPLICATES FROM COURSES 
                             GROUP BY COURSEID
                             HAVING COUNT(*) > 1;
  
SELECT ENROLLMENTID,COUNT(*) AS DUPLICATES FROM ENROLLMENTS 
                             GROUP BY ENROLLMENTID
                             HAVING COUNT(*) > 1;
```
# Data Type Validation and Alteration
Query 
``` sql
DESC ATTENDANCE;
SET SQL_SAFE_UPDATE=0;
UPDATE ATTENDANCE
SET DATE=STR_TO_DATE(DATE,'%Y-%M-%D');
ALTER TABLE ATTENDANCE MODIFY COLUMN DATE DATE;

DESC ENROLLMENTS;
ALTER TABLE ENROLLMENTS MODIFY YEAR YEAR;
```
# Analysis Process
## Display all courses offered along with their department and instructor
Query
``` sql
SELECT COURSENAME,DEPARTMENT,INSTRUCTOR FROM COURSES;
```
## Show the attendance records for a given student on a particular date
Query
``` sql
SELECT* FROM ATTENDANCE;
SELECT * FROM ATTENDANCE WHERE STUDENTID=1084 AND DATE='2022-09-26';
```
## List all enrollment records for the current year
Query
``` sql
SELECT * FROM ENROLLMENTS WHERE YEAR=2019;
```
## Display all feedback submitted, ordered from newest to oldest
Query
``` sql
SELECT * FROM FEEDBACK ORDER BY FEEDBACKDATE DESC LIMIT 10;
```
## Show each student's enrolled courses (Student Full Name + Course Name + Semester + Year)
Query 
``` sql
SELECT A.SEMESTER,
       A.YEAR,
       A.STUDENTID,
       A.COURSEID,
       CONCAT(B.FIRSTNAME," ", B.LASTNAME) AS FULLNAME,
       C.COURSENAME
       FROM ENROLLMENTS AS A JOIN STUDENTS AS B ON  A.STUDENTID=B.STUDENTID 
							 JOIN COURSES AS C ON A.COURSEID=C.COURSEID;
```
## Count how many students are enrolled in each course
Query
``` sql
CREATE VIEW CONNECTIONTABLE AS(SELECT A.SEMESTER,
       A.YEAR,
       A.STUDENTID,
       A.COURSEID,
       CONCAT(B.FIRSTNAME," ", B.LASTNAME) AS FULLNAME,
       C.COURSENAME
       FROM ENROLLMENTS AS A JOIN STUDENTS AS B ON  A.STUDENTID=B.STUDENTID 
							 JOIN COURSES AS C ON A.COURSEID=C.COURSEID);
SELECT COUNT(STUDENTID)AS TOTAL_OF_STUDENTS ,COURSENAME FROM CONNECTIONTABLE GROUP BY  COURSENAME;
```
## Calculate the attendance percentage for each student in each course
Query
``` sql
SELECT StudentID, CourseID,
       (SUM(CASE WHEN AttendanceStatus='Present' THEN 1 ELSE 0 END) / COUNT(*)) * 100 AS ATTENDANCEPER
FROM ATTENDANCE
GROUP BY StudentID, CourseID HAVING ATTENDANCEPER > 60;
```
## Determine the most popular course (highest enrollment count)
Query
``` sql
SELECT COURSEID,
       COUNT(ENROLLMENTID) AS ENROLLMENTCOUNT 
       FROM ENROLLMENTS 
       GROUP BY COURSEID ORDER BY ENROLLMENTCOUNT DESC LIMIT 1;
```
