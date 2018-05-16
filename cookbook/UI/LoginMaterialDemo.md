

```dart
import 'package:flutter/material.dart';

void main() => runApp(new ShrineApp());

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: const Text('SHRINE'),
      ),
      body: const Center(
        child: const Text('You did it!'),
      ),
    );
  }
}

class LoginPage extends StatefulWidget {
  @override
  _LoginPageState createState() => new _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
  final _usernameController = TextEditingController();
  final _passwordController = TextEditingController();
  
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      body: new SafeArea(
        child: new ListView(
          padding: const EdgeInsets.symmetric(horizontal: 24.0),
          children: <Widget>[
            const SizedBox(height: 80.0),
            new Column(
              children: <Widget>[
                new Image.asset('assets/diamond.png'),
                const SizedBox(height: 16.0),
                const Text('SHRINE'),
              ],
            ),
            const SizedBox(height: 120.0),
            TextField(
              controller: _usernameController,
              decoration: InputDecoration(filled: true, labelText:' Username'),
            ),
            const SizedBox(height: 12.0),
            TextField(
              controller: _passwordController,
              decoration: InputDecoration(filled: true, labelText:' Password'),
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

class ShrineApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Shrine',
      home: new HomePage(),
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
      builder: (BuildContext context) => new LoginPage(),
      fullscreenDialog: true,
    );
  }
}
```

sources


https://codelabs.developers.google.com/codelabs/mdc-101-flutter/#0