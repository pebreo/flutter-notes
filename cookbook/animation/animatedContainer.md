
```dart
import 'package:flutter/material.dart';

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
      home: new AnimateContentExample(),
    );
  }
}
class AnimateContentExample extends StatefulWidget {
  @override
  _AnimateContentExampleState createState() => new _AnimateContentExampleState();
}

class _AnimateContentExampleState extends State<AnimateContentExample> {
  double _animatedHeight = 100.0;
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(title: new Text("Animate Content"),),
      body: new Column(
        children: <Widget>[
          new Card(
            child: new Column(
              mainAxisAlignment: MainAxisAlignment.center,
              crossAxisAlignment: CrossAxisAlignment.center,
              children: <Widget>[
                new GestureDetector(
                  onTap: ()=>setState((){
                    _animatedHeight!=0.0?_animatedHeight=0.0:_animatedHeight=100.0;}),
                  child:  new Container(
                  child: new Text("CLICK ME"),
                  color: Colors.blueAccent,
                  height: 25.0,
                    width: 100.0,
                ),),
                new AnimatedContainer(duration: const Duration(milliseconds: 120),
                  child: new Text("Toggle Me"),
                  height: _animatedHeight,
                  color: Colors.tealAccent,
                  width: 100.0,
                )
              ],
            ) ,
          )
        ],
      ),
    );
  }
}
```

source

https://stackoverflow.com/questions/49029841/how-to-animate-collapse-elements-in-flutter/49034627#49034627
