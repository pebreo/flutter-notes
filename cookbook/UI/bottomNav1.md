

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
      title: 'Row & Column Example',
      theme: new ThemeData(
        primaryColor: const Color(0xFF43a047),
        accentColor: const Color(0xFFffcc00),
        primaryColorBrightness: Brightness.dark,
      ),
      home: new Example1Page(),
    );
  }
}

class Example1Page extends StatefulWidget {

  // connect the widget to the state
  @override
  State createState() => new Example1PageState();
}

class Example1PageState extends State<Example1Page> {
  bool showBotNavbar = false;

  @override
  Widget build(BuildContext context) {

  void _showBottomNavbar() {
      print('edit');
      setState((){
          showBotNavbar==true ? showBotNavbar=false : showBotNavbar=true;
      });
    }

    var buildList =  new ListView.builder(
          itemCount: 5,
          itemBuilder: (context, rowNumber) {
          return new Container(
                padding: new EdgeInsets.all(16.0),
                child: new Column(
                  children: <Widget>[
                    new Text('hello',)
                  ],
                ));
          });

    List<Widget> menu = <Widget>[
      new IconButton(
        icon: new Icon(Icons.edit),
        tooltip: 'Show botnav',
        onPressed: _showBottomNavbar,
      ),
    ];
  
    Widget subtitle = new Container (
      padding: new EdgeInsets.all(8.0),
      color: new Color(0X33000000),
      child: new Text('Subtitle'),
    );
  
    Widget middleSection = new Expanded(
      child: new Container (
        padding: new EdgeInsets.all(8.0),
        color: new Color(0X9900CC00),
        child: buildList,
      ),
    );
  
    Widget bottomBanner = new Container (
      padding: new EdgeInsets.all(8.0),
      color: new Color(0X99CC0000),
      height: 48.0,
      child: new Center(
        child: new Text('Bottom Banner'),
      ),
    );
  
    Widget body = new Column(
      // This makes each child fill the full width of the screen
      crossAxisAlignment: CrossAxisAlignment.stretch,
      mainAxisSize: MainAxisSize.min,
      children: <Widget>[
        subtitle,
        middleSection,
        bottomBanner,
      ],
    );

    var buildBotNavbar = new BottomNavigationBar(items:
        <BottomNavigationBarItem>[
          new BottomNavigationBarItem(
            icon: const Icon(Icons.ac_unit),
            title: new Text('foo'),
            
          ),
                new BottomNavigationBarItem(
            icon: const Icon(Icons.access_alarms),
            title: new Text('bar'),
            
          ),
        ],

    );

    return new Scaffold(
      appBar: new AppBar(
        title: new Text("Example 4 Page"),
        actions: menu,
      ),
      body: new Padding(
        padding: new EdgeInsets.symmetric(vertical: 0.0, horizontal: 0.0),
        child: body,
      ),
      bottomNavigationBar: showBotNavbar ? buildBotNavbar : null,
    );
  }
  


}


```