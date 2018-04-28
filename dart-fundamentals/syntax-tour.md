
### `this`
Just like Javascript, the `this` property refers to the instance
```dart
class Person {
  var name;
  Person(this.name);
 
  sayName() {
    print(this.name);
  }
}

main() {
  var p = new Person('john');
  p.sayName();
}
```


### common expressions
```dart
(myValue == true) ? "true" : "false"

myobject?.data ?? ""
```

### arrow functions 
```dart
foo(3);
foo(var x) => x+1;
```

### Map literals
```dart
main() {
    var x = {'b': 99};
    var foo = {
      "bar": x,
      "baz": 5,
    };
  print(foo["bar"]);
}
```

### Map 
```dart
var x = new Map();
x['e'] = 1;
x.putIfAbsent('e',() => 3);
x.putIfAbsent('f',() => 1);
x.putIfAbsent('f',() => 5);
print(x);
```

### Maps - looping
Using foreach
```dart
Map<String, int> example = { 'A': 1, 'B': 2, 'C': 3 };
example.forEach((key,value) {
  print(key);
  print(value);
})
```
Using for-loop
```dart
Map<String, int> example = { 'A': 1, 'B': 2, 'C': 3 };

for (String key in example.keys) {
  if (example[key] == 2 && key == 'B') {
    break;
  }
}
```



### Named parameters
```dart
main() {
    foo(x: true); // named parameter
    baz(false);  // unnamed param
    bar(on: false, up: false, open: false);
}

foo({bool x}) {
    print(x);
}

baz(bool y) {
  print(y);
}

bar({on = true, up = true, open=false}) {
  print('ah');
}
```
### Parametered types (Generics)



#### Lists initialization
`List foo` is the same as `List<dynamic> foo`.
```dart
var mylist = List<String>();
var mylist = <List>[]
```
Here are three different ways to initialize lists
```dart
// List demo
main() {
  foo();
  bar();
  baz();
}

// Dynamic declaration
foo() {
  var names = new List();
  names.addAll(['Seth', 'Kathy', 'Lars']);
  names.add(42); 
}

// Dynamic declaration
bar() {
  var names = new List<dynamic>();
  names.addAll(['Seth', 'Kathy', 'Lars']);
  names.add(42); 
}

// Static declaration
baz() {
  var names = new List<String>();
  names.addAll(['Seth', 'Kathy', 'Lars']);
  names.add(42); // Error
}
```


### Constructors
```dart
class Person {
    String name;

    Person(this.name);
}

var p = Person('john')
```

### Constructors (custom)
```dart
class ChatModel {
  
  ChatModel(this.y) {
    this.set();
  }
  void set() {
    this.x = 9;
  }
  var x;
  var y;

}

main() {
  var c = new ChatModel(5);
  print(c.x);

  
}
```

### Constructors (initializer list)
```dart
class RoomPage {
  final x;
  final y;
  final String user;
  final String channel;
  

  const RoomPage({String key, this.user, this.channel}) : 
    x = 3, // initializer list
    y = 5; // second part of initializer list

}

main() {
  var a = new RoomPage(user: 'ou');
  print(a.x);
  print(a.y);
}

```

### Constructors (Flutter)
```dart
class RoomPage extends StatefulWidget {
  final x;
  final PersonData user;
  final WebSocketChannel channel;
  
  const RoomPage({Key key, this.user, this.channel}) : super(key: key);
  // or
  const RoomPage({Key key, this.user, this.channel}) : 
    x = 3;
    super(key: key),
  @override
  State createState() => new RoomPageState();
}

// instantiation
var foo = new RoomPage(user: myuser, channel: mychannel)

```

### Constructors (Flutter)
```dart
class RoomPage extends StatefulWidget {
  final var key
  final PersonData user;
  final WebSocketChannel channel;
  
  const RoomPage({key, user, channel}) {
    key = key;
    user = user;
    channel = channel;
    super(key: key);
  } 

    @override
  State createState() => new RoomPageState();
}
// instantiation:

var foo = new RoomPage(user: myuser, channel: mychannel)

```

### Getters
```dart
class Quiz {
  // private because of underscore
  List<Question> _questions;
  int _currentQuestionIndex = -1;
  int _score = 0;

  
  Quiz(this._questions) {
    _questions.shuffle();
  }

  // getters - using anynomous functions
  List<Question> get questions => _questions;
  int get length => _questions.length;
  int get questionNumber => _currentQuestionIndex+1;
  int get score => _score;

  // getter using a function
  Question get nextQuestion {
    _currentQuestionIndex++;
    if(_currentQuestionIndex >= this.length) return null;
    return _questions[_currentQuestionIndex];
  }
  void answer(bool isCorrect) {
    if(isCorrect) _score++;
  }
}
```

### Static methods
Static methods are methods available only
to the class. For example
```dart
class Foo {
  static void hello() {
    print('hello');
  }
}

main() {
  Foo.hello();
}
```

### async
There are a couple of ways to write code that executes asynchronously.

##### codes executes out-of-order
The first is using the familiar `then()` syntax. When you use this
syntax your code will not necessarily run in order. You can 
only use the then when a `Future` object is return like in
the `longWait` function below which returns a `Future<bool>`.

```dart
import 'dart:async';

Future<bool> longWait(foo) async {
  var x = [1,2,3];
  x.forEach((item) => print(item));
  return true;
}


// Using then() syntax
myAsync() {
  longWait('myparam').then((bool value) {
    print('done waiting');  
  });
  print('done');
}

// chaining then() syntax
myAsync() {
  longWait('myparam').then((bool value) {
    print('done waiting');  
  }).then((bool value) {
    print('done waiting');  
  }).then((bool value) {
    print('done waiting');  
  });
  print('done');
}

main() {
  myAsync();
}
```
##### codes executes in order
The other async syntax is to use `await` in your function.
Using `await`, code will run in order if you use `await` on any function
call that returns a `Future` object.

```dart
import 'dart:async';

// Futures in order
Future myAsync() async {
    print('start');
    bool ret = await longWait('async');
    print(ret);
    print('done');
}

// Futures in order
myAsync() async {
  print('start');
  Future f1 = longWait('one');
  Future f2 = longWait('two');
  Future f3 = longWait('three');

  await Future.wait([f1, f2, f3]);
  print('done');
}

main() {
  myAsync();
}
```
##### using `async` with `await`
Note that whenever, you have an `await` in your function, you
must annotate that function with an `async`.

```dart
import 'dart:async';

Future<bool> longWait(foo) async {
  var x = [1,2,3];
  x.forEach((item) => print(item));
  return true;
}

// Futures in order
Future<dynamic> myAsync() async {
    print('start');
    bool ret = await longWait('async');
    return ret;
}

main() async {
 var b = await myAsync();
  print(b);
}
```

### typedef
Think of `typedef` is similar to class interfaces, that is,
you create a contract which requires a specific input type
as well as a specific output type. The typedef is
useful for making callbacks interfaces (aka contracts).

In the example below, we create typedef of a function
called `LoggerFxn` which takes in a `String` and a returns `void`.
Now any function that does not meet that contract requirements
defined by `typedef void LoggerFxn(String msg)` should return
an error.
```dart
// make function interface (contract)
typedef void LoggerFxn(String msg);

class Logger {
  LoggerFxn out;
  Logger() {
    // upon construction, assign the print function to the out variable 
    out = print;
  }
  void log(String msg) {
    out(msg);
  }
}

// notice that this function fits the definition of LoggerFxn
void timeStampFxn(String msg) {
  String timeStamp = new DateTime.now().toString(); 
  print('${timeStamp}: $msg');
}

main() {
  Logger logger = new Logger();
  logger.out('hello');
  
  // override the out method with timeStampFxn
  // This works since timeStampFxn meets the requirements
  // that was defined by the typedef of LoggerFxn
  logger.out = timeStampFxn;
  logger.out('hello again');
}
```


### Class variables


### Final vs. Const 


### Interfaces
Interfaces are contracts that enforced upon a Class.
In this case the interface is declared using `abstract class Warrior`.
The code below does not run because the `Ninja` class does not
follow what the interface has defined, specifically `Ninja` does
not declare an `equip` method with parameter `weapon`.
```
abstract class Warrior {
  equip(weapon);
} 

class Sword {
}

class Ninja implements Warrior {
  // if i don't implement the equip() method, I get an error
}

class Pirate implements Warrior {
  equip(weapon) {
    print('yarr!');
  }
}

equipForBattle(warrior) {
  warrior.equip(new Sword());
}

void main() {
  //equipForBattle(new Ninja());
  equipForBattle(new Pirate());
}
```

### Files
```dart
import 'dart:convert';
import 'dart:io';
import 'dart:async';

Future getFileData() async {
   var x = await new File('words5.json').readAsString();
   var y = await JSON.decode(x);
   return y;
}

main() async {

  var jdata = await getFileData();

}
```

## Resources
https://www.dartlang.org/guides/language/language-tour

https://dartpad.dartlang.org/

https://flutter.io/cookbook/