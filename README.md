# STUDENT-GRADE-MANAGEMENT-SYSTEM
#include <iostream>
#include <vector>
#include <string>
#include <iomanip>
using namespace std;

struct Student {
    int SAPid;
    string name;
    vector<float> marks;
    vector<char> subjectGrades;
    float average;
    char grade;
};

void addStudent(vector<Student>& students);
void displayStudents(const vector<Student>& students);
void calculateGrades(vector<Student>& students);
char assignGrade(float mark);

int main() {
    vector<Student> students;
    int choice;

    do {
        cout << "\n========== Student Grade Management System ==========" << endl;
        cout << "1. Add Student" << endl;
        cout << "2. Display All Students" << endl;
        cout << "3. Calculate Grades" << endl;
        cout << "4. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                addStudent(students);
                break;
            case 2:
                displayStudents(students);
                break;
            case 3:
                calculateGrades(students);
                break;
            case 4:
                cout << "Exiting program. enjoyed alot and learned alot from SIR NADEEM/SIR IHTISHAMULLAH!" << endl;
                break;
            default:
                cout << "Invalid choice! Please try again." << endl;
        }
    } while (choice != 4);

    return 0;
}

void addStudent(vector<Student>& students) {
    Student newStudent;
    cout << "\nEnter Student SAP ID: ";
    cin >> newStudent.SAPid;
    cin.ignore();
    cout << "Enter Student Name: ";
    getline(cin, newStudent.name);

    int numSubjects;
    cout << "Enter the number of subjects: ";
    cin >> numSubjects;

    newStudent.marks.resize(numSubjects);
    newStudent.subjectGrades.resize(numSubjects);
    for (int i = 0; i < numSubjects; ++i) {
        cout << "Enter marks for subject " << i + 1 << ": ";
        cin >> newStudent.marks[i];
    }

    newStudent.average = 0;
    newStudent.grade = 'N';
    students.push_back(newStudent);
    cout << "Student added successfully!" << endl;
}

void displayStudents(const vector<Student>& students) {
    if (students.empty()) {
        cout << "\nNo students to display." << endl;
        return;
    }

    cout << "\n========= Student List =========" << endl;
    for (const auto& student : students) {
        cout << "\nSAP ID: " << student.SAPid << endl;
        cout << "Name: " << student.name << endl;
        cout << "Average: " << fixed << setprecision(2) << student.average << endl;
        cout << "Overall Grade: " << student.grade << endl;
        cout << "Subject Grades: " << endl;
        for (size_t i = 0; i < student.marks.size(); ++i) {
            cout << "  Subject " << i + 1 << ": Marks = " << student.marks[i] << ", Grade = " << student.subjectGrades[i] << endl;
        }
    }
}

void calculateGrades(vector<Student>& students) {
    if (students.empty()) {
        cout << "\nNo students to calculate grades for." << endl;
        return;
    }

    for (auto& student : students) {
        float total = 0;
        for (size_t i = 0; i < student.marks.size(); ++i) {
            total += student.marks[i];
            student.subjectGrades[i] = assignGrade(student.marks[i]);
        }
        student.average = total / student.marks.size();
        student.grade = assignGrade(student.average);
    }

    cout << "\nGrades calculated successfully!" << endl;
}

char assignGrade(float mark) {
    if (mark >= 90) return 'A';
    else if (mark >= 80) return 'B';
    else if (mark >= 70) return 'C';
    else if (mark >= 60) return 'D';
    else return 'F';
    return 0;
}
