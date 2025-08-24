Flutter/Dart mein API se CRUD operations karne ke liye aapko kuch basic steps follow karne honge. Main aapko **Model**, **Controller**, aur **Page** banane ka tareeka step-by-step bataunga, jisme aap CRUD operations ko API se handle karenge. Aap isko apne GitHub ke notes ke liye use kar sakte hain. Sabhi CRUD operations (Create, Read, Update, Delete) ko implement karenge.

### 1. **Model Class** (`student.dart`)

Model class mein aapko student ke data ka structure define karna hota hai. Ye class API response ko parse karne aur data ko manage karne mein madad karti hai.

```dart
class Student {
  final int id;
  final String name;
  final int age;

  Student({required this.id, required this.name, required this.age});

  // Factory method to create a Student from JSON
  factory Student.fromJson(Map<String, dynamic> json) {
    return Student(
      id: json['id'],
      name: json['name'],
      age: json['age'],
    );
  }

  // Method to convert Student object to JSON
  Map<String, dynamic> toJson() {
    return {
      'id': id,
      'name': name,
      'age': age,
    };
  }
}
```

### 2. **API Service Class** (`api_service.dart`)

Is class mein aapko API calls handle karni hoti hain. HTTP requests karne ke liye `http` package ka use karte hain.

#### Install `http` package:

```bash
flutter pub add http
```

#### API Service Class:

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;
import 'student.dart';

class ApiService {
  final String baseUrl = 'https://api.example.com/students';

  // Fetch Students List
  Future<List<Student>> fetchStudents() async {
    final response = await http.get(Uri.parse(baseUrl));
    if (response.statusCode == 200) {
      List<dynamic> data = json.decode(response.body);
      return data.map((json) => Student.fromJson(json)).toList();
    } else {
      throw Exception('Failed to load students');
    }
  }

  // Add a new Student
  Future<void> addStudent(Student student) async {
    final response = await http.post(
      Uri.parse(baseUrl),
      headers: {'Content-Type': 'application/json'},
      body: json.encode(student.toJson()),
    );
    if (response.statusCode != 201) {
      throw Exception('Failed to add student');
    }
  }

  // Update an existing Student
  Future<void> updateStudent(Student student) async {
    final response = await http.put(
      Uri.parse('$baseUrl/${student.id}'),
      headers: {'Content-Type': 'application/json'},
      body: json.encode(student.toJson()),
    );
    if (response.statusCode != 200) {
      throw Exception('Failed to update student');
    }
  }

  // Delete a Student
  Future<void> deleteStudent(int id) async {
    final response = await http.delete(Uri.parse('$baseUrl/$id'));
    if (response.statusCode != 200) {
      throw Exception('Failed to delete student');
    }
  }
}
```

### 3. **Controller Class** (`student_controller.dart`)

Controller class ko use karke aap CRUD operations ko handle karenge aur UI ko data pass karenge.

```dart
import 'package:flutter/material.dart';
import 'api_service.dart';
import 'student.dart';

class StudentController extends ChangeNotifier {
  final ApiService apiService = ApiService();
  List<Student> _students = [];
  List<Student> get students => _students;

  // Fetch students from API
  Future<void> fetchStudents() async {
    try {
      _students = await apiService.fetchStudents();
      notifyListeners();
    } catch (e) {
      print('Error fetching students: $e');
    }
  }

  // Add a new student
  Future<void> addStudent(Student student) async {
    try {
      await apiService.addStudent(student);
      await fetchStudents();  // Refresh the list after adding
    } catch (e) {
      print('Error adding student: $e');
    }
  }

  // Update an existing student
  Future<void> updateStudent(Student student) async {
    try {
      await apiService.updateStudent(student);
      await fetchStudents();  // Refresh the list after update
    } catch (e) {
      print('Error updating student: $e');
    }
  }

  // Delete a student
  Future<void> deleteStudent(int id) async {
    try {
      await apiService.deleteStudent(id);
      await fetchStudents();  // Refresh the list after deleting
    } catch (e) {
      print('Error deleting student: $e');
    }
  }
}
```

### 4. **UI Page** (`student_page.dart`)

UI page mein aap data ko display karenge aur user actions (add, update, delete) handle karenge.

```dart
import 'package:flutter/material.dart';
import 'student_controller.dart';
import 'student.dart';
import 'package:provider/provider.dart';

class StudentPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (_) => StudentController(),
      child: Scaffold(
        appBar: AppBar(title: Text('Student Management')),
        body: Consumer<StudentController>(
          builder: (context, controller, child) {
            return ListView.builder(
              itemCount: controller.students.length,
              itemBuilder: (context, index) {
                final student = controller.students[index];
                return ListTile(
                  title: Text(student.name),
                  subtitle: Text('Age: ${student.age}'),
                  trailing: IconButton(
                    icon: Icon(Icons.delete),
                    onPressed: () async {
                      await controller.deleteStudent(student.id);
                    },
                  ),
                  onTap: () async {
                    // Implement update functionality here
                  },
                );
              },
            );
          },
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () async {
            // Implement add student functionality here
            final newStudent = Student(id: 0, name: 'New Student', age: 18);
            await context.read<StudentController>().addStudent(newStudent);
          },
          child: Icon(Icons.add),
        ),
      ),
    );
  }
}
```

### 5. **Main.dart** (`main.dart`)

Aapko `main.dart` mein application ko run karne ke liye `StudentPage` ko home page ke roop mein set karna hoga.

```dart
import 'package:flutter/material.dart';
import 'student_page.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Student App',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: StudentPage(),
    );
  }
}
```

### 6. **GitHub Notes Example**

Aap apne GitHub par notes is tarah likh sakte hain:

---

## Flutter API CRUD Operations Example

This repository contains an example of how to perform CRUD (Create, Read, Update, Delete) operations using Flutter and an external API.

### Structure

1. **Model**:

   * `student.dart`: Contains the `Student` class to handle student data.

2. **API Service**:

   * `api_service.dart`: Provides functions to interact with the API (GET, POST, PUT, DELETE).

3. **Controller**:

   * `student_controller.dart`: Handles business logic and updates the UI through the ChangeNotifier pattern.

4. **UI**:

   * `student_page.dart`: Displays the list of students and provides options to add, update, and delete students.

### Dependencies

* `http`: For making network requests.

### CRUD Operations

1. **Create**:

   * `addStudent(Student student)`: Adds a new student to the API.

2. **Read**:

   * `fetchStudents()`: Fetches the list of students from the API.

3. **Update**:

   * `updateStudent(Student student)`: Updates an existing student's details.

4. **Delete**:

   * `deleteStudent(int id)`: Deletes a student from the API by ID.

### Usage

1. Clone the repo: `git clone <repo-url>`
2. Run the app: `flutter run`

---

Is tarah aap apne notes ko organize kar sakte hain aur GitHub par share kar sakte hain.
