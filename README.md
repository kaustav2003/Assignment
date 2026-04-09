## 📘 PROJECT README

Project Title: Scholarship Management System
Subject: DBMS & Core Java
Assessment: Technical Class Assessment — April 2026
Programme: MCA
Set Number: 7

---

📌 PROJECT DESCRIPTION
This project is a console-based Scholarship Management System developed using Core Java and MySQL with JDBC connectivity.

The system is designed to automate the scholarship application process for students. It eliminates manual verification delays by automatically determining eligibility based on predefined criteria and allows efficient management of applications.

---

⚙️ TECHNOLOGIES USED

* Core Java (Console Application)
* MySQL Database
* JDBC (Java Database Connectivity)

---

📂 PROJECT FEATURES

1. Submit Application

   * Allows user to enter student name, percentage, and annual income
   * Automatically determines eligibility based on:
     Percentage ≥ 75 AND Income ≤ 300000

2. Approve Application

   * Approves only eligible applications
   * Updates status from 'pending' to 'approved'

3. View Approved Students

   * Displays all students whose applications are approved

4. Total Scholarship Payout

   * Calculates total amount distributed
   * ₹10,000 per approved student

---

🗄️ DATABASE DETAILS

Database Name: (Specify your database name here)

Table Used: applications

Table Structure:

* app_id (Primary Key, Auto Increment)
* student (VARCHAR)
* percentage (DECIMAL)
* income (INT)
* eligible (BOOLEAN)
* status (ENUM: pending/approved/rejected)
* applied_on (DATE)

---

📁 PROJECT STRUCTURE

YourName_RollNo_SetNo/
│
├── src/
│   ├── DBConnection.java
│   └── Main.java
│
├── sql/
│   └── schema.sql
│
├── screenshots/
│   └── screenshot.png
│
└── README.txt

---

▶️ HOW TO RUN THE PROJECT

1. Install MySQL (version 5.7 or above)
2. Create a database
3. Run the schema.sql file to create the required table
4. Update database credentials in DBConnection.java
5. Compile the Java files:
   javac DBConnection.java Main.java
6. Run the program:
   java Main

---

⚠️ IMPORTANT NOTES

* All SQL queries are executed using PreparedStatement
* Exception handling is implemented using try-catch blocks
* The application is completely menu-driven
* No GUI is used — only console input via Scanner

---

📸 OUTPUT

Screenshot file (screenshot.png) demonstrates at least two working features of the system.

---

✅ CONCLUSION

This project successfully demonstrates the integration of Java with MySQL using JDBC and showcases how database-driven applications can automate real-world processes like scholarship management efficiently. 

---

👨‍💻 STUDENT DETAILS

Name: Kaustav Datta
Roll No: 37
Section: MCA 1 SEC A
Set No: 7

---
