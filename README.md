
# Flutter Firebase Authentication

This Flutter project demonstrates how to implement Firebase Authentication using email and password login and registration.

## Features

- Firebase email and password authentication
- User login
- User registration

## Requirements

- Flutter SDK
- Firebase account

## Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/flutter-firebase-auth.git
cd flutter-firebase-auth
```

### 2. Install Dependencies

Open a terminal in the project directory and run:

```bash
flutter pub get
```

### 3. Firebase Configuration

1. Go to the [Firebase Console](https://console.firebase.google.com/).
2. Create a new project or use an existing project.
3. Add an Android app to your Firebase project. Follow the steps to download the `google-services.json` file.
4. Place the `google-services.json` file in the `android/app` directory.

### 4. Update `pubspec.yaml`

Ensure the following dependencies are included in your `pubspec.yaml`:

```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^2.10.1
  firebase_auth: ^4.9.0
```

Run the following command to get the dependencies:

```bash
flutter pub get
```

### 5. Firebase Initialization

In your `main.dart` file, initialize Firebase:

```dart
import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';
import 'firebase_options.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(
    options: DefaultFirebaseOptions.currentPlatform,
  );
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Firebase Auth',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: LoginScreen(),
    );
  }
}
```

### 6. Create Login Screen

Create a new file `login_screen.dart` and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:firebase_auth/firebase_auth.dart';

class LoginScreen extends StatefulWidget {
  @override
  _LoginScreenState createState() => _LoginScreenState();
}

class _LoginScreenState extends State<LoginScreen> {
  final TextEditingController _emailController = TextEditingController();
  final TextEditingController _passwordController = TextEditingController();
  final FirebaseAuth _auth = FirebaseAuth.instance;

  void _login() async {
    try {
      UserCredential userCredential = await _auth.signInWithEmailAndPassword(
        email: _emailController.text.trim(),
        password: _passwordController.text.trim(),
      );
      print('Successfully logged in: ${userCredential.user}');
    } on FirebaseAuthException catch (e) {
      print('Failed to sign in: $e');
    }
  }

  void _register() async {
    try {
      UserCredential userCredential = await _auth.createUserWithEmailAndPassword(
        email: _emailController.text.trim(),
        password: _passwordController.text.trim(),
      );
      print('Successfully registered: ${userCredential.user}');
    } on FirebaseAuthException catch (e) {
      print('Failed to register: $e');
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Login'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            TextField(
              controller: _emailController,
              decoration: InputDecoration(labelText: 'Email'),
            ),
            TextField(
              controller: _passwordController,
              decoration: InputDecoration(labelText: 'Password'),
              obscureText: true,
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: _login,
              child: Text('Login'),
            ),
            ElevatedButton(
              onPressed: _register,
              child: Text('Register'),
            ),
          ],
        ),
      ),
    );
  }
}
```

### 7. Update Main File

Ensure your `main.dart` is set up to use the login screen:

```dart
import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';
import 'login_screen.dart';
import 'firebase_options.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(
    options: DefaultFirebaseOptions.currentPlatform,
  );
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Firebase Auth',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: LoginScreen(),
    );
  }
}
```

### 8. Run the App

Connect your device or start an emulator and run:

```bash
flutter run
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.



This README provides a detailed guide on setting up and running your Flutter project with Firebase authentication. You can modify it to fit your specific project needs and add any additional sections you find necessary.