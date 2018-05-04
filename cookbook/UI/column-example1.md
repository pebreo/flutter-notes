

```dart
void main() {
  runApp(new MyApp());
}
 
class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Row & Column Example',
      theme: new ThemeData(
        primaryColor: const Color(0xFF43a047),
        accentColor: const Color(0xFFffcc00),
        primaryColorBrightness: Brightness.dark,
      ),
      home: new Example1Page(),
    );
  }
}

class Example1Page extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    List<Widget> menu = <Widget>[
      new IconButton(
        icon: new Icon(Icons.send),
        tooltip: 'To Example 2',
        onPressed: () => _toExample2(context),
      ),
      new IconButton(
        icon: new Icon(Icons.help),
        tooltip: 'To Example 3',
        onPressed: () => _toExample3(context),
      )
    ];
 
    return new Scaffold(
      appBar: new AppBar(
        title: new Text("Example 1 Page"),
        actions: menu,
      ),
      body: new Padding(
        padding: new EdgeInsets.symmetric(vertical: 0.0, horizontal: 0.0),
        child: new Text('Example Page 1 content'),
      ),
    );
  }
 
  void _toExample2(BuildContext context) {
    Navigator.of(context).push(new MaterialPageRoute<dynamic>(
      builder: (BuildContext context) {
        return new Example2Page();
      },
    ));
  }
 
  void _toExample3(BuildContext context) {
    Navigator.of(context).push(new MaterialPageRoute<dynamic>(
      builder: (BuildContext context) {
        return new Example3Page();
      },
    ));
  }
 
}

// Note: for simplicity, this is a stateless widget but, in a real app,
// a full screen is likely to be a stateful widget.
class Example2Page extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text("Example 2 Page"),
      ),
      body: new Padding(
        padding: new EdgeInsets.symmetric(vertical: 0.0, horizontal: 0.0),
        child: new Text('Example Page 2 content'),
      ),
    );
  }
 
}

class Example3Page extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text("Example 3 Page"),
      ),
      body: new Padding(
        padding: new EdgeInsets.symmetric(vertical: 0.0, horizontal: 0.0),
        child: new Text('Example Page 3 content'),
      ),
    );
  }
 
}
```