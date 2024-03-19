# Basic uses of Asset Images and Network Images

## For asset images update the `pubspec.yaml` file as follows

```yml
flutter:
  # The following line ensures that the Material Icons font is
  # included with your application, so that you can use the icons in
  # the material Icons class.
  uses-material-design: true

  # To add assets to your application, add an assets section, like this:
  assets:
    - assets/
```

- Create a directory called `assets` inside the root directory
- Paste the images inside the `assets` directory. Thats it.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(
    const MaterialApp(home: Home()),
  );
}

class Home extends StatelessWidget {
  const Home({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text(
          "Learning Flutter",
          style: TextStyle(color: Colors.white),
        ),
        centerTitle: true,
        backgroundColor: Colors.red[600],
      ),
      // body: Image.asset(
      //   "assets/fireworks-1.jpg",
      // ),
      body: Image.network(
          "https://cdn.pixabay.com/photo/2024/02/21/15/28/dahlia-8587940_1280.jpg"),
      backgroundColor: Colors.blue[300],
      bottomNavigationBar: BottomAppBar(
        shape: const CircularNotchedRectangle(),
        child: Container(
          height: 30.0,
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () => {},
        backgroundColor: Colors.red[600],
        child: const Text(
          "Click",
          style: TextStyle(color: Colors.white),
        ),
      ),
      floatingActionButtonLocation: FloatingActionButtonLocation.centerDocked,
    );
  }
}

```
