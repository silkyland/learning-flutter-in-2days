**Understanding Widgets in Flutter**

In Flutter, everything is a widget². Widgets are the building blocks of a Flutter app, and understanding them is the key to creating dynamic and interactive user interfaces². They can be categorized into two main types: StatelessWidgets and StatefulWidgets². StatelessWidgets are immutable and don't change once created, while StatefulWidgets can change over time².

**Basic Widgets: AppBar, Button, Text, Container, Row, Column**

- **AppBar**: This widget displays content and actions at the top of a screen⁵. It commonly displays branding information such as logos and titles and often contains buttons or other points of user interaction⁹.
- **Button**: Flutter provides several types of buttons, like `ElevatedButton`, `FlatButton`, `IconButton`, etc⁵.
- **Text**: This widget is used to display a run of styled text⁵.
- **Container**: A convenience widget that combines common painting, positioning, and sizing widgets⁵.
- **Row and Column**: These widgets allow for horizontal and vertical arrangements of other widgets, respectively¹¹.

**Building a Simple App Using These Widgets**

Here's a simple example of a Flutter app using these basic widgets:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('My First Flutter App'),
        ),
        body: Column(
          children: <Widget>[
            Text('Hello, Flutter!'),
            ElevatedButton(
              onPressed: () {},
              child: Text('Press me'),
            ),
            Container(
              margin: EdgeInsets.all(10.0),
              child: Text('This is a container'),
            ),
            Row(
              children: <Widget>[
                Text('Row Item 1'),
                Text('Row Item 2'),
              ],
            ),
          ],
        ),
      ),
    );
  }
}
```

This code creates a simple Flutter app with an AppBar, a Column containing a Text widget, an ElevatedButton, a Container, and a Row with two Text widgets. The `ElevatedButton` doesn't perform any action when pressed as the `onPressed` function is empty⁸.

### References

1. Understanding the Flutter Widget Tree: A Comprehensive Overview. https://medium.com/@fredricknsiah/understanding-the-flutter-widget-tree-a-comprehensive-overview-e716fadc26e8.
2. Basics | Flutter. https://docs.flutter.dev/ui/widgets/basics.
3. Customizing the AppBar in Flutter: An overview with examples. https://blog.logrocket.com/flutter-appbar-tutorial/.
4. Widgets | Flutter University. https://flutteruniversity.gitbook.io/docs/learn-flutter/basics/widgets.
5. Building Your First Flutter App: A Step-by-Step Guide. https://etwinworkshop.medium.com/building-your-first-flutter-app-a-step-by-step-guide-d7c81ddb6434.
6. Widgets | Flutter. https://docs.flutter.dev/ui/widgets.
7. Widget class - widgets library - Dart API - Flutter. https://api.flutter.dev/flutter/widgets/Widget-class.html.
8. Understanding Flutter Widgets: A Beginner’s Guide to ... - Medium. https://medium.com/@kavyamistry0612/understanding-flutter-widgets-a-beginners-guide-to-building-user-interfaces-eed1acf17070.
9. Step-by-Step Guide to Coding Your First Flutter App: Widgets ... - Medium. https://medium.com/@sahaj.blup/step-by-step-guide-to-coding-your-first-flutter-app-widgets-structure-and-build-method-6319920b92ec.
10. Designing App UI with Flutter Widgets: A Comprehensive Guide. https://flutterone.com/designing-app-ui-with-flutter-widgets-a-comprehensive-guide/.
11. Layout | Flutter. https://docs.flutter.dev/ui/widgets/layout.
12. github.com. https://github.com/kustavo/guia-rapido/tree/8e6453cfeb1d18c65b7f590888949814ab5c48df/docs%2Fflutter%2Fintroducao.md.
