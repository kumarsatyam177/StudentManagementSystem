import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Student {
    private String name;
    private int rollNumber;
    private String section;

    public Student(String name, int rollNumber, String section) {
        this.name = name;
        this.rollNumber = rollNumber;
        this.section = section;
    }

    public int getRollNumber() {
        return rollNumber;
    }

    @Override
    public String toString() {
        return "NAME: " + name + ", ROLL NUMBER: " + rollNumber + ", SECTION: " + section;
    }
}

class StudentManagementSystem {
    private List<Student> students;

    public StudentManagementSystem() {
        students = new ArrayList<>();
    }

    public void addStudent(Student student) {
        students.add(student);
    }

    public boolean removeStudent(int rollNumber) {
        for (Student student : students) {
            if (student.getRollNumber() == rollNumber) {
                students.remove(student);
                return true;
            }
        }
        return false;
    }

    public Student searchStudent(int rollNumber) {
        for (Student student : students) {
            if (student.getRollNumber() == rollNumber) {
                return student;
            }
        }
        return null;
    }

    public List<Student> getAllStudents() {
        return students;
    }
}

public class Student_Management_System {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        StudentManagementSystem sms = new StudentManagementSystem();

        while (true) {
            System.out.println("\n----- STUDENT MANAGEMENT SYSTEM -----");
            System.out.println("1. ADD STUDENT");
            System.out.println("2. REMOVE STUDENT");
            System.out.println("3. SEARCH STUDENT");
            System.out.println("4. DISPLAY ALL STUDENTS");
            System.out.println("5. EXIT");
            System.out.print("ENTER YOUR CHOICE: ");
            int choice = sc.nextInt();

            switch (choice) {
                case 1:
                    sc.nextLine(); // consume newline
                    System.out.print("ENTER STUDENT NAME: ");
                    String name = sc.nextLine();

                    System.out.print("ENTER ROLL NUMBER: ");
                    int rollNumber = sc.nextInt();
                    sc.nextLine(); // consume newline

                    System.out.print("ENTER SECTION: ");
                    String section = sc.nextLine();

                    Student newStudent = new Student(name, rollNumber, section);
                    sms.addStudent(newStudent);
                    System.out.println("STUDENT ADDED SUCCESSFULLY.");
                    break;

                case 2:
                    System.out.print("ENTER ROLL NUMBER OF STUDENT TO REMOVE: ");
                    int rollToRemove = sc.nextInt();
                    boolean removed = sms.removeStudent(rollToRemove);
                    if (removed) {
                        System.out.println("STUDENT REMOVED.");
                    } else {
                        System.out.println("STUDENT NOT FOUND.");
                    }
                    break;

                case 3:
                    System.out.print("ENTER ROLL NUMBER OF STUDENT TO SEARCH: ");
                    int rollToSearch = sc.nextInt();
                    Student searchedStudent = sms.searchStudent(rollToSearch);
                    if (searchedStudent != null) {
                        System.out.println("STUDENT FOUND:");
                        System.out.println(searchedStudent);
                    } else {
                        System.out.println("STUDENT NOT FOUND.");
                    }
                    break;

                case 4:
                    List<Student> allStudents = sms.getAllStudents();
                    if (allStudents.isEmpty()) {
                        System.out.println("NO STUDENTS TO DISPLAY.");
                    } else {
                        System.out.println("ALL STUDENTS:");
                        for (Student student : allStudents) {
                            System.out.println(student);
                        }
                    }
                    break;

                case 5:
                    System.out.println("EXITING...");
                    System.out.println("THANK YOU");
                    System.out.println("HAVE A NICE DAY");
                    sc.close();
                    System.exit(0);
                    break;

                default:
                    System.out.println("INVALID CHOICE. PLEASE CHOOSE AGAIN.");
            }
        }
    }
}
