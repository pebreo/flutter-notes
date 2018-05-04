
```dart

import 'package:flutter/material.dart';
import 'dart:async';


void main() {
  runApp(new MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Stack Box Decoration Example',
      theme: new ThemeData(
        primaryColor: const Color(0xFF43a047),
        accentColor: const Color(0xFFffcc00),
        primaryColorBrightness: Brightness.dark,
      ),
      home: new HomePage(),
    );
  }
}

 
class HomePage extends StatefulWidget {
  HomePage({Key key}) : super(key: key);
 
  @override
  _HomePageState createState() => new _HomePageState();
 
}
 
class _HomePageState extends State<HomePage> {
 
  @override
  Widget build(BuildContext context) {
    List<Widget> menu = <Widget>[new IconButton(
      icon: new Icon(Icons.image),
      tooltip: 'Second screen',
      onPressed: _toSecondPage,
    ),
    ];
 
    return new Scaffold(
      appBar: new AppBar(
        title: new Text("Box Decoration example"),
        actions: menu,
      ),
      body: _buildBody(),
    );
  }
 
 Widget _buildBody() {
    return new Container(
      constraints: new BoxConstraints.expand(
        height: 200.0,
      ),
      alignment: Alignment.bottomLeft,
      padding: new EdgeInsets.only(left: 16.0, bottom: 8.0),
      decoration: new BoxDecoration(
        image: new DecorationImage(
          image: Image.network(
                'http://lorempixel.com/output/abstract-q-c-1920-1080-8.jpg',
                fit: BoxFit.cover,
              ).image,
          fit: BoxFit.cover,
        ),
      ),
      child: new Text('Title',
        style: new TextStyle(
          fontWeight: FontWeight.bold,
          fontSize: 20.0,
          color: Colors.white,
        )
      ),
    );
  }
 
  Future _toSecondPage() async {
    Navigator.of(context).push(new MaterialPageRoute<dynamic>(
      builder: (BuildContext context) {
        return new SecondPage();
      },
    ));
  }
 
}



class SecondPage extends StatefulWidget {
  SecondPage({Key key}) : super(key: key);

  @override
  _SecondPageState createState() => new _SecondPageState();

}

class _SecondPageState extends State<SecondPage> {

  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text("Box Decoration and Stack example"),
      ),
      body: _buildBody(),
    );
  }

  Widget _buildBody() {
    return new Container(
        constraints: new BoxConstraints.expand(
          height: 200.0,
        ),
        padding: new EdgeInsets.only(left: 16.0, bottom: 8.0, right: 16.0),
        decoration: new BoxDecoration(
          image: new DecorationImage(
            image: Image.network(
                'http://lorempixel.com/output/abstract-q-c-1920-1080-8.jpg',
                fit: BoxFit.cover,
              ).image,
            fit: BoxFit.cover,
          ),
        ),
        child: new Stack(
          children: <Widget>[
            new Positioned(
              left: 0.0,
              bottom: 0.0,
              child: new Text('Title',
                  style: new TextStyle(
                    fontWeight: FontWeight.bold,
                    fontSize: 20.0,
                    color: Colors.white,
                  )
              ),
            ),
            new Positioned(
              right: 0.0,
              bottom: 0.0,
              child: new Icon(Icons.star, color: Colors.white,),
            ),
          ],
        )
    );
  }
}
```