
```dart

import 'package:flutter/material.dart';

void main() {

  runApp(new MaterialApp(
    home: new Zone(),
  ));
}


class Page extends StatelessWidget {
  final String title;
  Page(this.title);
  @override
  Widget build(BuildContext context) {
    return new Container(
      child: new Center(
        child: new Text(title),
      ),
    );
  }
}

class Zone extends StatefulWidget {

  // connect the widget to the state
  @override
  ZoneState createState() => new ZoneState();
}

//state class of stateful class zone.
class ZoneState extends State<Zone> with SingleTickerProviderStateMixin {
  TabController tabController;
//here in the initstate we assign the tabcontroller and give it a length and vsyc for animation.
  @override
  void initState() {
    super.initState();
    tabController = new TabController(length: 3, vsync: this);
  }

//dispose method for good practice.
  @override
  void dispose() {
    super.dispose();
    tabController.dispose();
  }

//our build widget of state class.
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
        appBar: new AppBar(
          title: new Text('bottomNavigation'),
        ),
//here we define our TabBarView.
        body: new TabBarView(
          children: <Widget>[
            new Page("hey bottomNavigation"),
            new Page('the other one!'),
            new Page('headset is on?')
          ],
          controller: tabController,
        ),
//now we can just create a bottomnavigationBar under our scaffold
        bottomNavigationBar: new Material(
          color: Colors.orange,
          child: new TabBar(
            controller: tabController,
            tabs: <Widget>[
              new Tab(
                child: new Semantics(
                  label: 'ue',
                  child: new Icon(Icons.favorite),),
              ),
              new Tab(
                text: 'Random',
              ),
              new Tab(
                child: new Icon(Icons.headset),
              ),
            ],
          ),
        )); //scaffold
  }
}


```

other sources

https://www.youtube.com/watch?v=5_zQ6rjv00s