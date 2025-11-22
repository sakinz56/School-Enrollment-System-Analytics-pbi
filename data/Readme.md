# School Enrollment System Analytics (Power BI + SQL)

Author: Sakin Zaman  
Major: Computer Systems – Database Track  
University: NYC College of Technology (CUNY)  
Tools: SQL Server, Power BI, DAX, GitHub, CSV, Excel  

------------------------------------------------------------

PROJECT OVERVIEW

This project is a full School Enrollment Management System Analytics Dashboard.

It was built by designing a real relational database in SQL Server, exporting it as structured CSV files, and then building a full analytics dashboard in Power BI with proper data modeling and DAX measures.

This project simulates how real universities track enrollments, grades, performance, and course success.

------------------------------------------------------------

TECHNICAL WORKFLOW

SQL Server Database  
→ Data normalized into 3NF  
→ Exported as CSV files  
→ Imported into Power BI  
→ Relationships rebuilt in data model  
→ DAX measures created  
→ Interactive dashboard built  

------------------------------------------------------------

DATABASE DESIGN (SQL SERVER)

Tables created:

1. school_students  
2. school_courses  
3. school_enrollments  
4. school_grades  

------------------------------------------------------------

COMPOSITE ENROLLMENT KEY (CRITICAL SQL + POWER BI LOGIC)

To link enrollments and grades, a surrogate key was created:

EnrollmentKey = StudentID + '-' + CourseID + '-' + Term

This key connects:

school_enrollments → school_grades

Since Power BI does not support composite keys, this surrogate key was essential for building correct relationships.

------------------------------------------------------------

SQL QUERIES USED

Here are actual SQL queries used in the project:

-- Total distinct students
SELECT COUNT(DISTINCT StudentID)  
FROM school_students;

-- Total enrollments by course
SELECT CourseID, COUNT(*)  
FROM school_enrollments  
GROUP BY CourseID;

-- Completion rate by course
SELECT CourseID,
COUNT(CASE WHEN Status = 'Completed' THEN 1 END) * 100.0 / COUNT(*) AS CompletionRate
FROM school_enrollments
GROUP BY CourseID;

-- Average grade by course
SELECT CourseID, AVG(NumericScore)
FROM school_grades
GROUP BY CourseID;

------------------------------------------------------------

POWER BI DATA MODEL

Relationships rebuilt manually inside Power BI:

school_students[StudentID] → school_enrollments[StudentID]  
school_courses[CourseID] → school_enrollments[CourseID]  
school_enrollments[EnrollmentKey] → school_grades[EnrollmentKey]  

Star schema model.

------------------------------------------------------------

POWER BI DAX MEASURES

Total Enrollments =
COUNTROWS(school_enrollments)

Completed Enrollments =
CALCULATE(
    COUNTROWS(school_enrollments),
    school_enrollments[Status] = "Completed"
)

Completion Rate =
DIVIDE(
    [Completed Enrollments],
    [Total Enrollments]
)

Distinct Students =
DISTINCTCOUNT(school_enrollments[StudentID])

Average Grade =
AVERAGE(school_grades[NumericScore])

------------------------------------------------------------

DASHBOARD VISUALS

The Power BI dashboard includes:

1. Student Enrollment by Course  
2. Course Completion Rate by Course  
3. Grade Distribution by Course  
4. Course Difficulty Ranking (based on average grade)  
5. Total Students vs Total Enrollments cards  

All visuals are interactive and respond to filters and cross-highlighting.

------------------------------------------------------------

KEY INSIGHTS

• Some courses show high enrollment but lower completion rates.  
• Some advanced courses have lower average grades, indicating higher difficulty.  
• Not all enrollments have grades, which explains mismatches in counts.  
• Distinct student counts differ from total enrollments due to multiple course enrollments per student.

------------------------------------------------------------

PROJECT FOLDER STRUCTURE

/data  
    school_students.csv  
    school_courses.csv  
    school_enrollments.csv  
    school_grades.csv  

/dashboard  
    SchoolDashboard.pbix  

/sql  
    schema.sql  
    queries.sql  

------------------------------------------------------------

SKILLS DEMONSTRATED

✔ SQL Database Design  
✔ Normalization (3NF)  
✔ Composite Key Handling  
✔ Power BI Data Modeling  
✔ DAX Measures  
✔ Business Intelligence Development  
✔ Data Pipeline Design  
✔ Dashboard Storytelling  

------------------------------------------------------------

WHY THIS PROJECT MATTERS

This project reflects real-world data engineering and business intelligence pipelines used in actual organizations:

Database → ETL → Modeling → Analytics → Dashboard → Decision Making

 

------------------------------------------------------------

CONTACT

Name: Sakin Zaman  
GitHub: https://github.com/sakinz56  
LinkedIn: ADD YOUR LINK HERE  
Email: ADD IF YOU WANT
