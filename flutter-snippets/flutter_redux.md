## flutter_redux explanation


The following code demonstrates how to use `flutter_redux` library to
increment a number when a button is pressed.

In redux you need the following:
* You need a store - the store will contain your state which can be a class or simple type
* You need actions - we define actions that will be run on our data/state
* And you need a reducer - the reducer is a function that will handle actions on a store

The setup requires that we enumerate actions. In the example below, there is only one action
called `Increment`. In the `counterReducer` we define how to handle that action
and how to handle the `state`. The state can be a complex object or a simple type which,
in this case, is simply an integer called `state`. Later the state will be transformed and we
will call it `count` as it becomes the parameter to a builder method.

We put all our data into the store which contains a state. 
In order to access, the `store`, we will need to wrap our widgets with the outer widget `StoreProvider`.

### Abridged code
##### Setting up the action, counter, and store
```dart
// One simple action: Increment
enum Actions { Increment }

// The reducer, which takes the previous count and increments it in response
// to an Increment action.
int counterReducer(int state, dynamic action) {
  if (action == Actions.Increment) {
    return state + 1;
  }

  return state;
}

void main() {
  // Create your store as a final variable in a base Widget
  final store = new Store<int>(counterReducer, initialState: 0);

  runApp(new FlutterReduxApp(
    title: 'Flutter Redux Demo',
    store: store,
  ));
}
```

##### use the `StoreProvider` and `StoreConnector` in our widgets
```dart
@override
Widget build(BuildContext context) {
    // The StoreProvider should wrap your MaterialApp or WidgetsApp. This will
    // ensure all routes have access to the store.
    return new StoreProvider<int>(
        home: new Scaffold(
            body: new Center(
                child: new Column(
                    children: [
                        new StoreConnector<int, String>(
                            converter: (store) => store.state.toString(),
                            // pass the string to builder function
                            builder: (context, count) {
                                count, // the state was passed as count
                                style: Theme.of(..)
                            };
                        ),
                    ]
                ),
            ),
        )
    );
}
```

### complete
```dart
```


### Resources

https://pub.dartlang.org/packages/flutter_redux