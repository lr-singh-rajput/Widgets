Bilkul! Main aapko detail me samjhaata hoon ki Flutter me checkbox (ya kisi box-type widget) ke click hone par kaise kisi aur widget ko enable/disable kiya jaata hai – jaise ki **form field ya button**.

Isme hum Flutter ka **Checkbox**, **TextField** aur **ElevatedButton** use karenge. Main niche ek full working example de raha hoon, **step by step explanation aur comments ke sath**, jise aap **notes** bana sakte ho.

---

## ✅ Target:

* Ek **checkbox** banayenge.
* Jab tak user checkbox **tick nahi karega**, tab tak:

  * Text field **disable** rahegi.
  * Submit button **disable** rahega.
* Jaise hi user checkbox tick karega:

  * Text field aur button **enable** ho jayenge.

---

## 🧠 Concepts Used:

1. **StatefulWidget** – kyunki state (checkbox ka status) change hoti hai.
2. **bool variable** – checkbox ke liye.
3. **setState()** – UI ko update karne ke liye.

---

## ✅ Full Example Code with Comments:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

// Hamara main widget jisme UI banayenge
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Checkbox Enable/Disable Example',
      home: CheckboxExample(), // Home screen hamara custom StatefulWidget hoga
    );
  }
}

// Hamara StatefulWidget jisme checkbox, text field aur button honge
class CheckboxExample extends StatefulWidget {
  @override
  _CheckboxExampleState createState() => _CheckboxExampleState();
}

class _CheckboxExampleState extends State<CheckboxExample> {
  // Ye variable checkbox ke state ko store karega (checked ya not)
  bool isChecked = false;

  // TextField ke liye ek controller
  final TextEditingController _controller = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Form Control with Checkbox'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(20.0),
        child: Column(
          children: [
            /// ✅ Checkbox Widget
            Row(
              children: [
                Checkbox(
                  value: isChecked,
                  onChanged: (bool? value) {
                    // Jab checkbox click hoga, setState se UI update karenge
                    setState(() {
                      isChecked = value ?? false;
                    });
                  },
                ),
                Text('I agree to the terms'),
              ],
            ),

            SizedBox(height: 20),

            /// ✅ TextField - sirf tab enable jab checkbox tick ho
            TextField(
              controller: _controller,
              enabled: isChecked, // Checkbox ke value par depend karta hai
              decoration: InputDecoration(
                labelText: 'Enter your name',
                border: OutlineInputBorder(),
              ),
            ),

            SizedBox(height: 20),

            /// ✅ Submit Button - sirf tab enable jab checkbox tick ho
            ElevatedButton(
              onPressed: isChecked
                  ? () {
                      // Agar checkbox tick hai, tabhi ye function chalega
                      String name = _controller.text;
                      ScaffoldMessenger.of(context).showSnackBar(
                        SnackBar(content: Text('Submitted: $name')),
                      );
                    }
                  : null, // Agar checkbox unticked hai, button disabled rahega
              child: Text('Submit'),
            ),
          ],
        ),
      ),
    );
  }
}
```

---

## 📝 Explanation / Notes (Aap Copy kar sakte ho):

### ✅ `Checkbox`:

* Checkbox ek bool value rakhta hai (`true` ya `false`).
* Jab user checkbox par click karta hai, hum `onChanged` function ke andar `setState()` use karte hain taaki UI update ho jaye.

```dart
Checkbox(
  value: isChecked,
  onChanged: (bool? value) {
    setState(() {
      isChecked = value ?? false;
    });
  },
)
```

### ✅ `TextField` Enable/Disable:

* `enabled: isChecked` likhne se, ye field sirf tab enable hoti hai jab checkbox tick hota hai.

### ✅ `ElevatedButton` Enable/Disable:

* Agar `onPressed` null diya gaya hai, to button automatically disabled ho jata hai.
* Jab checkbox tick hota hai, tabhi `onPressed` me function milta hai.

```dart
onPressed: isChecked ? () { ... } : null
```

---

## 📌 Summary:

| Widget    | Control Condition        | Enabled when     |
| --------- | ------------------------ | ---------------- |
| Checkbox  | User interaction         | Always           |
| TextField | `enabled: isChecked`     | isChecked = true |
| Button    | `onPressed: isChecked ?` | isChecked = true |

---

Agar tum chaho to me isme aur bhi functionality add kar sakta hoon, jaise validation, dialog box, ya checkbox ke jagah switch use karna.

Agar tum chaho to me ye notes **PDF format** me bhi likh ke de sakta hoon. Let me know.
