

## States

#### main
```dart
void main(){
  runApp(new MaterialApp(
    home: new MyPage()
  ));
}
```

#### Stateless Widget example
```dart

import 'package:flutter/material.dart';

class ScorePage extends StatelessWidget {
  final int score;
  final int totalQuestions;

  ScorePage(this.score, this.totalQuestions);

  @override
  Widget build(BuildContext context) {
    return new Material(
      color: Colors.blueAccent,
      child: new Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <Widget>[
          new Text("Your Score:", style: new TextStyle(color: Colors.white, fontWeight: FontWeight.bold, fontSize: 50.0)),
          new Text(score.toString() + "/" + totalQuestions.toString() , style: new TextStyle(color: Colors.white, fontWeight: FontWeight.bold, fontSize: 50.0)),
          new IconButton(
            icon: new Icon(Icons.arrow_right),
            color: Colors.white,
            iconSize: 50.0,
            onPressed: () => print('pressed'),
            )
        ],
      )
    ); 
  }
}
```

### StatefulWidget blank
```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());
 
class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Row & Column Example',
      home: new MyPage(),
    );
  }
}

class MyPage extends StatefulWidget {

  // connect the widget to the state
  @override
  State createState() => new MyPageState();
}
  
class MyPageState extends State<MyPage> {
  @override
  void initState() {
      super.initState(); 
      // your code follows
  }

  @override
  void dispose() {
    // your code precedes
    super.dispose();
  }

  @override
  void didUpdateWidget(MyPage oldWidget) {
    super.didUpdateWidget(oldWidget);
    // your code follows
    if(oldWidget._question != widget._question) {
      _fontSizeAnimationController.reset();
      _fontSizeAnimationController.forward();
    }
  }

  @override

  @override
  Widget build(BuildContext context) {

  }
}
```

#### StatefulWidget example
```dart
// a widget
class QuizPage extends StatefulWidget {

  // connect the widget to the state
  @override
  State createState() => new QuizPageState();
}

// a state
class QuizPageState extends State<QuizPage> {
  @override
  Widget build(BuildContext context) {
    return new Stack(
       children: <Widget>[
        new Column(// this is our main page
            children: <Widget>[
          new AnswerButton(true, () => print('you answered true')),
          new QuestionText("Pizza is nice", 1),
          new AnswerButton(false, () => print('you answered false')),
        ])
      ],
    );
  }
}
```