# Java-Mini-Project

package Java.Mini.Priject;

import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;


class Student {
    private String name;
    private int rollNumber;
    private String className;
    private Account account;
    private Library library;

    public Student(String name, int rollNumber, String className) {
        this.name = name;
        this.rollNumber = rollNumber;
        this.className = className;
        this.account = new Account();
        this.library = new Library();
    }

    public String getName() {
        return name;
    }

    public int getRollNumber() {
        return rollNumber;
    }

    public String getClassName() {
        return className;
    }

    public Account getAccount() {
        return account;
    }
    
    public Library getLibrary() {
        return library;
    }
}

class Account {
    private double totalFees;
    private double payments;

    public Account() {
        totalFees = 0.0;
        payments = 0.0;
    }

    public void setTotalFees(double totalFees) {
        this.totalFees = totalFees;
    }

    public double getTotalFees() {
        return totalFees;
    }

    public void makePayment(double amount) {
        payments += amount;
    }

    public double getRemainingFees() {
        return totalFees - payments;
    }
}


class Library {
    private List<Book> books;

    public Library() {
        books = new ArrayList<>();
    }

    public void addBook(Book book) {
        books.add(book);
        System.out.println("Book added successfully.");
    }

    public void displayBooks() {
        if (books.isEmpty()) {
            System.out.println("No books found in the library.");
        } else {
            System.out.println("Books in the library:");
            for (Book book : books) {
                System.out.println("Title: " + book.getTitle() + ", Author: " + book.getAuthor());
            }
        }
    }
}

class Book {
    private String title;
    private String author;

    public Book(String title, String author) {
        this.title = title;
        this.author = author;
    }

    public String getTitle() {
        return title;
    }

    public String getAuthor() {
        return author;
    }
}


class School {
    private List<Student> students;

    public School() {
        students = new ArrayList<>();
    }

    public void addStudent(Student student) {
        students.add(student);
        System.out.println("Student added successfully.");
    }

    public void displayStudents() {
        if (students.isEmpty()) {
            System.out.println("No students found.");
        } else {
            System.out.println("Students:");
            for (Student student : students) {
                System.out.println("Name: " + student.getName() + ", Roll Number: " + student.getRollNumber() + ", Class: " + student.getClassName());
            }
        }
    }

    public List<Student> getStudents() {
        return students;
    }
}

public class SchoolManagementSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        School school = new School();

        while (true) {
            System.out.println("School Management System");
            System.out.println("1. Add Student");
            System.out.println("2. Display Students");
            System.out.println("3. Manage Student Account");
            
            System.out.println("4. Manage Library");
         
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");
            
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    scanner.nextLine(); // Consume newline character
                    System.out.println("Enter student name: ");
                    String name = scanner.nextLine();
                    System.out.println("Enter roll number: ");
                    int rollNumber = scanner.nextInt();
                    scanner.nextLine(); // Consume newline character
                    System.out.println("Enter class name: ");
                    String className = scanner.nextLine();

                    Student student = new Student(name, rollNumber, className);
                    school.addStudent(student);
                    break;

                case 2:
                    school.displayStudents();
                    break;

                case 3:
                    System.out.print("Enter student roll number: ");
                    int rollNum = scanner.nextInt();
                    scanner.nextLine(); // Consume newline character

                    boolean found = false;
                    for (Student s : school.getStudents()) {
                        if (s.getRollNumber() == rollNum) {
                            found = true;
                            manageAccount(scanner, s);
                           
                            break;
                        }
                    }

                    if (!found) {
                        System.out.println("Student not found.");
                    }
                    break;
                case 4:
                	System.out.print("Enter student roll number: ");
                    int rollN = scanner.nextInt();
                    scanner.nextLine(); // Consume newline character

                    boolean foundl = false;
                    for (Student s : school.getStudents()) {
                        if (s.getRollNumber() == rollN) {
                        	foundl = true;
                            manageLibrary(scanner, s);
                           
                            break;
                        }
                    }

                    if (!foundl) {
                        System.out.println("Student not found.");
                    }
                    break;
                case 5:
                    System.out.println("Exiting...");
                    System.out.println("");
                    System.out.println("Process complted");
                    System.out.println("");
                    System.out.println("Thank you...");
                    System.exit(0);

                default:
                    System.out.println("Invalid choice. Please try again.");
            }
            System.out.println();
        }
    }
    
    private static void manageLibrary(Scanner scanner, Student student) {
        Library library = student.getLibrary();

        while (true) {
            System.out.println("Library Management");
            System.out.println("1. Add Book");
            System.out.println("2. Display Books");
            System.out.println("3. Go Back");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    scanner.nextLine(); // Consume newline character
                    System.out.print("Enter book title: ");
                    String title = scanner.nextLine();
                    System.out.print("Enter author name: ");
                    String author = scanner.nextLine();

                    Book book = new Book(title, author);
                    library.addBook(book);
                    break;

                case 2:
                    library.displayBooks();
                    break;

                case 3:
                    return;

                default:
                    System.out.println("Invalid choice. Please try again.");
            }
            System.out.println();
        }
    }

    private static void manageAccount(Scanner scanner, Student student) {
        Account account = student.getAccount();

        while (true) {
            System.out.println("Student Account Management");
            System.out.println("1. Set Total Fees");
            System.out.println("2. Make Payment");
            System.out.println("3. Calculate Remaining Fees");
            System.out.println("4. Go Back");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter total fees: ");
                    double totalFees = scanner.nextDouble();
                    account.setTotalFees(totalFees);
                    System.out.println("Total fees set successfully.");
                    break;

                case 2:
                    System.out.print("Enter payment amount: ");
                    double payment = scanner.nextDouble();
                    account.makePayment(payment);
                    System.out.println("Payment recorded successfully.");
                    break;

                case 3:
                    double remainingFees = account.getRemainingFees();
                    System.out.println("Remaining fees: " + remainingFees);
                    break;

                case 4:
                    return;

                    
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
            System.out.println();
        }
    }
}
