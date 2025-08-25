Flutter mein `TabBar` ek bohot useful widget hai jab aapko ek screen pe multiple tabs dikhani hoti hain. Har tab alag-alag content ko display karta hai, aur user ko tab switch karne ka option milta hai.

Yeh `TabBar` ko aap `TabController` ke saath use karte hain, jo tab ke selection aur content ko manage karta hai. Aap `TabBar` ko `AppBar` ke andar ya alag se bhi use kar sakte hain.

### Example: Simple TabBar in Flutter with Comments

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: TabBarExample(),
    );
  }
}

class TabBarExample extends StatefulWidget {
  @override
  _TabBarExampleState createState() => _TabBarExampleState();
}

class _TabBarExampleState extends State<TabBarExample> with SingleTickerProviderStateMixin {
  // TabController ka use karna hoga TabBar aur TabBarView ko sync karne ke liye.
  late TabController _tabController;

  @override
  void initState() {
    super.initState();
    // TabController initialize karte hain, jisme tab count aur vsync parameter ko pass karte hain.
    _tabController = TabController(length: 3, vsync: this); 
  }

  @override
  void dispose() {
    _tabController.dispose(); // TabController ko dispose karte hain jab screen close ho.
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("TabBar Example"),
        // TabBar ko AppBar mein add karte hain.
        bottom: TabBar(
          controller: _tabController, // TabController ko link karte hain TabBar ke saath.
          tabs: [
            Tab(text: "Tab 1"), // First Tab
            Tab(text: "Tab 2"), // Second Tab
            Tab(text: "Tab 3"), // Third Tab
          ],
        ),
      ),
      // TabBarView ko use karte hain jisme har tab ka content display karte hain.
      body: TabBarView(
        controller: _tabController, // TabController ko link karte hain TabBarView ke saath.
        children: [
          Center(child: Text('Content of Tab 1')), // Content for Tab 1
          Center(child: Text('Content of Tab 2')), // Content for Tab 2
          Center(child: Text('Content of Tab 3')), // Content for Tab 3
        ],
      ),
    );
  }
}
```

### **Explanation with Comments:**

1. **Stateful Widget**:

   * `TabBarExample` ko ek `StatefulWidget` banaya gaya hai, kyunki hum tab selection ke state ko manage kar rahe hain.
   * `State` class (`_TabBarExampleState`) ko `SingleTickerProviderStateMixin` ke saath mix kiya gaya hai taaki tab animation ke liye ek **vsync** provide kiya ja sake.

2. **TabController**:

   * **`TabController`**: Yeh controller `TabBar` aur `TabBarView` ko sync karta hai. Isme tab count (`length`) aur `vsync` parameter dene padte hain.
   * **vsync**: `vsync` ek animation controller ka part hota hai, jo tab switching ke animations ko smooth banata hai. Hum yahan `SingleTickerProviderStateMixin` ka use karte hain jo automatically **vsync** provide karta hai.

3. **TabBar in AppBar**:

   * `TabBar` ko `AppBar` ke `bottom` property mein add kiya gaya hai.
   * **tabs**: Yeh ek list hai jisme aap har tab ka content define karte hain. Hum yahan simple text tabs bana rahe hain (`Tab 1`, `Tab 2`, `Tab 3`).

4. **TabBarView**:

   * `TabBarView` ko `body` ke andar set kiya gaya hai. Yeh widget tab ke selected index ke basis pe content dikhata hai.
   * Har tab ke liye ek `Center` widget hai jisme simple text display ho raha hai. Aap yahan apne custom widgets ya content daal sakte hain.

5. **Lifecycle Management**:

   * `initState()`: TabController ko initialize karte hain.
   * `dispose()`: TabController ko properly dispose karte hain jab widget destroy ho, taaki memory leaks na ho.

### **Customization**:

* **Tab Indicator**: Aap tab ka indicator (active tab ka underline) customize kar sakte hain. Jaise color ya height change karna.

  ```dart
  TabBar(
    indicatorColor: Colors.blue, // Tab indicator ka color set karte hain
    indicatorWeight: 4, // Tab indicator ki height set karte hain
    ...
  );
  ``

* **Tab Bar Styling**: Tab bar ka background color aur text style bhi customize kiya ja sakta hai.

  ```dart
  TabBar(
    labelColor: Colors.white, // Tab label ka color set karte hain
    unselectedLabelColor: Colors.grey, // Unselected tabs ka color set karte hain
    backgroundColor: Colors.teal, // TabBar ka background color set karte hain
    ...
  );
  ```

### **Final Output**:

Aapko ek screen milega jisme upar ek `TabBar` hoga (3 tabs ke saath). Har tab par click karne par niche ek `TabBarView` dikhega jisme har tab ka content alag dikhega.

### **Other Tab Bar Customizations**:

* **Scrollable Tabs**: Agar tabs ki number bohot zyada ho, toh `TabBar` ko scrollable bana sakte hain.

  ```dart
  TabBar(
    isScrollable: true, // Tabs ko horizontally scrollable bana deta hai
    ...
  );
  ```

* **Icons in Tabs**: Aap tab labels ke jagah icons bhi use kar sakte hain.

  ```dart
  Tab(
    icon: Icon(Icons.home), // Icon tab ke liye
  );
  ```

Agar aapko aur kisi customization ya feature ka example chahiye ho toh bataiye!
