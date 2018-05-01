```dart
import 'package:flutter/material.dart';
import 'package:scoped_model/scoped_model.dart';
import 'package:lyric_maker/esl/models.dart';

class SubcategoryPage extends StatelessWidget {
  final String category;

  SubcategoryPage({this.category});

  @override
  Widget build(BuildContext context) {
   
    var buildTile = () => ScopedModelDescendant<WordModel>(
          builder: (context, child, model) {
            return const ListTile(title: const Text('Oee'));
          }
    ,);

     List<Widget> _buildList() {
    var x =  <Widget>[
          const ListTile(title: const Text('Toup')),
          new ExpansionTile(
             title: const Text('Sublist'),
             backgroundColor: Theme.of(context).accentColor.withOpacity(0.025),
             children:  <Widget>[
               buildTile(),
               const ListTile(title: const Text('Two')),
               const ListTile(title: const Text('Free')),
               const ListTile(title: const Text('Four'))
             ]
          ),
           const ListTile(title: const Text('Bottom'))
        ];
    return x;
  }
    return new Scaffold(
      appBar: new AppBar(title: new Text(category)),
      body: new ListView(
        children: _buildList(),
      )
    );
  }
}
```