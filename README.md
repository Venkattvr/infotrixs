# infotrixs
public class Employee {
 private int id;
 private String name;
 private double salary;
}
FileManager Class:
import java.io.*;
import java.util.ArrayList;
import java.util.List;
public class FileManager {
 private static final String FILE_NAME = 
"employees.txt";
 public static void writeToFile(List<Employee> 
employees) {
 try (ObjectOutputStream oos = new
ObjectOutputStream(new FileOutputStream(FILE_NAME))) {
 oos.writeObject(employees);
 } catch (IOException e) {
 e.printStackTrace();
 }
 }
 public static List<Employee> readFromFile() {
 List<Employee> employees = new ArrayList<>();
 try (ObjectInputStream ois = new
ObjectInputStream(new FileInputStream(FILE_NAME))) {
 employees = (List<Employee>) 
ois.readObject();
 } catch (IOException | ClassNotFoundException 
e) {
 e.printStackTrace();
 }
 return employees;
 }
}
EmployeeManagementSystem Class:
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;
public class EmployeeManagementSystem {
 private static List<Employee> employees = new
ArrayList<>();
 private static Scanner scanner = new
Scanner(System.in);
 public static void main(String[] args) {
 loadEmployees();
 boolean exit = false;
 while (!exit) {
 System.out.println("1. Add Employee");
 System.out.println("2. View Employees");
 System.out.println("3. Exit");
 System.out.print("Enter your choice: ");
 int choice = scanner.nextInt();
 scanner.nextLine(); // Consume newline
 switch (choice) {
 case 1:
 addEmployee();
break;
 case 2:
 viewEmployees();
break;
 case 3:
 saveEmployees();
exit = true;
 break;
 default:
 System.out.println("Invalid 
choice!");
 }
 }
 }
 private static void loadEmployees() {
 employees = FileManager.readFromFile();
 }
 private static void saveEmployees() {
 FileManager.writeToFile(employees);
 }
 private static void addEmployee() {
 
 
 }
 private static void viewEmployees() {
 
 }
}
Employee Class:
import java.io.Serializable;
public class Employee implements Serializable {
 
import java.io.*;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;
public class EmployeeManagementSystem {
 private static List<Employee> employees = new
ArrayList<>();
 private static final String FILE_NAME = 
"employees.dat";
 private static Scanner scanner = new
Scanner(System.in);
 public static void main(String[] args) {
 loadEmployees();
 boolean exit = false;
 while (!exit) {
 System.out.println("1. Add Employee");
 System.out.println("2. View Employees");
 System.out.println("3. Update Employee");
 System.out.println("4. Search Employee");
 System.out.println("5. Exit");
 System.out.print("Enter your choice: ");
 int choice = scanner.nextInt();
 scanner.nextLine(); 
 switch (choice) {
 case 1:
 addEmployee();
break;
 case 2:
 viewEmployees();
break;
 case 3:
 updateEmployee();
break;
 case 4:
 searchEmployee();
break;
 case 5:
 saveEmployees();
exit = true;
break;
 default:
 System.out.println("Invalid 
choice!");
 }
 }
 }
 private static void loadEmployees() {
 try (ObjectInputStream ois = new
ObjectInputStream(new FileInputStream(FILE_NAME))) {
 employees = (List<Employee>) 
ois.readObject();
 } catch (IOException | ClassNotFoundException 
e) {
 // Ignore for now, file might not exist on 
first run
 }
 }
 private static void saveEmployees() {
 try (ObjectOutputStream oos = new
ObjectOutputStream(new FileOutputStream(FILE_NAME))) {
 oos.writeObject(employees);
 } catch (IOException e) {
 e.printStackTrace();
 }
 }
 private static void addEmployee() {
 System.out.print("Enter Employee ID: ");
 int id = scanner.nextInt();
 scanner.nextLine(); 
 System.out.print("Enter Employee Name: ");
 String name = scanner.nextLine();
 System.out.print("Enter Employee Salary: ");
 double salary = scanner.nextDouble();
 Employee employee = new Employee(id, name, 
salary);
 employees.add(employee);
 System.out.println("Employee added 
successfully!");
 }
 private static void viewEmployees() {
 System.out.println("Employee List:");
 for (Employee employee : employees) {
 System.out.println(employee);
 }
 }
 private static void updateEmployee() {
 System.out.print("Enter Employee ID to update: 
");
 int id = scanner.nextInt();
 scanner.nextLine(); 
 for (Employee employee : employees) {
 if (employee.getId() == id) {
 System.out.print("Enter new Employee 
Name: ");
 String name = scanner.nextLine();
 System.out.print("Enter new Employee 
Salary: ");
 double salary = scanner.nextDouble();
 employee.setName(name);
 employee.setSalary(salary);
 System.out.println("Employee 
information updated successfully!");
 return;
 }
 }
 System.out.println("Employee with ID " + id + " 
not found.");
 }
 private static void searchEmployee() {
 System.out.print("Enter Employee ID to search: 
");
 int id = scanner.nextInt();
 for (Employee employee : employees) {
 if (employee.getId() == id) {
 System.out.println("Employee found:");
 System.out.println(employee);
 return;
 }
 }
 System.out.println("Employee with ID " + id + " 
not found.");
 }
}
