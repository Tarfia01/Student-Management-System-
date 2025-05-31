# Student-Management-System-
The system is about management of students.        We can add , delete or edit the record of the students. 
CODE FOR MANAGEMENT:
#include <iostream>
#include <vector>
#include <string>

using namespace std;

class Student {
public:
    int id;
    string name;
    int age;
    string course;

    void display() const {
        cout << "ID: " << id << ", Name: " << name
             << ", Age: " << age << ", Course: " << course << endl;
    }
};

vector<Student> students;
int nextId = 1;

void addStudent() {
    Student s;
    s.id = nextId++;

    cout << "Enter student name: ";
    cin.ignore();
    getline(cin, s.name);

    cout << "Enter age: ";
    cin >> s.age;

    cout << "Enter course: ";
    cin.ignore();
    getline(cin, s.course);

    students.push_back(s);
    cout << "Student added successfully.\n";
}

void viewStudents() {
    if (students.empty()) {
        cout << "No student records found.\n";
        return;
    }

    cout << "\n-- Student List --\n";
    for (const auto& s : students) {
        s.display();
    }
}

void deleteStudent() {
    int id;
    cout << "Enter student ID to delete: ";
    cin >> id;

    for (auto it = students.begin(); it != students.end(); ++it) {
        if (it->id == id) {
            students.erase(it);
            cout << "Student record deleted.\n";
            return;
        }
    }
    cout << "Student ID not found.\n";
}

void editStudent() {
    int id;
    cout << "Enter student ID to edit: ";
    cin >> id;

    for (auto& s : students) {
        if (s.id == id) {
            cout << "Editing record for ID: " << id << "\n";
            cout << "Enter new name (current: " << s.name << "): ";
            cin.ignore();
            getline(cin, s.name);

            cout << "Enter new age (current: " << s.age << "): ";
            cin >> s.age;

            cout << "Enter new course (current: " << s.course << "): ";
            cin.ignore();
            getline(cin, s.course);

            cout << "Record updated.\n";
            return;
        }
    }

    cout << "Student ID not found.\n";
}

int main() {
    int choice;

    do {
        cout << "\n===== Student Management System =====\n";
        cout << "1. Add Student\n";
        cout << "2. View All Students\n";
        cout << "3. Edit Student\n";
        cout << "4. Delete Student\n";
        cout << "5. Exit\n";
        cout << "Enter choice (1-5): ";
        cin >> choice;

        switch (choice) {
            case 1: addStudent(); break;
            case 2: viewStudents(); break;
            case 3: editStudent(); break;
            case 4: deleteStudent(); break;
            case 5: cout << "Exiting...\n"; break;
            default: cout << "Invalid choice. Try again.\n"; break;
        }

    } while (choice != 5);

    return 0;
}
