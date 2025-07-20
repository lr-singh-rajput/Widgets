Aapne jo mention kiya hai, uske hisaab se aapko API se data fetch karna hai aur us data ko filter karna hai. Ye kaafi common task hota hai jab aapko data ko display karna ho aur kisi condition ke basis pe filter karna ho.

Is example mein, hum **API** se data fetch karenge, **model** banayenge, **controller** ke through business logic ko handle karenge, aur **service** ke through API call karenge.

### **Approach:**

1. **Model**: Data structure ko define karenge jo API se aa raha hai.
2. **Controller**: Data ko manage karenge aur filter ko implement karenge.
3. **Service**: API calls ko manage karenge.
4. **UI**: Data ko display karenge aur filter options provide karenge.

### **Step-by-Step Implementation**

#### **Step 1: Define the Model**

Pehle hum ek model banayenge jisme jo data API se aayega, uska structure define hoga. Hum assume kar rahe hain ki API se kuch aise data aa raha hoga:

```json
[
  {
    "name": "John Doe",
    "father_name": "James Doe",
    "number": "1234567890",
    "email": "john.doe@example.com",
    "city": "New York",
    "country": "USA"
  },
  {
    "name": "Jane Smith",
    "father_name": "William Smith",
    "number": "0987654321",
    "email": "jane.smith@example.com",
    "city": "Los Angeles",
    "country": "USA"
  }
]
```

**Model (`User.dart`)**:

```dart
class User {
  final String name;
  final String fatherName;
  final String number;
  final String email;
  final String city;
  final String country;

  User({
    required this.name,
    required this.fatherName,
    required this.number,
    required this.email,
    required this.city,
    required this.country,
  });

  // Factory method to create a User object from JSON data
  factory User.fromJson(Map<String, dynamic> json) {
    return User(
      name: json['name'],
      fatherName: json['father_name'],
      number: json['number'],
      email: json['email'],
      city: json['city'],
      country: json['country'],
    );
  }
}
```

#### **Step 2: Create the Service Class**

Hum API se data fetch karenge `http` package ke through. Iske liye hum ek service class banaenge jo network calls ko handle karega.

**Service (`UserService.dart`)**:

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;
import 'User.dart';

class UserService {
  final String baseUrl = 'https://example.com/api/users'; // API URL

  // Fetch users from the API
  Future<List<User>> fetchUsers() async {
    try {
      final response = await http.get(Uri.parse(baseUrl));
      
      if (response.statusCode == 200) {
        List<dynamic> data = json.decode(response.body);
        // Convert JSON data to List of Users
        return data.map((userJson) => User.fromJson(userJson)).toList();
      } else {
        throw Exception('Failed to load users');
      }
    } catch (e) {
      throw Exception('Failed to load users: $e');
    }
  }
}
```

#### **Step 3: Controller for Managing State and Filter Logic**

Controller mein hum `UserService` se data fetch karenge aur filtering ko handle karenge. Hum state ko manage karenge jaise ki selected filter.

**Controller (`UserController.dart`)**:

```dart
import 'package:get/get.dart';
import 'User.dart';
import 'UserService.dart';

class UserController extends GetxController {
  var users = <User>[].obs; // Observable list to hold users
  var filteredUsers = <User>[].obs; // Observable list to hold filtered users
  var isLoading = false.obs;

  // Fetch users and apply initial filter
  Future<void> fetchUsers() async {
    isLoading(true);
    try {
      var fetchedUsers = await UserService().fetchUsers();
      users.value = fetchedUsers; // Update users list
      filteredUsers.value = fetchedUsers; // Initially, show all users
    } catch (e) {
      print("Error: $e");
    } finally {
      isLoading(false);
    }
  }

  // Filter users based on name, city, or country
  void filterUsers(String query) {
    if (query.isEmpty) {
      filteredUsers.value = users; // Show all users if query is empty
    } else {
      filteredUsers.value = users.where((user) {
        return user.name.toLowerCase().contains(query.toLowerCase()) ||
               user.city.toLowerCase().contains(query.toLowerCase()) ||
               user.country.toLowerCase().contains(query.toLowerCase());
      }).toList(); // Filter users based on query
    }
  }
}
```

#### **Step 4: Create the UI with Filtering Options**

UI mein hum `TextField` denge jisme user search query dal sakta hai aur filtered data `ListView.builder` ke through show karenge.

**UI (`UserScreen.dart`)**:

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';
import 'UserController.dart';

class UserScreen extends StatelessWidget {
  final UserController userController = Get.put(UserController());

  @override
  Widget build(BuildContext context) {
    // Fetch the users when the screen is loaded
    userController.fetchUsers();

    return Scaffold(
      appBar: AppBar(
        title: Text('Users List'),
      ),
      body: Column(
        children: [
          // Search bar to filter users
          Padding(
            padding: const EdgeInsets.all(8.0),
            child: TextField(
              onChanged: (value) {
                userController.filterUsers(value); // Call the filter function on text change
              },
              decoration: InputDecoration(
                labelText: 'Search by name, city, or country',
                border: OutlineInputBorder(),
                suffixIcon: Icon(Icons.search),
              ),
            ),
          ),
          
          // Show loading indicator while fetching users
          Obx(() {
            if (userController.isLoading.value) {
              return Center(child: CircularProgressIndicator());
            } else {
              return Expanded(
                child: Obx(() {
                  return ListView.builder(
                    itemCount: userController.filteredUsers.length,
                    itemBuilder: (context, index) {
                      var user = userController.filteredUsers[index];
                      return ListTile(
                        title: Text(user.name),
                        subtitle: Text("${user.city}, ${user.country}"),
                      );
                    },
                  );
                }),
              );
            }
          })
        ],
      ),
    );
  }
}
```

### **Explanation of Each Part**:

#### **1. Model (`User.dart`)**:

* **User Model**: Model class hai jo API se aane wale data ko define karta hai. `fromJson` method use kiya gaya hai jisse JSON data ko `User` object mein convert kiya jata hai.

#### **2. Service (`UserService.dart`)**:

* **fetchUsers()**: Hum `http.get` method ka use kar rahe hain API call ke liye. Agar response successful hota hai, toh hum response data ko JSON se parse kar ke list of `User` objects mein convert kar lete hain.

#### **3. Controller (`UserController.dart`)**:

* **fetchUsers()**: Ye method `UserService` ko call karta hai aur users ko fetch kar ke store karta hai. Fetching ke baad hum `filteredUsers` ko initially same set kar dete hain (i.e., sab users).
* **filterUsers()**: Ye function `query` ke basis par users ko filter karta hai. Agar query empty hai, toh sab users dikhenge. Agar kuch likha gaya hai, toh woh name, city, ya country ke basis par filter hota hai.

#### **4. UI (`UserScreen.dart`)**:

* **TextField**: Ye search bar user ko allow karta hai query type karne ke liye. Jab user kuch type karta hai, `filterUsers()` function call hota hai aur filtered list update hoti hai.
* **ListView\.builder**: Jab users load ho jate hain, tab ye widget filtered list ko display karta hai.
* **Obx**: Ye reactive state management ka part hai. Hum `GetX` ko use kar rahe hain to update UI reactively jab `filteredUsers` ya `isLoading` ki value change hoti hai.

### **Conclusion**:

Is example mein, humne API se data fetch karne ke liye `http` package ka use kiya, data ko model mein map kiya, aur `GetX` ko use karke state management handle kiya. Humne `ListView.builder` ko filter ke saath implement kiya, jisme user kisi bhi query ke basis par filter kar sakta hai.

Agar aapko koi part clear nahi ho, ya aur kuch chahiye ho, toh zarur batayein!
