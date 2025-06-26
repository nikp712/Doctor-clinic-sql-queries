# Doctor’s Clinic SQL Queries-Part A
SQL portfolio project for Doctor’s Clinic database case

## Table of Contents
1. [Overview](#overview)
2. [Project Features](#project-features)
3. [Database Summary](#database-summary)
4. [Preprocessing Steps](#preprocessing-steps)
5. [SQL Queries and Analysis](#sql-queries-and-analysis)
6. [Key Insights](#key-insights)
7. [How to Run the Project](#how-to-run-the-project)
8. [Results](#results)
9. [Future Improvements](#future-improvements)
10. [Acknowledgments](#acknowledgments)

---

## Overview
This project demonstrates SQL querying skills applied to a medical clinic relational database. The queries answer realistic business and operational questions, such as patient demographics, appointment volumes, staff analytics, and resource usage. The project is designed as a portfolio-ready SQL challenge for business analysts and data professionals.

---

## Project Features
- **SQL Query Design:** 10 real-world queries for business and healthcare analytics.
- **Data Filtering & Aggregation:** Use of WHERE, GROUP BY, HAVING, and advanced date functions.
- **Performance Focus:** Optimized for clarity, efficiency, and accuracy.
- **HR & Resource Analytics:** Analyze doctors, patients, appointments, drugs, and rooms.
- **Modular Queries:** Each section can be run independently for insight or adapted to other datasets.

---

## Database Summary
- **Dataset:** Doctor’s Clinic sample database from RMIT (2022).
- **Key Tables:** `patient`, `doctor`, `appointment`, `disease`, `drug`, `room`.
- **Data Types:** Includes text, numeric, date, and time fields.

> **Note:** The original database contains sensitive information and cannot be shared publicly. This repository includes only SQL code, sample queries, and documentation. If you are an instructor or reviewer and need access to the dataset, please contact me directly.

---

## Preprocessing Steps
1. Connected to the sample database in MySQL/MariaDB (or any SQL-compatible system).
2. Reviewed all tables, data types, and key relationships (ERD provided in the assignment PDF).
3. Prepared modular queries to answer business questions efficiently.

---

## SQL Queries and Analysis

1. **Find diseases containing "syndrome"**
   ```sql
   SELECT diseaseID, diseaseName
   FROM disease
   WHERE diseaseName LIKE '%syndrome%';
   ```

2. **Male patients over 50 in WOODSTOCK, oldest to youngest**   
   ```sql
   SELECT CONCAT(surname,', ', given) AS full_name, 
   TRUNCATE(DATEDIFF(SYSDATE(), dob)/365,0) AS age
   FROM patient 
   WHERE suburb = 'WOODSTOCK' AND sex = 'M'
   AND TRUNCATE(DATEDIFF(SYSDATE(), dob)/365,0) > 50
   ORDER BY dob DESC;
   ```

3. **Morning completed appointments in Room 2, Feb 2022**
   ```sql
   SELECT * FROM appointment
   WHERE DATE_FORMAT(dateOfAppointment, '%M') = 'February'
   AND DATE_FORMAT(dateOfAppointment, '%Y') = '2022'
   AND roomno = '2' AND done = 'Y' AND timeofappointment < "12:00:00"
   ORDER BY dateOfAppointment DESC, timeOfAppointment;
   ```

4. **Active female doctors (not resigned), full name, phone, years working**
   ```sql
   SELECT CONCAT(surname,',', given), phone, TRUNCATE(DATEDIFF(SYSDATE(),
   joined)/365,0) AS No_Of_Years_Working
   FROM doctor
   WHERE resigned IS NULL AND sex = 'F';
   ```

5. **Number of drugs per manufacturer**
   ```sql
   SELECT manufactureCode, COUNT(*)
   FROM drug
   GROUP BY manufactureCode;
   ```

6. **Number of appointments per patient**
   ```sql
   SELECT PatientID, COUNT(*)
   FROM appointment
   GROUP BY PatientID;
   ```

7. **For each gender, avg years worked & count (resigned doctors only)**
   ```sql
   SELECT sex, AVG(TRUNCATE(DATEDIFF(resigned, joined)/365,0)) AS
   "Average_No_Of_Years", COUNT(*)
   FROM doctor
   WHERE resigned IS NOT NULL
   GROUP BY sex;
   ```

8. **Blood types with fewer than 100 patients**
   ```sql
   SELECT bloodtype, COUNT(*)
   FROM patient
   GROUP BY bloodtype
   HAVING COUNT(*) <100;
   ```

9. **Doctors with less than 5000 appointments in 2021**
   ```sql
   FROM appointment
   WHERE DATE_FORMAT(dateOfAppointment, '%Y') = '2021'
   GROUP BY doctorID
   HAVING COUNT(*) < 5000;
   ```

10. **Appointments per month in 2021 (month order)**
    ```sql
    SELECT MONTHNAME(dateOfAppointment), COUNT(*)
    FROM appointment
    WHERE YEAR(dateOfAppointment)=2021
    GROUP BY MONTHNAME(dateOfAppointment),MONTH(dateOfAppointment)
    ORDER BY MONTH(dateOfAppointment);
    ```
    
---
 
## Key Insights
- The database supports detailed operational and clinical reporting.
- The majority of analytic needs (patient demographics, appointments, staff activity) can be met with targeted SQL.
- Advanced SQL functions (e.g. DATEDIFF, GROUP BY, HAVING) enable deeper business insights.

---

## How to Run the Project

1. Clone or download this repository to your computer.
2. Set up a MySQL or MariaDB instance (local or cloud).
3. Import the provided sample database (from your instructor or assignment kit).
4. Review your database schema and relational model, then use my sample queries as a template or reference.
5. Open SQL_Queries.sql in SQL Workbench/J or MySQL Workbench.
6. Run each query independently and review the results.

> **Note:**  
> The original database is not included due to privacy and copyright.  
> Adjust table/column names as needed for your database schema.

---

## Results
- Each query runs successfully on the provided dataset.
- Insights support decision-making for operations, HR, and resource management.
- Example result sets can be saved/exported for further analysis.

---

## Future Improvements
- Develop additional queries for appointment scheduling and billing analytics.
- Create stored procedures for common reporting tasks.
- Add visual dashboards using Tableau or Power BI.

---

## Acknowledgments
- Database brief: RMIT University.
- SQL tools: MySQL, SQL Workbench.
---

## Author

Nik Phan | RMIT University  
Final year student, Bachelor of Business Information Systems (Expected November 2025)

---
    


