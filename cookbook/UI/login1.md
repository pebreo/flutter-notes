

```dart
import 'package:flutter/material.dart';
import 'package:meta/meta.dart';
import 'dart:async';

@immutable
class MyUser {
  final String name;

  MyUser(this.name);
}

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Flutter Demo',
      home: new MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);

  final String title;

  @override
  _MyHomePageState createState() => new _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  Future<MyUser> user;

  void _logIn() {
    setState(() {
      user = new Future.delayed(const Duration(seconds: 3), () {
        return new MyUser("Toto");
      });
    });
  }

  Widget _buildForm(AsyncSnapshot<MyUser> snapshot) {
    var floatBtn = new RaisedButton(
      onPressed:
          snapshot.connectionState == ConnectionState.none ? _logIn : null,
      child: new Icon(Icons.save),
    );
    var action =
        snapshot.connectionState != ConnectionState.none && !snapshot.hasData
            ? new Stack(
                alignment: FractionalOffset.center,
                children: <Widget>[
                  floatBtn,
                  new CircularProgressIndicator(
                    backgroundColor: Colors.red,
                  ),
                ],
              )
            : floatBtn;

    return new ListView(
      padding: const EdgeInsets.all(15.0),
        children: <Widget>[
          new ListTile(
            title: new TextField(),
          ),
          new ListTile(
            title: new TextField(obscureText: true),
          ),
          new Center(child: action)
        ],
    );
  }

  @override
  Widget build(BuildContext context) {
    return new FutureBuilder(
      future: user,
      builder: (context, AsyncSnapshot<MyUser> snapshot) {
        if (snapshot.hasData) {
          return new Scaffold(
            appBar: new AppBar(
              title: new Text("Hello ${snapshot.data.name}"),
            ),
          );
        } else {
          return new Scaffold(
            appBar: new AppBar(
              title: new Text("Connection"),
            ),
            body: _buildForm(snapshot),
          );
        }
      },
    );
  }
}
```

source

https://stackoverflow.com/questions/47065098/how-work-with-progress-indicator-in-flutter