# Switching between states


### User input

iconButton
```
new IconButton(
            icon: new Icon(Icons.arrow_right),
            color: Colors.white,
            iconSize: 50.0,
            onPressed: () =>   Navigator.of(context).pushAndRemoveUntil(new MaterialPageRoute(builder: (BuildContext context) => new LandingPage()), (Route route) => route == null),
            )
```


### Navigator

```dart
 Navigator.of(context).pushAndRemoveUntil(new MaterialPageRoute(builder: (BuildContext context) => new ScorePage(quiz.score, quiz.length)), (Route route) => route == null);
```


Most of the time you will use 
```dart
class CorrectWrongOverlay extends StatefulWidget {
  // declare anonymous function
  final VoidCallback _onTap;
}
//
child: new InkWell(
    onTap: () => widget._onTap()
    // ...
)
```
And it will be use in tk like this:
```dart
new CorrectWrongOverlay(true, 
     // pass anynomous function
    () {
         Navigator.of(context).pushAndRemoveUntil(new MaterialPageRoute(builder: (BuildContext context) => new ScorePage(quiz.score, quiz.length)), (Route route) => route == null);
    }
)
```

If you don't want the user to be able to move back a state you would use
```dart
Navigator.of(context).pushAndRemoveUntil(new MaterialPageRoute(builder: (BuildContext context) => new ScorePage(quiz.score, quiz.length)), (Route route) => route == null)
```



TODO

VoidCallback _onTap;

onPressed

Navigator.to


new InkWell(
          onTap: () => widget._onTap(),