
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
onTap: () => Navigator.of(context).push(new MaterialPageRoute(builder: (BuildContext context) => new AskRoomPage())),

//or

Navigator.of(context).push(new MaterialPageRoute(builder: (BuildContext context) => new QuizPage()))
```

### Navigato to another state using `var route` and passing params to the other widget
```
var route = new MaterialPageRoute(
  builder: (BuildContext context) =>
      new RoomPage(user:person, channel: chan)
);

Navigator.of(context).push(route);
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


#### Navigate and pass params to another state
```dart

class FirstPageState extends State<FirstPage> {

  // defined in some button
  onPressed: () {
      var route = new MaterialPageRoute(
          builder: (BuildContext context) => 
              new NextPage(value: _textController.text),
      );
      Navigator.of(context).push(route);

  }
  
}

//located in the next state
class NextPage extends StatefulWidget {
    final String value;

    // key is mandatory but 'value' is optional
    NextPage({Key key, this.value}) : super(key: key);

 // .. 
}

class NextPageState extends State<NextPage> {
    // now you can use widget.value
}

Source:

https://www.youtube.com/watch?v=MsycCv5r2Wo
```


### Navigate using url
```dart
main() {
  var model = new ChatModel();
  Widget app = new ScopedModel<ChatModel>(
    model: model,
    child: new MaterialApp(
      home: LandingPage(),
      theme: ThemeData(
        canvasColor: Colors.blueGrey,
        iconTheme: IconThemeData(
          color: Colors.white,
        ),
        accentColor: Colors.pinkAccent,
        brightness: Brightness.dark,
      ),
      routes: <String, WidgetBuilder>
      {
        "/RoomPage": (BuildContext context) => new RoomPage(),
        "/LoginPage": (BuildContext context) => new LoginPage(),
      },
    ),
  );
  runApp(app);
} 

// Usage using pushNamed
onPressed: () {
  Navigator.of(context).pushNamed("/RoomPage");
},

// Usage using popAndPushNamed
void _clickItem() {
  Navigator.popAndPushNamed(context, "/RoomPage");    
}
```


#### Add navigation to ListTile
```
_pushMember(Member member) {
  Navigator.of(context).push(
    new MaterialPageRoute(
      builder: (context) => new MemberWidget(member)
    )
  );
}

Widget _buildRow(int i) {
  return new Padding(
    padding: const EdgeInsets.all(16.0),
    child: new ListTile(
      title: new Text("${_members[i].login}", style: _biggerFont),
      leading: new CircleAvatar(
          backgroundColor: Colors.green,
          backgroundImage: new NetworkImage(_members[i].avatarUrl)
      ),
      // Add onTap here:
      onTap: () { _pushMember(_members[i]); },
    )
  );
}
```


### Pushing InkWell, Card, InkResponse
You have to wrap the above in `GestureDetector` in order to handle respons 
```dart
new GestureDetector(
  onTap: () { print('tapped!') },
  child: new Card(...),
);
```

### JSON and Websockets
##### `pubspec.yaml`
```yaml
name: ws_demo
description: A new Flutter project.

dependencies:
  web_socket_channel:

```
You should then run `pub get`

##### `foo.yaml`
```dart
import 'package:web_socket_channel/io.dart';
import 'dart:convert';

class Message {
  final String type;
  final String message;

  Message(this.type, this.message);

  Message.fromJson(Map<String, dynamic> json)
      : type = json['type'],
        message = json['message'];

  Map<String, dynamic> toJson() =>
    {
      'type': type,
      'message': message,
    };
}

main() {
    var ws = new IOWebSocketChannel.connect('ws://localhost:8000/ws/chat/lobby/');
    var msg = new Message('chat_message','herro');
    print(JSON.encode(msg));
    ws.sink.add(JSON.encode(msg));    
}
```
http://cogitas.net/parse-json-dart-flutter/

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

### Fonts
```dart
// pubspec.yml
flutter:
  uses-material-design: true
  assets:
    - lib/gallery/example_code.dart
    - packages/flutter_gallery_assets/videos/butterfly.mp4
  fonts:
    - family: Raleway
      fonts:
        - asset: packages/flutter_gallery_assets/pesto/fonts/Raleway-Regular.ttf
        - asset: packages/flutter_gallery_assets/pesto/fonts/Raleway-Medium.ttf
          weight: 500
        - asset: packages/flutter_gallery_assets/pesto/fonts/Raleway-SemiBold.ttf
          weight: 600
    - family: AbrilFatface
      fonts:
        - asset: packages/flutter_gallery_assets/shrine/fonts/abrilfatface/AbrilFatface-Regular.ttf
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








