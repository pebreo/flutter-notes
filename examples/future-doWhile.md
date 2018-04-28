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