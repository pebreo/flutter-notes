### Example 1
```dart
import 'dart:async';

main() {
    int count = 0;
  Future.doWhile((){
    return new Future.delayed(new Duration(milliseconds:500), (){
      count++;
      if(count<=3) {
        print(count);
        return true;
      }
      return false;
    });
  });
}
```

### Example 2
```dart
import 'dart:async';

int count = 0;

bool doCount() {
    count++;
    if(count<=3) {
      print(count);
      return true;
    }
    return false;
}

main() {
  Future.doWhile((){
    return new Future.delayed(new Duration(milliseconds:500), doCount);
  });
}

```

### Example 3
```dart
import 'dart:async';

int count = 0;

Future<String> s;

Future<String> expensiveA() async {
  await new Future.delayed(new Duration(milliseconds: 1000));
  return 'delayed string';
}

Future<bool> doCount() async {
    count++;
    if(count<=3) {
      String s = await expensiveA();
      print(count);
      print(s);
      return true;
    }
    return false;
}

main() {
  Future.doWhile((){
    return new Future.delayed(new Duration(milliseconds:100), doCount);
  });
}

/// https://docs.flutter.io/flutter/widgets/State/setState.html
```

### Example 4
```dart
import 'dart:async';

List<String> mynames = ['john','paul'];

Future<bool> doCount() async {
    
    if(mynames.isNotEmpty) {
      String s = mynames.last;
      mynames.removeLast();
      print(s);
      return true;
    }
    return false;
}

main() {
  Future.doWhile((){
    return new Future.delayed(new Duration(milliseconds:1000), doCount);
  });
}
```


### Example 5
In this example, we simulate a service that is called every 2 seconds.
We limit the number of times it is called to only 3 times.
```dart
import 'dart:async';

List heroes;
int count = 0;

// simulate expensive service
Future<List> myService() async {
  await new Future.delayed(new Duration(milliseconds: 500));
  List heroes = ['batman', 'superman'];
  return heroes;
}

// fetch data from service and assign to global variable
Future<Null> runService() async {
  heroes = await myService();
}


main() async {
  Future.doWhile(() async {
    await new Future.delayed(new Duration(milliseconds:2000));
    count++;
    // limit number of calls
    if(count<=3) {
      await runService();
      print('done waiting');
      print(heroes);
      return true;
    } else {
      return false;
    }
  });
}
```