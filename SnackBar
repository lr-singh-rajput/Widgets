Bilkul! Flutter ke andar **SnackBar** ek transient (temporary) message hota hai jo screen ke bottom par show hota hai. Yeh kisi action ke response me user ko feedback dene ke liye use hota hai — jaise form submit karna, delete karna, ya koi error batana.

Main aapko **SnackBar ke related detailed notes** de raha hoon, jisme code, explanation, aur saare important widgets ka zikr hoga.

---

### 🔸 **Flutter SnackBar - Detailed Notes**

---

## ✅ 1. What is a SnackBar?

> A **SnackBar** is a lightweight message that briefly appears at the bottom of the screen to provide user feedback.

* Transient feedback (temporary)
* Disappears after a few seconds (default: 4 seconds)
* Can have actions (like "UNDO")

---

## 🧱 2. Basic Structure of a SnackBar

```dart
final snackBar = SnackBar(
  content: Text('This is a SnackBar'),
);

ScaffoldMessenger.of(context).showSnackBar(snackBar);
```

---

## 🧰 3. SnackBar Widgets & Properties

| Property          | Description                                                               |
| ----------------- | ------------------------------------------------------------------------- |
| `content`         | **Required**. Main message inside the SnackBar. Usually a `Text` widget.  |
| `action`          | Adds an optional action button (e.g., "UNDO"). Uses `SnackBarAction`.     |
| `duration`        | Time for which SnackBar is visible. Default is 4 seconds.                 |
| `backgroundColor` | Sets background color of SnackBar.                                        |
| `behavior`        | Defines the positioning of the SnackBar. `fixed` (default) or `floating`. |
| `shape`           | Sets shape (e.g., rounded corners) using `RoundedRectangleBorder`.        |
| `margin`          | Sets margin around the SnackBar (only works with `floating` behavior).    |
| `elevation`       | Shadow behind the SnackBar.                                               |

---

## 🎨 4. SnackBar with All Features

```dart
final snackBar = SnackBar(
  content: Text('Item deleted'),
  action: SnackBarAction(
    label: 'UNDO',
    onPressed: () {
      // Some code to undo the change
    },
    textColor: Colors.yellow,
  ),
  duration: Duration(seconds: 3),
  backgroundColor: Colors.black87,
  behavior: SnackBarBehavior.floating,
  shape: RoundedRectangleBorder(
    borderRadius: BorderRadius.circular(10),
  ),
  margin: EdgeInsets.all(16),
  elevation: 10,
);

ScaffoldMessenger.of(context).showSnackBar(snackBar);
```

---

## ⚙️ 5. How to Show SnackBar

> Use `ScaffoldMessenger.of(context)` instead of `Scaffold.of(context)` (old way, now deprecated).

### ✅ Correct Way:

```dart
ScaffoldMessenger.of(context).showSnackBar(snackBar);
```

### ❌ Old Way (Don't Use):

```dart
Scaffold.of(context).showSnackBar(snackBar); // Deprecated
```

---

## 📚 6. Common Use Case Example

```dart
ElevatedButton(
  onPressed: () {
    final snackBar = SnackBar(
      content: Text('You pressed the button!'),
      action: SnackBarAction(
        label: 'DISMISS',
        onPressed: () {},
      ),
    );

    ScaffoldMessenger.of(context).showSnackBar(snackBar);
  },
  child: Text('Show SnackBar'),
)
```

---

## 📝 7. Notes Summary (for Copy in Notebook)

* ✅ `SnackBar` is used for temporary messages.
* 📌 Always use `ScaffoldMessenger.of(context).showSnackBar(...)`.
* 💡 Use `SnackBarAction` to add interactive actions like "UNDO".
* 🎨 Customize using `backgroundColor`, `shape`, `margin`, `behavior`, etc.
* 🧪 Use `SnackBarBehavior.floating` for modern, rounded design.

---

Agar aap chaho toh main isse **PDF ya printable notes** format me bhi bana sakta hoon. Batao agar chahiye.
