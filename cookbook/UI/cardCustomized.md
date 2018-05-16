
```dart
import 'package:flutter/material.dart';

void main() => runApp(new ShrineApp());

class ShrineApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Shrine',
      home: HomePage(),
      initialRoute: '/login',
      onGenerateRoute: _getRoute,
    );
  }

  Route<dynamic> _getRoute(RouteSettings settings) {
    if (settings.name != '/login') {
      return null;
    }

    return MaterialPageRoute<void>(
      settings: settings,
      builder: (BuildContext context) => LoginPage(),
      fullscreenDialog: true,
    );
  }
}

class LoginPage extends StatefulWidget {
  @override
  _LoginPageState createState() => _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
  final _usernameController = TextEditingController();
  final _passwordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SafeArea(
        child: ListView(
          padding: EdgeInsets.symmetric(horizontal: 24.0),
          children: <Widget>[
            SizedBox(height: 80.0),
            Column(
              children: <Widget>[
                Image.asset('assets/diamond.png'),
                SizedBox(height: 16.0),
                Text('SHRINE'),
              ],
            ),
            SizedBox(height: 120.0),
            TextField(
              controller: _usernameController,
              decoration: InputDecoration(
                filled: true,
                labelText: 'Username',
              ),
            ),
            SizedBox(height: 12.0),
            TextField(
              controller: _passwordController,
              decoration: InputDecoration(
                filled: true,
                labelText: 'Password',
              ),
              obscureText: true,
            ),
            ButtonBar(
              children: <Widget>[
                FlatButton(
                  child: Text('CANCEL'),
                  onPressed: () {
                    _usernameController.clear();
                    _passwordController.clear();
                  },
                ),
                RaisedButton(
                  child: Text('NEXT'),
                  onPressed: () {
                    Navigator.pop(context);
                  },
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }
}

class HomePage extends StatelessWidget {

  var _buildCol = new Column(
    crossAxisAlignment: CrossAxisAlignment.start,
    children: <Widget>[
      AspectRatio(aspectRatio: 18.0/11.0,
        child: Container(color: Colors.blueAccent, child:Image.asset('assets/diamond.png'),)
        
      ),
      Padding(
        padding: new EdgeInsets.fromLTRB(5.0 ,25.0, 12.0, 8.0),
        child: Container(color: Colors.black26, 
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: <Widget>[
                Text('Title'),
                SizedBox(height: 8.0),
                Text("Secondary text")
            ],
          ),
        )
        
         
      ),
    ],
  );
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title:Text('SHRINE'),
        // hamburger icon
        leading:IconButton(
          icon: Icon(Icons.menu),
          onPressed:(){ print('menu pressed!');},
        ),
        // right-side icon menus
        actions: <Widget>[
            IconButton(
              icon: Icon(Icons.search),
              onPressed: (){
                print("pressed search");
              },
            ),
            IconButton(
              icon: Icon(Icons.tune),
              onPressed: (){
                print("pressed tune");
              },
            ),
        ],
      ),
    
      body: GridView.count(
          crossAxisCount: 2,
          padding: EdgeInsets.all(16.0),
          childAspectRatio: 8.0/9.0,
          children: <Widget>[Card(child:_buildCol)],
      ),
    );
  }
}

```