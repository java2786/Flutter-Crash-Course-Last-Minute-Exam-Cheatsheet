# Flutter-Crash-Course-Last-Minute-Exam-Cheatsheet


## Flutter Full Cheatsheet & Theory Notes
### 1. Introduction to Flutter
- Flutter: Open-source UI toolkit by Google.
- Write once, run everywhere: Android, iOS, Web, Windows, macOS, Linux.
- Language: Dart (OOP, sound null safety).
- Uses: Mobile apps, web apps, desktop apps.
- Rendering Engine: Skia (renders everything on canvas).
- Hot Reload: Instantly see code changes without restarting the app.
### 2. Flutter App Structure
- main.dart: App’s entry point.
- MaterialApp: Root of the widget tree, provides navigation, themes, routes.
- **Common Folders**:
    - *models/*: Dart data classes.
    - *screens/*: Page-wise UI.
    - *widgets/*: Reusable UI components.
    - *services/*: Business logic (APIs, local DB, etc.).
    - *providers/*: State management (Provider, Riverpod).
    - *utils/*: Constants, validators, helpers.
### 3. Widgets Overview
#### StatelessWidget
- Static UI, no state changes.
```dart
class Hello extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Text('Hi!');
  }
}
```
#### StatefulWidget
- Dynamic UI that changes based on user interaction.
```dart
class Counter extends StatefulWidget {
  @override
  _CounterState createState() => _CounterState();
}
class _CounterState extends State<Counter> {
  int count = 0;
  void increment() => setState(() => count++);
}
```
- StatefulWidget lifecycle methods:
```plaintext
initState() → build() → didUpdateWidget() → dispose()
```
### 4. Navigation in Flutter
- Basic:
```dart
Navigator.push(context, MaterialPageRoute(builder: (_) => NextPage()));
Navigator.pop(context);
```
- Named routes:
```dart
Navigator.pushNamed(context, '/home');
```
- Advanced:
    - Use go_router, auto_route, or GetX for nested and deep linking.

### 5. State Management Techniques
- **setState()**: For local widget state.
- **Provider**: InheritedWidget wrapper for simple state. Recommended for beginners.
- **Riverpod**: Modern, testable version of Provider.
- **BLoC (flutter_bloc)**: Stream-based, separates logic from UI. Clean architecture with Streams.
- **GetX**: All-in-one (state, routes, DI). Lightweight state, route, and dependency management.
- **Use cases**:
    - Auth state
    - Theme toggling
    - Cart/Bookmarks
    - Form inputs
    - Quiz answers

### 6. Firebase Authentication
- Add packages:
```yaml
firebase_core: ^latest
firebase_auth: ^latest
```
- Initialize Firebase:
```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}
```
- Signup/Login:
```dart
await FirebaseAuth.instance.createUserWithEmailAndPassword(...);
await FirebaseAuth.instance.signInWithEmailAndPassword(...);
```
- Logout:
```dart
await FirebaseAuth.instance.signOut();
```
- Session Check:
```dart
FirebaseAuth.instance.authStateChanges().listen(...)
```
### 7. Shared Preferences (Local Storage)
- Lightweight key-value data storage.
```dart
final prefs = await SharedPreferences.getInstance();
prefs.setBool('isLoggedIn', true);
```
- Use cases:
    - Dark mode
    - Auth token
    - Bookmarks
    - Quiz score cache
### 8. HTTP & API Integration
- Add:
```yaml
http: ^latest
```
- Call API:
```dart
final response = await http.get(Uri.parse('http://localhost:3000/courses'));
```
- Decode JSON:
```dart
final data = jsonDecode(response.body);
```

- Error Handling (Critical for APIs)
  - try-catch with http and async/await.

### 9. Form Handling & Validation
- Use Form, TextFormField, and a GlobalKey<FormState>:
```dart
final _formKey = GlobalKey<FormState>();
Form(
  key: _formKey,
  child: TextFormField(
    validator: (value) => value!.isEmpty ? 'Required' : null,
  ),
);
```
### 10. Project Features to Practice
- Login & Signup using Firebase
- Course listing + details (with REST API)
- Add/update/delete user data (CRUD)
- Quiz with scores & summary
- Bookmarks using Provider + Shared Preferences
- Theme switcher (dark/light)

### 11. Themes & Dark Mode
- In MaterialApp:
```dart
theme: ThemeData.light(),
darkTheme: ThemeData.dark(),
themeMode: ThemeMode.system,
```
- Save theme mode using Shared Preferences.

### 12. Quiz Implementation Logic
- Fetch MCQs from API or local JSON.
- Track selected options.
- Show summary and score.
- Store result in local DB or remote API.

### 13. ListView & GridView
```dart
ListView.builder(
  itemCount: items.length,
  itemBuilder: (_, i) => Text(items[i]),
);
```
```dart
GridView.count(
  crossAxisCount: 2,
  children: [...],
);
```

### 14. Reusable Widgets Example
```dart
class AppButton extends StatelessWidget {
  final String label;
  final VoidCallback onTap;
  AppButton({required this.label, required this.onTap});
  ...
}
```
### 15. Error Handling
```dart
try {
  final res = await http.get(...);
} catch (e) {
  print('Failed: $e');
}
```
- Use ScaffoldMessenger for SnackBars.
- Graceful handling of no-internet using connectivity_plus.

### 16. Testing Basics
- Use flutter_test and mockito.
```bash
flutter test
```
- Widget test example:
```dart
testWidgets('Check login screen UI', (tester) async {
  await tester.pumpWidget(MyApp());
  expect(find.text('Login'), findsOneWidget);
});
```
### 17. Clean Architecture (Optional)
- *data/*: remote/local data handling.
- *domain/*: models + use cases.
- *presentation/*: UI + state.
- Follow MVVM or layered architecture.

### 18. Best Practices Summary
- Use const constructors where possible.
- Avoid hardcoded values → use constants file.
- Use late final for non-null variables.
- Separate logic from UI.
- Use formatter & linter rules.
- Break widgets into small parts.
- Document important functions.
- Always dispose controllers (e.g., TextEditingController, ScrollController).

### Final Revision Tips for Exams
- Understand widget lifecycle.
- Practice basic UI layout using Row/Column/Stack/ListView.
- Implement at least 1 complete project with login, listing, CRUD, and quiz.
- Be ready to explain setState, Provider, and Firebase Auth.
- Learn how to handle APIs and errors.
- Practice theme switch + local storage.
