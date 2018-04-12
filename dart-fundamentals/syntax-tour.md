
### `this`
```dart
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

#### Example: Stateful Widget subclassing


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


## Resources
https://www.dartlang.org/guides/language/language-tour

https://dartpad.dartlang.org/

https://flutter.io/cookbook/