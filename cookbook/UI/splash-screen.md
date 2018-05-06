
```dart

import 'dart:async';
import 'package:flutter/material.dart';

class Flutkart {
  static const String name = "Flutkart";
  static const String store = "Online Store\n For Everyone";
  static const String wt1 = "WELCOME";
  static const String wc1 =
      "Flutkart is Premium Online Shopping\n Platform for Everyone";
  static const String wt2 = "DISCOVER PRODUCT";
  static const String wc2 =
      "Search Latest and Featured Product\n With Best Price";
  static const String wt3 = "ADD TO CART";
  static const String wc3 =
      "Add to Cart All Product You need\n And Checkout the Order";
  static const String wt4 = "VERIFY AND RECEIVE";
  static const String wc4 =
      "We Will Verify Your Order\n Pay the bill and Receive the Product";
  static const String skip = "SKIP";
  static const String next = "NEXT";
  static const String gotIt = "GOT IT";
}

class MyNavigator {
  static void goToHome(BuildContext context) {
    Navigator.pushNamed(context, "/home");
  }

  static void goToIntro(BuildContext context) {
    Navigator.pushReplacementNamed(context, "/intro");
  }
}

var routes = <String, WidgetBuilder>{
"/home": (BuildContext context) => HomePage(),
"/intro": (BuildContext context) => IntroPage(),
};


void main() => runApp(new MaterialApp(
    theme:
        ThemeData(primaryColor: Colors.red, accentColor: Colors.yellowAccent),
    debugShowCheckedModeBanner: false,
    home: SplashScreen(),
    routes: routes));


class SplashScreen extends StatefulWidget {
  @override
  _SplashScreenState createState() => _SplashScreenState();
}

class _SplashScreenState extends State<SplashScreen> {
  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    Timer(Duration(seconds: 3), () => MyNavigator.goToIntro(context));
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Stack(
        fit: StackFit.expand,
        children: <Widget>[
          Container(
            decoration: BoxDecoration(color: Colors.redAccent),
          ),
          Column(
            mainAxisAlignment: MainAxisAlignment.start,
            children: <Widget>[
              Expanded(
                flex: 2,
                child: Container(
                  child: Column(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: <Widget>[
                      CircleAvatar(
                        backgroundColor: Colors.white,
                        radius: 50.0,
                        child: Icon(
                          Icons.shopping_cart,
                          color: Colors.greenAccent,
                          size: 50.0,
                        ),
                      ),
                      Padding(
                        padding: EdgeInsets.only(top: 10.0),
                      ),
                      Text(
                        Flutkart.name,
                        style: TextStyle(
                            color: Colors.white,
                            fontWeight: FontWeight.bold,
                            fontSize: 24.0),
                      )
                    ],
                  ),
                ),
              ),
              Expanded(
                flex: 1,
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: <Widget>[
                    CircularProgressIndicator(),
                    Padding(
                      padding: EdgeInsets.only(top: 20.0),
                    ),
                    Text(
                      Flutkart.store,
                      softWrap: true,
                      textAlign: TextAlign.center,
                      style: TextStyle(
                          fontWeight: FontWeight.bold,
                          fontSize: 18.0,
                          color: Colors.white),
                    )
                  ],
                ),
              )
            ],
          )
        ],
      ),
    );
  }
}



class IntroPage extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return new Material(
      color: Colors.blueAccent,
      child: new Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <Widget>[
          new Text("Intro Page", style: new TextStyle(color: Colors.white, fontWeight: FontWeight.bold, fontSize: 50.0)),
        ],
      )
    ); 
  }
}

class HomePage extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return new Material(
      color: Colors.blueAccent,
      child: new Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <Widget>[
          new Text("Home Page", style: new TextStyle(color: Colors.white, fontWeight: FontWeight.bold, fontSize: 50.0)),
        ],
      )
    ); 
  }
}
```


sources

https://www.youtube.com/watch?v=FNBuo-7zg2Q

https://github.com/iampawan/FlutKart