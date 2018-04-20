# The Scoped Model Technique

If you want to pass data among widgets, you can
use the Scoped Model library. The Scoped Model
library is similar to Redux approach in that 
you have some sort of "parent" model that the widgets
use as a central place to store data. Since
there is a common place for all widgets to store
that saves a lot of passing data around as
parameters to class declarations.

### Setup

To implement the scoped model appoarch you will need to 
include `scoped_model : 0.2.0` in your `pubspec.yaml`
file.

In your code, you will define a model like this
```dart
import 'package:scoped_model/scoped_model.dart';

class CounterModel extends Model {
    int _counter = 0;
    
    int get counter => _counter;

    void increment() {
        // ..
    }
}
```

### Usage

Note that `counter` is the getter for the private
variable `_counter`.

Now you hook up the model to your widgets by
making your `MaterialApp` the child of the `ScopedModel<T>`
class, where T is the model that you want that child to 
be able to share among each other.
```dart
ScopedModel<CounterModel>(
      model: new CounterModel(),
      child: new MaterialApp(
        title: 'Flutter Demo',
        theme: new ThemeData(
          primarySwatch: Colors.green,
        ),
        home: new CounterHome('Scoped Model Demo'),
      ),
    );
```
So all the children of `MaterialApp` will be able to 
access the model. Remember that `MaterialApp` is a
widget, and all it's children are widgets.

Any widget that wants to access variables
and methods from `CounterModel` will need to use
`ScopedModelDescendant`. Specifically, that
widget will need to be created in the `builder` property
of `ScopedModelDescendant`. So something like this:

```dart
new ScopedModelDescendant<CounterModel>(
    builder: (context, child, model) => new Text(
        model.counter.toString(),
        style: Theme.of(context).textTheme.display1),
    ),
```
Note that `model` is the instance of our `CounterModel`.

#### Propagating changes

To propagate changes to all your widgets you'll
need to run `notifyListeners()` in your `increment()`
method like this:

```dart
void increment() {
    // First, increment the counter
    _counter++;

    // Then notify all the listeners.
    notifyListeners();
}
```


#### Multiple models
It seems that working with a simple data model is pretty
straightforward. But what about if you have more than 
one model that you want your widgets to have access to.
For this, we can just use the keywords `abstract`, `extends`
and `with`. 

For example, let's say I wanted to add a `DecrementModel`
class with decrement behavior. I would write it like this:

```dart
abstract class DecrementModel extends CounterModel {
    void decrement() {
        _counter--;

        // Notify all widgets listeners
        notifyListeners();
    }

}
```
You then hook up `CounterModel` and `Decrement` models
to a `MainModel` like this:

```dart
class MainModel extends Model with CounterModel, DecrementModel {}
```
Note the empting `{}` at the end of the `MainModel` declaration.

Now that we have the `MainModel` we then use
that as the parameter for our generic class/variable.

```dart
ScopedModel<MainModel>(
      model: new CounterModel(),
      child: new MaterialApp(
        //...
      ),
    );
```

#### Conclusion
As we have seen, implementing the Scoped Model approach
is not that difficult. When you start writing 
larger apps with more and more widgets that require
communicating with eachother, it will become
painfully obvious that passing parameters between
widgets get cumbersome. In your next project, give Scoped
Models a try.

The example code in this tutorial was taking from 
this code written by Brian Egan who is also the
author of the `scoped_model` Flutter library. Here
is the full example below. You can also find the repo
[here](https://github.com/brianegan/scoped_model/blob/master/example/lib/main.dart).

### Complete example code
```dart
import 'package:flutter/material.dart';
import 'package:scoped_model/scoped_model.dart';

void main() {
  runApp(new MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // At the top level of our app, we'll, create a ScopedModel Widget. This
    // will provide the CounterModel to all children in the app that request it
    // using a ScopedModelDescendant.
    return new ScopedModel<CounterModel>(
      model: new CounterModel(),
      child: new MaterialApp(
        title: 'Flutter Demo',
        theme: new ThemeData(
          primarySwatch: Colors.green,
        ),
        home: new CounterHome('Scoped Model Demo'),
      ),
    );
  }
}

// Start by creating a class that has a counter and a method to increment it.
//
// Note: It must extend from Model.
class CounterModel extends Model {
  int _counter = 0;

  int get counter => _counter;

  void increment() {
    // First, increment the counter
    _counter++;

    // Then notify all the listeners.
    notifyListeners();
  }
}

class CounterHome extends StatelessWidget {
  final String title;

  CounterHome(this.title);

  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text(title),
      ),
      body: new Center(
        child: new Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            new Text(
              'You have pushed the button this many times:',
            ),
            // Create a ScopedModelDescendant. This widget will get the
            // CounterModel from the nearest parent ScopedModel<CounterModel>.
            // It will hand that CounterModel to our builder method, and
            // rebuild any time the CounterModel changes (i.e. after we
            // `notifyListeners` in the Model).
            new ScopedModelDescendant<CounterModel>(
              builder: (context, child, model) => new Text(
                  model.counter.toString(),
                  style: Theme.of(context).textTheme.display1),
            ),
          ],
        ),
      ),
      // Use the ScopedModelDescendant again in order to use the increment
      // method from the CounterModel
      floatingActionButton: new ScopedModelDescendant<CounterModel>(
        builder: (context, child, model) => new FloatingActionButton(
              onPressed: model.increment,
              tooltip: 'Increment',
              child: new Icon(Icons.add),
            ),
      ),
    );
  }
}
```


### Resources

https://github.com/brianegan/scoped_model/blob/master/example/lib/main.dart