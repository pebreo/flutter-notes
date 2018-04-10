

### Named parameters
```
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
```
var mylist = String<List>();
var mylist = <List>[]
```

### Constructors
```
class Person {
    String name;

    Person(this.name);
}

var p = Person('john')
```

### Getters
```
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