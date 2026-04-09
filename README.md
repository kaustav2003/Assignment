src/main.java:
import java.sql.*;
import java.util.Scanner;
public class Main {
static Scanner sc = new Scanner(System.in);
public static void main(String[] args) {
System.out.println("===== Scholarship Portal =====");
while (true) {
System.out.println("\n1. Submit Application");
System.out.println("2. Approve Application");
System.out.println("3. View Approved Students");
System.out.println("4. Total Scholarship Payout");
System.out.println("5. Total Applications Submitted");
System.out.println("6. Exit");
System.out.print("Enter choice: ");
int choice = sc.nextInt();
sc.nextLine();
switch (choice) {
case 1: submitApplication(); break;
case 2: approveApplication(); break;
case 3: viewApproved(); break;
case 4: totalPayout(); break;
case 5: totalApplications(); break;
case 6:
System.out.println("Goodbye!");
System.exit(0);
default:
System.out.println("Invalid choice. Try again.");
}
}
}
static void submitApplication() {
System.out.print("Student Name: ");
String name = sc.nextLine();
System.out.print("Marks% (e.g. 88.5): ");
double percentage = sc.nextDouble();
System.out.print("Annual Income: ");
int income = sc.nextInt();
boolean eligible = (percentage >= 75 && income <= 300000);
String sql = "INSERT INTO applications (student, percentage, income, eligible) VALUES (?, ?, ?, ?)";
try (Connection con = DBConnection.getConnection();
PreparedStatement ps = con.prepareStatement(sql)) {
ps.setString(1, name);
ps.setDouble(2, percentage);
ps.setInt(3, income);
ps.setBoolean(4, eligible);
ps.executeUpdate();
System.out.println("Application submitted ");
} catch (SQLException e) {
System.out.println("Error submitting application: " + e.getMessage());
}
}
static void approveApplication() {
System.out.print("Enter Application ID to approve: ");
int appId = sc.nextInt();
String sql = "UPDATE applications SET status='approved' WHERE app_id=? AND eligible=TRUE";
try (Connection con = DBConnection.getConnection();
PreparedStatement ps = con.prepareStatement(sql)) {
ps.setInt(1, appId);
int rows = ps.executeUpdate();
if (rows > 0) {
System.out.println("Application " + appId + " approved successfully.");
} else {
System.out.println("Student is not eligible.");
}
} catch (SQLException e) {
System.out.println("Error approving application: " + e.getMessage());
}
}
static void viewApproved() {
String sql = "SELECT * FROM applications WHERE status='approved'";
try (Connection con = DBConnection.getConnection();
PreparedStatement ps = con.prepareStatement(sql);
ResultSet rs = ps.executeQuery()) {
System.out.println("\n--- Approved Students ---");
System.out.printf("%-5s %-20s %-10s %-12s%n", "ID", "Name", "Marks%", "Income");
System.out.println("---------------------------------------------");
boolean found = false;
while (rs.next()) {
found = true;
System.out.printf("%-5d %-20s %-10.2f %-12d%n",
rs.getInt("app_id"),
rs.getString("student"),
rs.getDouble("percentage"),
rs.getInt("income"));
}
if (!found) System.out.println("No approved students yet.");
} catch (SQLException e) {
System.out.println("Error fetching data: " + e.getMessage());
}
}
static void totalPayout() {
String sql = "SELECT COUNT(*) * 10000 AS total FROM applications WHERE status='approved'";
try (Connection con = DBConnection.getConnection();
PreparedStatement ps = con.prepareStatement(sql);
ResultSet rs = ps.executeQuery()) {
if (rs.next()) {
System.out.println("Total Scholarship Payout: Rs. " + rs.getInt("total"));
}
} catch (SQLException e) {
System.out.println("Error calculating payout: " + e.getMessage());
}
}
static void totalApplications() {
String sql = "SELECT COUNT(*) AS total FROM applications";
try (Connection con = DBConnection.getConnection();
PreparedStatement ps = con.prepareStatement(sql);
ResultSet rs = ps.executeQuery()) {
if (rs.next()) {
System.out.println("Total Applications Submitted: " + rs.getInt("total"));
}
} catch (SQLException e) {
System.out.println("Error fetching count: " + e.getMessage());
}
}
}
src/DBConnection.java:
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
public class DBConnection {
// Change these to match your MySQL setup
private static final String URL = "jdbc:mysql://localhost:3306/scholarship_db";
private static final String USER = "root";
private static final String PASSWORD = "Kaustav@02#.me";
public static Connection getConnection() throws SQLException {
try {
Class.forName("com.mysql.cj.jdbc.Driver");
return DriverManager.getConnection(URL, USER, PASSWORD);
} catch (ClassNotFoundException e) {
throw new SQLException("MySQL JDBC Driver not found!", e);
}
}
}
sql/schema.sql:
CREATE DATABASE IF NOT EXISTS scholarship_db;
USE scholarship_db;
CREATE TABLE IF NOT EXISTS applications (
app_id INT PRIMARY KEY AUTO_INCREMENT,
student VARCHAR(100),
percentage DECIMAL(5,2),
income INT,
eligible BOOLEAN,
status ENUM('pending', 'approved', 'rejected') DEFAULT 'pending',
applied_on DATE DEFAULT (CURRENT_DATE)
);
Screenshots:

