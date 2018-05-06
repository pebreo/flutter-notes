

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
      home: new TestSignInView(),
    );
  }
}

class TestSignInView extends StatefulWidget {
  @override
  _TestSignInViewState createState() => new _TestSignInViewState();
}


class _TestSignInViewState extends State<TestSignInView> {
  bool _load = false;
  final GlobalKey<ScaffoldState> _scaffoldKey = new GlobalKey<ScaffoldState>();

  @override
  Widget build(BuildContext context) {

    return new Scaffold(
      key: _scaffoldKey,
      backgroundColor: Colors.white,
      body: new Padding(
        padding: const EdgeInsets.symmetric(vertical: 50.0, horizontal: 20.0),
        child: new ListView(
          children: <Widget>[
            new Column(
              mainAxisAlignment: MainAxisAlignment.center,
              crossAxisAlignment: CrossAxisAlignment.center,
              children: <Widget>[
                    new TextField(),
                    new TextField(),
                    new FlatButton(color:Colors.blue, child: new Text('Sign In'),
                      onPressed: (){
                        _scaffoldKey.currentState.showSnackBar(
                          new SnackBar(duration: new Duration(seconds: 4),
                          content: new Row(
                                children: <Widget>[
                                    new CircularProgressIndicator(),
                                    new Text("  Signing-In...")
                                    ],
                                ),
                          )
                        );
                      },
                    )
              ],
            )
          ],
        ),  
      )
    );
  }

}


class NextPage extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return new Material(
      color: Colors.blueAccent,
      child: new Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <Widget>[
          new Text("Next Page", style: new TextStyle(color: Colors.white, fontWeight: FontWeight.bold, fontSize: 50.0)),
        ],
      )
    ); 
  }
}
```

source

https://stackoverflow.com/questions/47065098/how-work-with-progress-indicator-in-flutter