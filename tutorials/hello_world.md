
## Hello World Tutorial


### General approach

* Install Flutter SDK
* Install Android Studio
* Install VSC flutter add-ons
* Install Visual Studio Code (VSC)
* Start in `lib/main.dart`

### Instructions
* In VSC goto New Window -> Add Workspace Folder
* In VSC goto View -> Command Palette -> type: flutter -> New Project
* First we import the Material libraries. 
Material is the UI library which Google developed.
```dart
import 'package:flutter/material.dart';
```
Note that import statements can be both relative paths
or using the package syntax. The packages can be installed using
```dart
$ flutter packages get # gets packages defined in .package 
```

* Next we create a `main` function which is required on all Dart and Flutter
programs.
```dart
# syntax 1
void main() => runApp(new GettingStartedApp());
# or, syntax 2
void main() {
    runApp(new GettingStartedApp());
}
```

* Now we have to define `GettingStartedApp` class which was instantiated and 
passed into `runApp()`. The `GettingStartedApp` will be a subclass of `StatelessWidget`.
Pretty much all UI elements in our program will be widgets. The methods 
that we create and parameters we be what we use to handle user interaction.
So here's the class declaration by itself:
```dart
class GettingStartedApp extends StatelessWidget {
 // ...    
}
```
A stateless widget is a widget that doesn't change. For pratical purposes,
that means any instance variables will `final`.

* After declaring our custom widget, we will then override 
the `build()` method. The `build()` will return a `Widget`.
In our simple example, we return `MaterialApp` class which is a widget. 

```dart
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: "Getting STarted",
      home: new Text("Hello World"),
    );
```
In dartlang, named parameter value syntax looks like the above: with colon being
the equivalent of an equal sign. So, instead of `myfunc(title='mytitle', home=blah)`,
we use the colon syntax that you see above.

### Full example
```dart
import 'package:flutter/material.dart';

void main() => runApp(new GettingStartedApp());

class GettingStartedApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: "Getting STarted",
      home: new Text("Hello World"),
    );
    
  }
}
```