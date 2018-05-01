
## Callling a future in a class constructor

Let's say you needed to initialize data for your class
but you need to call an "expensive" function, that is,
it might be delayed. 

In Dart, you can approach it two ways:

* Have the user explicitly calls the async method
* Automatically run the async method


### User starts future initialization
```dart
class MyComponent{
  MyComponent();

  Future init() async {
    print("init");
  }
}

Future<Null> main() async {
  var c = new MyComponent();
  await c.init();
  print("done");
}
```

### Start initializiation in constructor
Allow the program to run and wait 
```dart
import 'dart:async';

class MyComponent{
  Future _doneFuture;

  MyComponent() {
    _doneFuture = _init();
  }

  Future<String> _init() async {
    return new Future.delayed(new Duration(milliseconds:10000), (){
      print('done delay');
      return 'hello';
    });
  }

  Future get initializationDone => _doneFuture;
}

 main() async {
  var c = new MyComponent();
  var msg = await c.initializationDone;
  print(msg);
  print("done");
}
```

#### Source

https://stackoverflow.com/questions/38933801/calling-an-async-method-from-component-constructor-in-dart