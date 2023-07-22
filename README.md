# project2
Student Gradebook:
 A program that manages student records, courses, and grades. Create classes for students, courses, and grades, and implement functionalities like adding students to courses, recording grades, and calculating overall GPA.


#include <iostream>
#include <string>
#include <vector>

class Student {
public:
    Student(std::string name, int rollNumber) : name(name), rollNumber(rollNumber) {}

    std::string getName() const {
        return name;
    }

    int getRollNumber() const {
        return rollNumber;
    }

private:
    std::string name;
    int rollNumber;
};

class Course {
public:
    Course(std::string name, int courseId) : name(name), courseId(courseId) {}

    std::string getName() const {
        return name;
    }

    int getCourseId() const {
        return courseId;
    }

private:
    std::string name;
    int courseId;
};

class Grade {
public:
    Grade(Student& student, Course& course, char grade) : student(student), course(course), grade(grade) {}

    char getGrade() const {
        return grade;
    }

    Student& getStudent() const {
        return student;
    }

    Course& getCourse() const {
        return course;
    }

private:
    Student& student;
    Course& course;
    char grade;
};

class Gradebook {
public:
    void addStudent(Student student) {
        students.push_back(student);
    }

    void addCourse(Course course) {
        courses.push_back(course);
    }

    void addGrade(Student& student, Course& course, char grade) {
        grades.push_back(Grade(student, course, grade));
    }

    float calculateGPA(Student& student) {
        int totalCredits = 0;
        float totalGradePoints = 0.0;

        for (const Grade& grade : grades) {
            if (&(grade.getStudent()) == &student) {
                totalCredits++;
                totalGradePoints += gradePoints(grade.getGrade());
            }
        }

        if (totalCredits == 0) {
            return 0.0;
        }

        return totalGradePoints / totalCredits;
    }

private:
    std::vector<Student> students;
    std::vector<Course> courses;
    std::vector<Grade> grades;

    float gradePoints(char grade) {
        switch (grade) {
            case 'A':
                return 4.0;
            case 'B':
                return 3.0;
            case 'C':
                return 2.0;
            case 'D':
                return 1.0;
            default:
                return 0.0;
        }
    }
};

int main() {
    Gradebook gradebook;

    // Add students
    Student student1("John Doe", 101);
    Student student2("Alice Smith", 102);
    Student student3("Bob Johnson", 103);
    Student student4("Emily Brown", 104);
    gradebook.addStudent(student1);
    gradebook.addStudent(student2);
    gradebook.addStudent(student3);
    gradebook.addStudent(student4);

    // Add courses
    Course course1("Mathematics", 201);
    Course course2("Science", 202);
    gradebook.addCourse(course1);
    gradebook.addCourse(course2);

    // Record grades
    gradebook.addGrade(student1, course1, 'A');
    gradebook.addGrade(student1, course2, 'B');
    gradebook.addGrade(student2, course1, 'B');
    gradebook.addGrade(student2, course2, 'C');
    gradebook.addGrade(student3, course1, 'A');
    gradebook.addGrade(student3, course2, 'A');
    gradebook.addGrade(student4, course1, 'A');
    gradebook.addGrade(student4, course2, 'A');

    // Calculate GPAs
    float gpa1 = gradebook.calculateGPA(student1);
    float gpa2 = gradebook.calculateGPA(student2);
    float gpa3 = gradebook.calculateGPA(student3);
    float gpa4 = gradebook.calculateGPA(student4);

    // Display GPAs
    std::cout << student1.getName() << "'s GPA: " << gpa1 << std::endl;
    std::cout << student2.getName() << "'s GPA: " << gpa2 << std::endl;
    std::cout << student3.getName() << "'s GPA: " << gpa3 << std::endl;
    std::cout << student4.getName() << "'s GPA: " << gpa4 << std::endl;

    return 0;
}
