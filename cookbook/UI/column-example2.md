

```dart

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

class Example1Page extends StatelessWidget {
  
  @override
  Widget build(BuildContext context) {

    var buildList =  new ListView.builder(
          itemCount: 5,
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

    List<Widget> menu = <Widget>[
      new IconButton(
        icon: new Icon(Icons.send),
        tooltip: 'To Example 2',
        onPressed: () => _toExample2(context),
      ),
      new IconButton(
        icon: new Icon(Icons.help),
        tooltip: 'To Example 3',
        onPressed: () => _toExample3(context),
      )
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
  
    return new Scaffold(
      appBar: new AppBar(
        title: new Text("Example 1 Page"),
        actions: menu,
      ),
      body: new Padding(
        padding: new EdgeInsets.symmetric(vertical: 0.0, horizontal: 0.0),
        child: body,
      ),
    );
  }
  
    void _toExample2(BuildContext context) {
      Navigator.of(context).push(new MaterialPageRoute<dynamic>(
        builder: (BuildContext context) {
          return new Example2Page();
        },
      ));
    }
  
    void _toExample3(BuildContext context) {
      Navigator.of(context).push(new MaterialPageRoute<dynamic>(
        builder: (BuildContext context) {
          return new Example3Page();
        },
      ));
    }
 
}

// Note: for simplicity, this is a stateless widget but, in a real app,
// a full screen is likely to be a stateful widget.
class Example2Page extends StatelessWidget {
  
  @override
  Widget build(BuildContext context) {


    List<Widget> menu = <Widget>[
        new IconButton(
          icon: new Icon(Icons.send),
          tooltip: 'To Example 2',
          onPressed: () => _toExample2(context),
        ),
        new IconButton(
          icon: new Icon(Icons.help),
          tooltip: 'To Example 3',
          onPressed: () => _toExample3(context),
        )
      ];

    Widget subtitle = new Container (
      padding: new EdgeInsets.all(8.0),
      color: new Color(0X33000000),
      child: new Text('Subtitle'),
    );
  
    Widget listSection = new Expanded(
      flex: 2,
      child: new ListView(
        scrollDirection: Axis.vertical,
        shrinkWrap: true,
        children: _generateListItems().map((String value) {
          return _displayListItem(value);
        }).toList()),
      );
  
    Widget gridSection = new Expanded(
      flex: 1,
      child: new GridView.count(
        crossAxisCount: 4,
        childAspectRatio: 1.0,
        mainAxisSpacing: 4.0,
        crossAxisSpacing: 4.0,
        children: _generateGridItems().map((String value) {
          return _displayGridItem(value);
        }).toList()),
    );
  
    Widget body = new Column(
      // This makes each child fill the full width of the screen
      crossAxisAlignment: CrossAxisAlignment.stretch,
      mainAxisSize: MainAxisSize.min,
      children: <Widget>[
        subtitle,
        listSection,
        gridSection,
      ],
    );
  
    return new Scaffold(
      appBar: new AppBar(
        title: new Text("Example 2 Page"),
        actions: menu,
      ),
      body: new Padding(
        padding: new EdgeInsets.symmetric(vertical: 0.0, horizontal: 0.0),
        child: body,
      ),
    );
  }
  
  Widget _displayListItem(String value) {
    return new Container (
      padding: new EdgeInsets.all(8.0),
      color: new Color(0X9900CCCC),
      child: new Text(value),
    );
  }
  
  Widget _displayGridItem(String value) {
    return new Container (
      padding: new EdgeInsets.all(8.0),
      color: new Color(0X99CCCC00),
      child: new Text(value),
    );
  }
  
  // Note: Placeholder method to generate list data.
  List<String> _generateListItems() {
    List<String> listItems = new List<String>();
    for (int i = 0; i < 20; i++) {
      listItems.add('List Item ' + i.toString() + ' title and description');
    }
    return listItems;
  }
  
  // Note: Placeholder method to generate grid data
  List<String> _generateGridItems() {
    List<String> gridItems = new List<String>();
    for (int i = 0; i < 24; i++) {
      gridItems.add('GI ' + i.toString());
    }
    return gridItems;
  }
    void _toExample2(BuildContext context) {
      Navigator.of(context).push(new MaterialPageRoute<dynamic>(
        builder: (BuildContext context) {
          return new Example2Page();
        },
      ));
    }
  
    void _toExample3(BuildContext context) {
      Navigator.of(context).push(new MaterialPageRoute<dynamic>(
        builder: (BuildContext context) {
          return new Example3Page();
        },
      ));
    }
 
}

class Example3Page extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    Widget titleRow = new Row(
      children: <Widget>[
        new Icon(Icons.people),
        new Expanded(
          child: new Container(
            padding: new EdgeInsets.symmetric(horizontal: 4.0),
            child: new Text('This is quite a long name that will be cut off',
              overflow: TextOverflow.ellipsis,
              maxLines: 1,
            ),
          ),
        ),
        new Text('0111 222 333'),
      ],
    );

    Widget textSection = new Container(
      color: new Color(0X3300CC00),
      child: new Column(
        crossAxisAlignment: CrossAxisAlignment.stretch,
        mainAxisSize: MainAxisSize.min,
        children: <Widget>[
          titleRow,
          new Text('We have a description here. It may fit on 2 lines, '
              'or it may fit on 1 line. Or will require more lines than 2, but'
              ' we only show 2 lines maximum f f f f f f f f f f f f f f f .',
            overflow: TextOverflow.ellipsis,
            maxLines: 2,)
        ],
      ),
    );

    Widget body = new Container(
      color: new Color(0X33000000),
      child: new Row(
        children: <Widget>[
          new IconButton(
            onPressed: null, // Not implemented in this code tutorial
            icon: new Icon(Icons.send),
          ),
          new Expanded(
              child: textSection),
          new IconButton(
            onPressed: null, // Not implemented in this code tutorial
            icon: new Icon(Icons.edit),
          ),
        ],
      ),
    );

    return new Scaffold(
      appBar: new AppBar(
        title: new Text("Example 3 Page"),
      ),
      body: new Padding(
        padding: new EdgeInsets.symmetric(vertical: 0.0, horizontal: 0.0),
        child: body,
      ),
    );
  }
  
}

```