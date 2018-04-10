
# Flutter snippets

## States

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