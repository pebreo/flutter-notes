
```dart
import 'package:flutter/foundation.dart';
import 'package:flutter/material.dart';

void main() {
  runApp(new MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final appName = 'Custom Themes';

    return new MaterialApp(
      title: appName,
      theme: new ThemeData(
        brightness: Brightness.dark,
        primaryColor: Colors.lightBlue[800],
        accentColor: Colors.cyan[600],
      ),
      home: new MyHomePage(
        title: appName,
      ),
    );
  }
}

class MyHomePage extends StatelessWidget {
  final String title;

  MyHomePage({Key key, @required this.title}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text(title),
      ),
      body: new Center(
        child: new Container(
          color: Theme.of(context).accentColor,
          child: new Text(
            'Text with a background color',
            style: Theme.of(context).textTheme.title,
          ),
        ),
      ),
      floatingActionButton: new Theme(
        data: Theme.of(context).copyWith(accentColor: Colors.yellow),
        child: new FloatingActionButton(
          onPressed: null,
          child: new Icon(Icons.add),
        ),
      ),
    );
  }
}
```

# Example 2

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(new MyApp());
}

final ThemeData _themeData = new ThemeData(
  brightness: Brightness.dark,
  primarySwatch: Colors.orange,
  accentColor: Colors.brown,
);

/// Material App
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      theme: _themeData,
      title: 'Flutter Demo',
      home: new MyHomePage(title: 'Home Page'),
      routes: <String, WidgetBuilder>{
        AnotherPage.routeName: (BuildContext context) =>
        new AnotherPage(title: "Another Page"),
      },
    );
  }
}

/// place: "/"
class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);
  final String title;

  @override
  _MyHomePageState createState() => new _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text(widget.title),
      ),
      body: new Container(
        child: new Row(
          children: <Widget>[
            new RaisedButton(
              child: new Text("Home Button"),
              onPressed: _onPress,
            ),
          ],
        ),
      ),
      floatingActionButton: new FloatingActionButton(
        onPressed: _onPress,
        tooltip: 'Increment',
        child: new Icon(Icons.add),
      ),);
  }

  void _onPress() {
    Navigator.of(context).pushNamed(AnotherPage.routeName);
  }
}

/// place: "/AnotherPage"
class AnotherPage extends StatefulWidget {
  AnotherPage({Key key, this.title}) : super(key: key);
  static const String routeName = "/AnotherPage";
  final String title;

  @override
  _AnotherPageState createState() => new _AnotherPageState();
}

class _AnotherPageState extends State<AnotherPage> {
  @override
  Widget build(BuildContext context) {
    // First Group
    var firstGroupOfWidgets = new Container(
      decoration: new BoxDecoration(
        border: new Border.all(color: Colors.white, width: 2.0),
      ),
      child: new Padding(
        padding: new EdgeInsets.all(20.0),
        child: new Column(
          children: <Widget>[
            new Text("First Group..."),
            new RaisedButton(
                child: new Text("First Button"),
                onPressed: _onPress
            ),
          ],
        ),
      ),
    );

    // Second Group
    var secondGroupOfWidgets = new Container(
      decoration: new BoxDecoration(
        border: new Border.all(color: Colors.white, width: 2.0),
      ),
      child: new Padding(
        padding: new EdgeInsets.all(20.0),
        child: new Column(
          children: <Widget>[
            new Text("Second Group..."),
            new RaisedButton(
                child: new Text("Second Button"),
                onPressed: _onPress
            ),
          ],
        ),
      ),
    );

    var themeOfSecondGroup = new Theme(
      child: secondGroupOfWidgets,
      data: _themeData.copyWith(
        buttonColor: Colors.red,
      ),
    );

    // Page
    return new Theme(
      data: _themeData.copyWith(
        primaryColor: Colors.teal,
        buttonColor: Colors.purple,
      ),
      child: new Scaffold(
        appBar: new AppBar(
          title: new Text(widget.title),
        ),
        body: new Container(
          child: new Column(
            children: <Widget>[
              firstGroupOfWidgets,
              themeOfSecondGroup,
            ],
          ),
        ),
        floatingActionButton: new FloatingActionButton(
          onPressed: _onPress,
          tooltip: 'Add',
          child: new Icon(Icons.add),
        ),
      ),
    );
  }

  void _onPress() {
    Navigator.of(context).pop();
  }
}
```

source

https://flutter.io/cookbook/design/themes/

https://gist.github.com/branflake2267/c5303a7946c82cb6163c197a1c72ef55