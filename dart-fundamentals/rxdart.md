
### Requirements
##### pubspec.yaml
```yaml
name: ws_demo
description: A Dart project.

dependencies:
  web_socket_channel:
  rxdart:

dev_dependencies:
  #flutter_test:
  #  sdk: flutter
```
Usage: `pub install`


### Simple Observable example
```dart

import 'package:rxdart/rxdart.dart';
import 'dart:async';

void main() {
    var obs = new Observable(new Stream.fromIterable([1]))
      .interval(new Duration(seconds: 3))
      .flatMap((i) => new Observable.just(i))
      .take(1);
    obs.listen(print);
}
```