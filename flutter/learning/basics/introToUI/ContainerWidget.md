# Container Widget

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyContainerApp());
}

class MyContainerApp extends StatelessWidget {
  const MyContainerApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          leading: Icon(Icons.menu),
          title: Text('Welcome'),
        ),
        body: const MyContainer(),
      ),
    );
  }
}

class MyContainer extends StatelessWidget {
  const MyContainer({super.key});

  @override
  Widget build(BuildContext context) {
    return Container(
      height: 200,
      width: double.infinity,
      margin: EdgeInsets.all(20),
      padding: EdgeInsets.all(30),
      alignment: Alignment.bottomCenter,
      decoration: BoxDecoration(
        color: Colors.amber,
        border: Border.all(
            width: 5.0, style: BorderStyle.solid, color: Colors.tealAccent),
      ),
      transform: Matrix4.rotationZ(.3),
      child: Text('Hello Container'),
    );
  }
}


```
