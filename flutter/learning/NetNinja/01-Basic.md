# Basic App

## Example 1

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(
    MaterialApp(
      home: HomePage(),
    ),
  );
}

class HomePage extends StatelessWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('My App!'),
        centerTitle: true,
        backgroundColor: Colors.red[200],
      ),
      body: Center(
        child: Text(
          'Hello Jagriti!',
          style: TextStyle(
            fontSize: 30,
            fontWeight: FontWeight.w900,
            letterSpacing: 3.0,
            color: Colors.grey[800],
            fontFamily: 'Lemon',
          ),
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () => "",
        backgroundColor: Colors.red[200],
        child: Text('Click'),
      ),
    );
  }
}

```

## Insert Network Images

```dart
Center(
    child: Image.network(
        'https://i.pinimg.com/564x/4f/30/5d/4f305dc5d3f1bbb336d35a71f1b953a2.jpg',
    ),
),
```

## Insert Local Images

- Download the images
- Paste them in assets/images/ directory
- Update the `yaml` file

```yaml
flutter:
  assets:
    - assets/images/

  fonts:
    - family: Lemon
      fonts:
        - asset: assets/fonts/Lemon-Regular.ttf
  uses-material-design: true
```

- In code

```dart
Center(
    child: Image(
        image: AssetImage('assets/images/love.avif'),
    ),
),
```

- Alternate Method

```dart
Center(
    child: Image.asset('assets/images/taj_mahal.jpeg'),
),
```

## Icons

```dart
Center(
    child: Icon(
        Icons.business_center,
        color: Colors.blue[400],
        size: 76.0,
    ),
)
```

## Elevated Button

```dart
Center(
    child: ElevatedButton(
        onPressed: () {},
        style: ElevatedButton.styleFrom(
        backgroundColor: Colors.amber[400],
        ),
        child: Text('Click Me'),
    ),
)
```
