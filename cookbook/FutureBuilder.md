
```dart
class Foo extends StatelessWidget {
  final String word;
  final Timer timer = new Timer(new Duration(seconds: 1), () {
    debugPrint("Print after 5 seconds");
});
  Foo({this.word});


  @override
  Widget build(BuildContext context) {
    var futureBuilder = new FutureBuilder(
      future: _getData(),
      builder: (BuildContext context, AsyncSnapshot snapshot) {
        switch (snapshot.connectionState) {
          case ConnectionState.none:
          case ConnectionState.waiting:
            return new Text('loading...');
          default:
            if (snapshot.hasError)
              return new Text('Error: ${snapshot.error}');
            else
              return Text('data: ${snapshot.data}');
        }
      },
    );
    
    return new Scaffold(
      appBar: new AppBar(
        title: new Text("Home Page"),
      ),
      body: futureBuilder,
    );
  }

    Future<String> _getData() async {
      await new Future.delayed(new Duration(seconds: 5));
      return 'foo';
  }
}

void main(){
  runApp(new MaterialApp(
    home: new Foo()
  ));
}

```
