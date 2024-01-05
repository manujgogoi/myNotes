# Introduction to Flutter’s UI

Reference from [GeeksForGeeks](https://www.geeksforgeeks.org/what-is-widgets-in-flutter/)

## Widgets

- Widgets are the building block of flutter applications. Widgets describe what their view should look like given their current configuration and state. It includes a text widget, row widget, column widget, container widget, and many more.

- Each element on a screen of the Flutter app is a widget. The view of the screen completely depends upon the choice and sequence of the widgets used to build the apps. And the structure of the code of an apps is a tree of widgets.

### Category of Widgets

There are mainly 14 categories in which the flutter widgets are divided. They are mainly segregated on the basis of the functionality they provide in a flutter application.

- **Accessibility**: These are the set of widgets that make a flutter app more easily accessible.
- **Animation and Motion**: These widgets add animation to other widgets.
- **Assets**, **Images**, and **Icons**: These widgets take charge of assets such as display images and show icons.
- **Async**: These provide async functionality in the flutter application.
- **Basics**: These are the bundle of widgets that are absolutely necessary for the development of any flutter application.
- **Cupertino**: These are the iOS designed widgets.
- **Input**: This set of widgets provides input functionality in a flutter application.
- **Interaction Models**: These widgets are here to manage touch events and route users to different views in the application.
- **Layout**: This bundle of widgets helps in placing the other widgets on the screen as needed.
- **Material Components**: This is a set of widgets that mainly follow material design by Google.
- **Painting and effects**: This is the set of widgets that apply visual changes to their child widgets without changing their layout or shape.
- **Scrolling**: This provides scrollability of to a set of other widgets that are not scrollable by default.
- **Styling**: This deals with the theme, responsiveness, and sizing of the app.
- **Text**: This displays text.

## HelloWorld

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Text(
        "Hello World",
        textDirection: TextDirection.ltr,
      ),
    );
  }
}
```

### AppBar example

```dart
import 'package:flutter/material.dart';

class MyAppBar extends StatelessWidget {
  const MyAppBar({required this.title, super.key});

  final Widget title;

  @override
  Widget build(BuildContext context) {
    return Container(
      height: 55,
      padding: EdgeInsets.symmetric(horizontal: 8),
      decoration: BoxDecoration(
        color: Colors.blue[500],
      ),
      child: Row(
        children: [
          const IconButton(
            onPressed: null,
            icon: Icon(Icons.menu),
            tooltip: 'Navigation Menu',
          ),
          Expanded(
            child: title,
          ),
          const IconButton(
            icon: Icon(Icons.search),
            tooltip: 'Search',
            onPressed: null,
          ),
        ],
      ),
    );
  }
}

class MyScaffold extends StatelessWidget {
  const MyScaffold({super.key});

  @override
  Widget build(BuildContext context) {
    return Material(
      child: Column(
        children: [
          MyAppBar(
            title: Text(
              'Example Text',
              style: Theme.of(context).primaryTextTheme.titleLarge,
            ),
          ),
          Text('World...'),
        ],
      ),
    );
  }
}

void main() {
  runApp(
    const MaterialApp(
      title: 'Hello World',
      home: SafeArea(child: MyScaffold()),
    ),
  );
}

```

## Types of Widgets

There are broadly two types of widgets in the flutter:

1. Stateless Widget
2. Stateful Widget

Examples:

1. Stateless Widget
