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
   <img width="588" height="77" alt="Screenshot 2025-11-18 154406" src="https://github.com/user-attachments/assets/0f2bf2d9-1bb3-4ce2-82ee-a422827426ed" />


# Data Cleaning in Courses
Query
``` sql
SELECT COUNT(*) AS NULL_VALUE FROM COURSES WHERE COURSEID IS NULL or
							   COURSENAME IS NULL or
                               DEPARTMENT IS NULL or
                               CREDITS IS NULL or
                               INSTRUCTOR IS NULL;
```
<img width="588" height="77" alt="Screenshot 2025-11-18 154406" src="https://github.com/user-attachments/assets/93f1b7be-aabf-4dc9-a164-abcde50707bf" />


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
<img width="588" height="77" alt="Screenshot 2025-11-18 154406" src="https://github.com/user-attachments/assets/5edd3abf-d831-427c-91cf-ec8e3f661997" />



# Data Cleaning in Feedback
Query
``` sql
SELECT COUNT(*) AS NULL_VALUE FROM FEEDBACK WHERE FEEDBACKID IS NULL or
							   STUDENTID IS NULL or
                               FEEDBACKDATE IS NULL or
                               FEEDBACKTEXT IS NULL;
```                  
<img width="588" height="77" alt="Screenshot 2025-11-18 154406" src="https://github.com/user-attachments/assets/a600f0a6-1cd1-4b62-a701-0b28df22ffe1" />

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
<img width="588" height="77" alt="Screenshot 2025-11-18 154406" src="https://github.com/user-attachments/assets/03aec528-4208-4328-9b13-d7350a016a4f" />

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
<img width="588" height="77" alt="Screenshot 2025-11-18 154406" src="https://github.com/user-attachments/assets/9df4d41f-d9bb-4ac2-b00d-91d017a654be" />

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
<img width="512" height="74" alt="image" src="https://github.com/user-attachments/assets/fbb4cb6b-b8f7-4851-8ed5-96a5de0ac075" />

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
<img width="362" height="117" alt="image" src="https://github.com/user-attachments/assets/39563157-c6f0-4c22-8317-27860d4ea942" />

# Analysis Process
## Display all courses offered along with their department and instructor
Query
``` sql
SELECT COURSENAME,DEPARTMENT,INSTRUCTOR FROM COURSES;
```
<img width="288" height="135" alt="image" src="https://github.com/user-attachments/assets/299455a3-7f1d-484d-a8bf-b9936ccb0818" />

## Show the attendance records for a given student on a particular date
Query
``` sql
SELECT* FROM ATTENDANCE;
SELECT * FROM ATTENDANCE WHERE STUDENTID=1084 AND DATE='2022-09-26';
```
<img width="419" height="49" alt="image" src="https://github.com/user-attachments/assets/59199f86-ebf3-4622-89c9-26b98f7b3dee" />

## List all enrollment records for the current year
Query
``` sql
SELECT * FROM ENROLLMENTS WHERE YEAR=2019;
```
<img width="396" height="140" alt="image" src="https://github.com/user-attachments/assets/589a8160-4cac-4b4c-95aa-5793c1ee9c22" />

## Display all feedback submitted, ordered from newest to oldest
Query
``` sql
SELECT * FROM FEEDBACK ORDER BY FEEDBACKDATE DESC LIMIT 10;
```
<img width="425" height="142" alt="image" src="https://github.com/user-attachments/assets/b88841d2-fbf2-4bfa-b3ac-e0f2eb3e8f61" />

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
<img width="478" height="142" alt="image" src="https://github.com/user-attachments/assets/f5c1da7f-10e8-4863-b1bb-e7bf84f61c8f" />

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
<img width="236" height="139" alt="image" src="https://github.com/user-attachments/assets/a1707d1c-3083-41b0-824c-9b85e86ec47a" />

## Calculate the attendance percentage for each student in each course
Query
``` sql
SELECT StudentID, CourseID,
       (SUM(CASE WHEN AttendanceStatus='Present' THEN 1 ELSE 0 END) / COUNT(*)) * 100 AS ATTENDANCEPER
FROM ATTENDANCE
GROUP BY StudentID, CourseID HAVING ATTENDANCEPER > 60;
```
<img width="179" height="140" alt="image" src="https://github.com/user-attachments/assets/1b7d333d-fb9e-4dca-8b87-fd737834f2a4" />

## Determine the most popular course (highest enrollment count)
Query
``` sql
SELECT COURSEID,
       COUNT(ENROLLMENTID) AS ENROLLMENTCOUNT 
       FROM ENROLLMENTS 
       GROUP BY COURSEID ORDER BY ENROLLMENTCOUNT DESC LIMIT 1;
```
<img width="215" height="50" alt="image" src="https://github.com/user-attachments/assets/28c17d39-7b37-4241-aa9b-30283ba7b42c" />

