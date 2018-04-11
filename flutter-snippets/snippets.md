
# Flutter snippets

## States

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

#### Navigate to another state
```dart
Navigator.of(context).push(new MaterialPageRoute(builder: (BuildContext context) => new QuizPage())),
```


## Containers


#### Stack
```dart
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
```

#### Expanded
```dart
new Expanded(
  child: new Material(
     
      color: Colors.greenAccent,
      child: new InkWell(
          onTap: () => _onTap(), // enable anonymous function as a parameter
          child: new Center(
            child: new Container(
              decoration: new BoxDecoration(
                border: new Border.all(color: Colors.white, width: 4.0)
              ),
              padding: new EdgeInsets.all(15.0),
              child: new Text("True": "False", 
                 style: new TextStyle(color: Colors.white, fontSize: 40.0, fontWeight: FontWeight.bold, fontStyle: FontStyle.italic)),
            ),
          ))));
  }
```


## User input


#### inkWell
```dart
child: new InkWell(
                      onTap: () => _onTap(), // enable anonymous function as a parameter
                      child: new Center(
                        child: new Container(
                          decoration: new BoxDecoration(
                            border: new Border.all(color: Colors.white, width: 4.0)
                          ),
                          padding: new EdgeInsets.all(15.0),
                          child: new Text(this._answer == true ? "True": "False", 
                          style: new TextStyle(color: Colors.white, fontSize: 40.0, fontWeight: FontWeight.bold, fontStyle: FontStyle.italic)),
                        ),
                      ))
```

#### floating action button
```dart
void _incrementCounter() {
    setState(() {

      _counter++;
    });
}


new FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: new Icon(Icons.add),
      ), // This trailing comma makes auto-formatting nicer for build methods.
```