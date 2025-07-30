# OOP-Based-System-Design
# TASK 1: UML DIAGRAM 
<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/743fcca2-a8ed-4309-a228-3a7cc2124a4e" />


## Task 2: JavaScript Code Structure
```
class User {
    constructor(id, name, email) {
        this.id = id;
        this.name = name;
        this.email = email;
    }

    login() {
        console.log(`${this.name} logged in`);
    }

    logout() {
        console.log(`${this.name} logged out`);
    }
}

class Student extends User {
    constructor(id, name, email) {
        super(id, name, email);
        this.enrolledCourses = [];
    }

    enroll(course) {
        this.enrolledCourses.push(course);
        course.enrollStudent(this);
    }

    uploadAssignment(assignment, submission) {
        assignment.submit(this, submission);
    }
}

class Instructor extends User {
    constructor(id, name, email) {
        super(id, name, email);
        this.createdCourses = [];
    }

    createCourse(courseId, title) {
        const course = new Course(courseId, title, this);
        this.createdCourses.push(course);
        return course;
    }

    gradeAssignment(submission, grade) {
        submission.grade = grade;
    }
}

class Course {
    constructor(courseId, title, instructor) {
        this.courseId = courseId;
        this.title = title;
        this.instructor = instructor;
        this.students = [];
        this.assignments = [];
    }

    addAssignment(assignment) {
        this.assignments.push(assignment);
    }

    enrollStudent(student) {
        this.students.push(student);
    }
}

class Assignment {
    constructor(assignmentId, description) {
        this.assignmentId = assignmentId;
        this.description = description;
        this.submissions = new Map(); // student -> submission
    }

    submit(student, submission) {
        this.submissions.set(student.id, {
            student,
            content: submission,
            grade: null
        });
    }
}
```
## Task 3: OOP Principles Explanation
OOP Principles Explanation
🔹 Abstraction: We hide complex internal operations like how assignments are saved or marked. Users only interact through simple functions like submit() or gradeAssignment().

🔹 Encapsulation: Important data like course enrollments or submissions is kept private and can only be changed using specific methods.

🔹 Inheritance: Student and Instructor are types of User—they share common features like login and logout, and add their own.

🔹 Polymorphism: The same method names can behave differently—for example, both Student and Instructor can have their own versions of uploadAssignment or gradeAssignment.

## Task 4: SOLID Principles Used
🔹 Single Responsibility Principle (SRP): Each class has a clear job—User manages login, Course manages enrollments, Assignment manages student submissions.

🔹 Open/Closed Principle (OCP): You can add new features or roles (like TA) by extending classes, without changing old code.

🔹 Liskov Substitution Principle (LSP): Wherever a User is needed, you can also use a Student or Instructor without issues.

🔹 Interface Segregation Principle (ISP): Though not directly shown, the design suggests breaking large interfaces into smaller ones as needed.

🔹 Dependency Inversion Principle (DIP): It can be improved later by using external services (like a grading module) instead of hardcoding logic.
