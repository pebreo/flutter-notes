

import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';
void main() => runApp(new MyApp());
 
class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Row & Column Example',
      home: ScorePage(3,3),
    );
  }
}

class ScorePage extends StatelessWidget {
  final int score;
  final int totalQuestions;

  ScorePage(this.score, this.totalQuestions);


  @override
  Widget build(BuildContext context) {
    return CupertinoPicker(
            itemExtent: 10.0,
          onSelectedItemChanged: (int foo) {print(foo);},
          children: <Widget>[
            Text('foo'),
            Text('bar'),
            Text('bra'),
          ],
        );
      
  }



  // @override
  // Widget build(BuildContext context) {
  //   return new Material(
  //     color: Colors.blueAccent,
  //     child: ListWheelScrollView(
  //             perspective: 0.005,
  //             diameterRatio: 2.0,
  //             itemExtent: 20.0,
  //             children: <Widget>[
  //                 Text('hello'),
  //                 Text('world'),
  //                 Text('hello'),
  //                 Text('world')
  //           ],)
        
    
  //   ); 
  // }
}

// https://github.com/tanjunze/Flutter-Example/blob/bc5b387f1302e2618423d89861b04dc8f21de8b3/flutter_compt/lib/assembly/wheel_picker.dart