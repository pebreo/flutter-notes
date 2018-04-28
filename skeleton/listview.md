
The `mypage.dart` file
```dart
import 'package:flutter/material.dart';


class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Flutter Demo',
      theme: new ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: new MyPage(),
    );
  }
}

class MyPage extends StatefulWidget {
  @override
  _MyPageState createState() => new _MyPageState();
}

class _MyPageState extends State<MyPage> {
  
  int _total = 3;

  @override
  Widget build(BuildContext context) {
    
    var listView = new ListView.builder(
      itemCount: _total,
      itemBuilder: (BuildContext context, int index) {
          return new ListTile(
            title: new Text('heuleo'),
          );
      },
    );

    return new Scaffold(
      appBar: new AppBar(
        title: new Text('App Biaur Title')
      ), 
      body: listView,
    );
  }

}
```

And the `main.dart` file should contain:
```dart
import 'package:flutter/material.dart';
import 'package:lyric_maker/esl/mypage.dart';

void main() => runApp(new MyApp()); 
```