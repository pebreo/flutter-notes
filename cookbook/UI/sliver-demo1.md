

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Sliver Demo',
      theme: ThemeData(
        primarySwatch: Colors.red,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Sliver Example'),
      ),
      body: CustomScrollView(
        slivers: <Widget>[
          SliverAppBar(
            title: Text(
              'Sliver App Bar',
            ),
            floating: true,
            pinned: true,
            snap: true,
            // centerTitle: true,
            // elevation: 10.0,
            expandedHeight: 250.0,
            flexibleSpace: FlexibleSpaceBar(
              background: Image.network(
                'http://lorempixel.com/output/abstract-q-c-1920-1080-8.jpg',
                fit: BoxFit.cover,
              ),
              title: Text('Spacebar Title'),
            ),
          ),

          SliverFixedExtentList(
            itemExtent: 50.0,
            delegate:
                SliverChildBuilderDelegate((BuildContext context, int index) {
              return Container(
                alignment: Alignment.center,
                color: Colors.indigo[100 * (index % 9)],
                child: Text('List Item: $index'),
              );
            }),
          )
        ],
      ),
    );
  }
}
```


source

https://github.com/tensor-programming/Flutter_Sliver_Tutorial/blob/master/lib/main.dart