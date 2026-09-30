#  Android Activity Lifecycle & Basic UI

An Android application developed using **Kotlin** to demonstrate basic UI development with `ConstraintLayout` and `TextView`, along with the **Activity Lifecycle** using Logcat and Toast messages.

---

## 🎯 Aim

To create an Android application to demonstrate the functions of the **Activity Life Cycle** and **Basic UI**.

The application demonstrates:

* Basic Android UI
* `ConstraintLayout`
* `TextView`
* Android built-in colors
* TextView properties
* Activity Lifecycle methods
* Log messages in Logcat
* Toast messages
* View IDs
* Edge-to-edge UI and system window insets

---

## 🛠️ Technologies Used

* **Language:** Kotlin
* **Platform:** Android
* **UI:** XML
* **IDE:** Android Studio
* **Layout:** ConstraintLayout
* **Activity:** AppCompatActivity

---

## 📚 Study / Concepts Covered

This practical covers:

* TextView and its properties
* Toast Message
* Snackbar Message
* Android built-in resources such as colors
* Activity Life Cycle
* Log Message in Logcat
* Properties of `ConstraintLayout`
* Generating an ID for a TextView

---

# 🎨 Basic UI

The application uses `ConstraintLayout` as the root layout.

The layout is configured with:

```xml
android:layout_width="match_parent"
android:layout_height="match_parent"
android:background="#FFFF00"
```

Therefore, the Activity uses a **yellow background**.

The root layout also has the ID:

```xml
android:id="@+id/main"
```

This ID is used by the Kotlin Activity to access the layout.

---

# 📝 TextView

The `activity_main.xml` file contains a `TextView` used to display the text **"hello world"**.

```xml
<TextView
    android:id="@+id/id"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginTop="356dp"
    android:layout_marginEnd="156dp"
    android:text="hello world"
    android:textSize="27sp"
    android:background="#ffff00"
    android:textColor="@android:color/holo_blue_bright"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintTop_toTopOf="parent" />
```

## TextView Properties

| Property   | Value                             | Description                             |
| ---------- | --------------------------------- | --------------------------------------- |
| ID         | `@+id/id`                         | Generates an ID for the TextView        |
| Width      | `wrap_content`                    | Width is based on the content           |
| Height     | `wrap_content`                    | Height is based on the content          |
| Text       | `hello world`                     | Text displayed in the TextView          |
| Text Size  | `27sp`                            | Sets the text size                      |
| Text Color | `@android:color/holo_blue_bright` | Uses Android's built-in Holo Blue color |
| Background | `#ffff00`                         | Yellow background                       |
| Top Margin | `356dp`                           | Sets the top margin                     |
| End Margin | `156dp`                           | Sets the end margin                     |

---

# 🔄 Activity Life Cycle

The Android Activity Lifecycle consists of several callback methods that are called as the Activity changes between different states.

The `LoginActivity` demonstrates the following lifecycle methods:

```text
onCreate()
    ↓
onStart()
    ↓
onResume()
    ↓
Activity Running
    ↓
onPause()
    ↓
onStop()
    ↓
onDestroy()
```

When an Activity that has been stopped is started again:

```text
onRestart()
    ↓
onStart()
    ↓
onResume()
```

---

## Lifecycle Methods Implemented

### `onCreate()`

Called when the Activity is created.

The implementation:

* Enables edge-to-edge display
* Loads `activity_login`
* Applies system-bar insets
* Calls the `display()` function

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)

    enableEdgeToEdge()
    setContentView(R.layout.activity_login)

    ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main)) { v, insets ->
        val systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars())

        v.setPadding(
            systemBars.left,
            systemBars.top,
            systemBars.right,
            systemBars.bottom
        )

        insets
    }

    display("onCreate method is called")
}
```

---

### `onStart()`

Called when the Activity becomes visible.

```kotlin
override fun onStart() {
    display("onStart method is called")
    super.onStart()
}
```

---

### `onResume()`

Called when the Activity enters the foreground and becomes ready for user interaction.

```kotlin
override fun onResume() {
    display("onResume method is called ")
    super.onResume()
}
```

---

### `onPause()`

Called when the Activity is no longer in the foreground or is partially obscured.

```kotlin
override fun onPause() {
    display("onPause method is called")
    super.onPause()
}
```

---

### `onStop()`

Called when the Activity is no longer visible.

```kotlin
override fun onStop() {
    display("onStop method is called ")
    super.onStop()
}
```

---

### `onRestart()`

Called when a previously stopped Activity is started again.

```kotlin
override fun onRestart() {
    display("onRestart method is called ")
    super.onRestart()
}
```

---

### `onDestroy()`

Called when the Activity is being destroyed.

```kotlin
override fun onDestroy() {
    display("onDestroy method is called ")
    super.onDestroy()
}
```

---

# 🪵 Logcat

The application uses Android's `Log` class to print Activity Lifecycle messages to **Logcat**.

A tag is defined for the Activity:

```kotlin
val TAG = "LoginActivity"
```

The lifecycle messages are printed using:

```kotlin
Log.i(TAG, msg)
```

For example:

```text
onCreate method is called
onStart method is called
onResume method is called
```

These messages can be viewed in **Android Studio → Logcat**.

---

# 🍞 Toast Message

The application uses a Toast message to display lifecycle information temporarily on the screen.

The Toast is implemented inside the `display()` function:

```kotlin
Toast.makeText(this, msg, Toast.LENGTH_SHORT).show()
```

The complete function is:

```kotlin
fun display(msg: String) {
    Log.i(TAG, msg)
    Toast.makeText(this, msg, Toast.LENGTH_SHORT).show()
}
```

This function allows the same lifecycle message to be sent to both **Logcat** and a **Toast**.

For example:

```text
onCreate method is called
```

is displayed through Toast and also recorded in Logcat.

---

# 🖥️ MainActivity

The `MainActivity` loads `activity_main.xml`.

```kotlin
class MainActivity : AppCompatActivity() {

    val TAG = "MainActivity"

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        enableEdgeToEdge()
        setContentView(R.layout.activity_main)

        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main)) { v, insets ->
            val systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars())

            v.setPadding(
                systemBars.left,
                systemBars.top,
                systemBars.right,
                systemBars.bottom
            )

            insets
        }

        Log.i(TAG, "onCreate: Method is called!!")
    }
}
```

The Activity:

1. Calls `super.onCreate()`
2. Enables edge-to-edge display
3. Loads `activity_main.xml`
4. Handles system-bar insets
5. Prints an `onCreate` message to Logcat

---

# 🔐 LoginActivity

`LoginActivity` loads the `activity_login.xml` layout.

It demonstrates the complete set of lifecycle callbacks implemented in the project:

```text
onCreate()
onStart()
onResume()
onPause()
onStop()
onRestart()
onDestroy()
```

Each lifecycle callback calls the `display()` function, which sends the message to:

* Logcat
* Toast

---

# 📱 Activity Layout

The project contains two layouts:

```text
res/
└── layout/
    ├── activity_main.xml
    └── activity_login.xml
```

### `activity_main.xml`

Contains the `TextView` demonstrating the basic UI requirements.

### `activity_login.xml`

Contains the yellow `ConstraintLayout` used by `LoginActivity`.

```xml
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#FFFF00"
    tools:context=".LoginActivity">
</androidx.constraintlayout.widget.ConstraintLayout>
```

---

# 📂 Project Structure

```text
24012021096_MAD_PR2/
│
├── app/
│   └── src/
│       └── main/
│           ├── java/
│           │   └── com/example/a24012021096_mad_pr2/
│           │       ├── MainActivity.kt
│           │       └── LoginActivity.kt
│           │
│           └── res/
│               └── layout/
│                   ├── activity_main.xml
│                   └── activity_login.xml
│
└── README.md
```

---

# ▶️ How to Run

1. Open the project in **Android Studio**.
2. Wait for Gradle synchronization to complete.
3. Connect an Android device or start an Android Emulator.
4. Click **Run ▶**.
5. Select the required device.
6. Observe the application UI.
7. Open **Logcat** in Android Studio to observe lifecycle messages.
8. Interact with the Activity or change its state to observe lifecycle callbacks and Toast messages.

---

# 🔍 Observing the Activity Lifecycle

The lifecycle can be observed by performing actions such as:

### Launching the Activity

Typical callbacks include:

```text
onCreate
onStart
onResume
```

### Moving the Activity to the background

Callbacks can include:

```text
onPause
onStop
```

### Returning to the Activity

Callbacks can include:

```text
onRestart
onStart
onResume
```

### Destroying the Activity

The Activity can eventually call:

```text
onDestroy
```

The exact lifecycle sequence can depend on how the Activity state changes and how Android manages the application.

---

# 🧩 Android Built-in Color Resource

The TextView uses the Android framework's built-in Holo Blue color:

```xml
android:textColor="@android:color/holo_blue_bright"
```

This demonstrates the use of an **Android built-in resource** rather than defining the color manually.

The Activity background uses:

```xml
android:background="#FFFF00"
```

which represents yellow.

---

# 🪟 Edge-to-Edge and Window Insets

Both Activities use:

```kotlin
enableEdgeToEdge()
```

and apply system window insets using:

```kotlin
ViewCompat.setOnApplyWindowInsetsListener(...)
```

The system bar insets are obtained using:

```kotlin
insets.getInsets(WindowInsetsCompat.Type.systemBars())
```

and applied as padding to the root layout.

This helps the layout account for system UI areas such as the status bar and navigation area.

---

# ⚠️ Implementation Notes

The current implementation differs from a few details in the stated practical requirements:

* The TextView currently displays **`hello world`** rather than **`Hello World`**.
* `android:textStyle="bold|italic"` is not currently present in `activity_main.xml`.
* The TextView is positioned using fixed margins rather than constraints that explicitly center it horizontally and vertically.
* The provided Kotlin implementation demonstrates **Logcat and Toast**, but no Snackbar implementation was provided.
* `LoginActivity` loads `activity_login.xml`, while `MainActivity` loads `activity_main.xml`.

These points reflect the code provided for this project.

---

# 📖 Concepts Learned

| Concept                | Demonstrated Through                      |
| ---------------------- | ----------------------------------------- |
| ConstraintLayout       | `activity_main.xml`, `activity_login.xml` |
| TextView               | `activity_main.xml`                       |
| TextView ID            | `@+id/id`                                 |
| Text Size              | `27sp`                                    |
| Android Built-in Color | `holo_blue_bright`                        |
| Yellow Background      | `#FFFF00`                                 |
| Activity Lifecycle     | `LoginActivity`                           |
| Logcat                 | `Log.i()`                                 |
| Toast                  | `Toast.makeText()`                        |
| Edge-to-Edge UI        | `enableEdgeToEdge()`                      |
| Window Insets          | `ViewCompat` / `WindowInsetsCompat`       |
| Kotlin Activity        | `MainActivity`, `LoginActivity`           |

---

# ✅ Conclusion

This practical demonstrates fundamental Android application development using **Kotlin and XML**.

The project covers basic UI creation using `ConstraintLayout` and `TextView`, Android resource usage, Activity Lifecycle callbacks, Logcat messages, Toast notifications, and edge-to-edge window handling.

The Activity Lifecycle implementation provides a practical understanding of how Android Activities transition through states such as creation, starting, resuming, pausing, stopping, restarting, and destruction.
