

###Requirement
You must put this in your `pubspec.yaml` file:
```
shared_preferences: "^0.4.1"
```


### Code
```dart

import 'dart:async';
import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';

void main() => runApp(new MyApp());


Future<bool> saveNamePreference(String name) async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  return prefs.setString("name",name);
}

Future<String> getNamePreference() async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  String name = prefs.getString("name");
  return name;
}
 
class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: new MyHomePage(),
      routes: <String, WidgetBuilder>{
        NextPage.routeName: (context) => new NextPage(),
      }
    );
  }
}

class MyHomePage extends StatefulWidget {

  // connect the widget to the state
  @override
  State createState() => new MyHomePageState();
}
  
class MyHomePageState extends State<MyHomePage> {
  var _controller = new TextEditingController();
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: AppBar(title: Text("Home Page")) ,
      body: new ListView(
        children: <Widget>[
          ListTile(
            title: TextField(controller: _controller,)
          ),
          ListTile(
            title: RaisedButton(
              child: Text("Next Page"),
              onPressed: () {
                saveName();
              },
            ),
          ),
        ],
      ) 
    );
  }
  void saveName() {
    String name = _controller.text;
    saveNamePreference(name).then((bool commited){
      Navigator.of(context).pushNamed(NextPage.routeName);
    });
  }

}

class NextPage extends StatefulWidget {
  static String routeName = "/nextPage";
  // connect the widget to the state
  @override
  State createState() => new NextPageState();
}
  
class NextPageState extends State<NextPage> {
  String _name = "";

  @override
  void initState(){
    getNamePreference().then((name){
      _name = name;
    });
    super.initState();
  }
  
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: AppBar(title: Text("Next Page")) ,
      body: ListTile(title: Text(_name))
      
    );
  }
}
```


### Code version 2
```dart

import 'dart:async';
import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';

void main() => runApp(new MyApp());


Future<bool> saveNamePreference(String name) async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  return prefs.setString("name",name);
}

Future<String> getNamePreference() async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  String name = prefs.getString("name");
  return name;
}
 
class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: new MyHomePage(),
      routes: <String, WidgetBuilder>{
        NextPage.routeName: (context) => new NextPage(),
      }
    );
  }
}

class MyHomePage extends StatefulWidget {

  // connect the widget to the state
  @override
  State createState() => new MyHomePageState();
}
  
class MyHomePageState extends State<MyHomePage> {
  var _controller = new TextEditingController();
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: AppBar(title: Text("Home Page")) ,
      body: new ListView(
        children: <Widget>[
          ListTile(
            title: TextField(controller: _controller,)
          ),
          ListTile(
            title: RaisedButton(
              child: Text("Next Page"),
              onPressed: () {
                saveName();
              },
            ),
          ),
        ],
      ) 
    );
  }
  void saveName() {
    String name = _controller.text;
    saveNamePreference(name).then((bool commited){
      Navigator.of(context).pushNamed(NextPage.routeName);
    });
  }

}

class NextPage extends StatefulWidget {
  static String routeName = "/nextPage";
  // connect the widget to the state
  @override
  State createState() => new NextPageState();
}
  
class NextPageState extends State<NextPage> {
  String _name = "";

  @override
  void initState(){
    getNamePreference().then(updateName);
    super.initState();
  }
  
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: AppBar(title: Text("Next Page")) ,
      body: ListTile(title: Text(_name))
      
    );
  }
  void updateName(String value) {
    _name = value;
  }
}
```