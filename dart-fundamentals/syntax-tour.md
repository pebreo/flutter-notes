
### `this`
```dart
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
}

foo({bool x}) {
    print(x);
}

baz(bool y) {
  print(y);
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

### Class variables


### Final vs. Const 



## Resources
https://www.dartlang.org/guides/language/language-tour

https://dartpad.dartlang.org/

https://flutter.io/cookbook/