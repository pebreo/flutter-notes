
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
Navigator.of(context).push(new MaterialPageRoute(builder: (BuildContext context) => new QuizPage()))
```

#### Navigate to another state and remove previous state
```dart
// prevents navigating backwards
 Navigator.of(context).pushAndRemoveUntil(new MaterialPageRoute(builder: (BuildContext context) => new ScorePage(quiz.score, quiz.length)), (Route route) => route == null)
```

#### Navigate to another state
```dart
void _pushSaved() {
    Navigator.of(context).push(
      new MaterialPageRoute(
        builder: (context) {
          final tiles = _saved.map(
            (pair) {
              return new ListTile(
                title: new Text(pair.asPascalCase, style: _biggerFont)
              );  
            }
          );
          final divided = ListTile.divideTiles(
            context: context,
            tiles: tiles,
          ).toList();
          return new Scaffold(
            appBar: new AppBar(
              title: new Text('Saved Suggestions.'),
            ),
            body: new ListView(children: divided),
          );
        }
      )
    );
  }

/// usage
 new IconButton(
      icon: new Icon(Icons.list), 
      onPressed: _pushSaved
),
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

#### IconButton
```dart
new IconButton(
            icon: new Icon(Icons.arrow_right),
            color: Colors.white,
            iconSize: 50.0,
            onPressed: () => Navigator.of(context).pushAndRemoveUntil(new MaterialPageRoute(builder: (BuildContext context) => new LandingPage()), (Route route) => route == null),
)
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


## Views


#### ListView

```dart
class HomeWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new ListView.builder(
        itemCount: 20,
        itemBuilder: (context, rowNumber) {
        return new Container(
              padding: new EdgeInsets.all(16.0),
              child: new Column(
                children: <Widget>[
                  new Image.network("https://goo.gl/vFdXGc"),
                  new Container(height: 8.0,),
                  new Text("Instagram firebas course: check it out using the dsecription link below",
                      style: new TextStyle(
                          fontWeight: FontWeight.bold, fontSize: 18.0)),
                  new Divider(color: Colors.green),
                ],
              ));
        });
  }
}
```

## Glossary

#### tools
Android Studio
Atom
IntelliJ
Sublime
VCS

#### Flutter
State
StreamBuilder

Store
StoreConnector
StoreProvider

setState
stream
widget

#### Design patterns / libraries
MVP
react
redux


#### Libraries
react
redux
flutter_redux

