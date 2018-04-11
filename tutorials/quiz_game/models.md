

## The Question & Quiz data models


We create a `Question` class and we will instatiate
new questions and pass in those new questions as a list to
the `Quiz` class. The quiz class will have a property
that takes in a list of `Question` objects.

The reason we are defining two separate classes is because
a quiz can have many questions. So, we are going to implement
that in our data structure by having a `Quiz` object that accepts
multiple `Question` objects.

### The Question class

To start, our `Question` class will have two object properties: question and answer.
For simplicity, I am dynamically typing them. Notice the constructor
syntax looks like `MyClass(this.myproperty)`.

```dart
class Question {
  var question;
  var answer;
  
  // constructor
  Question(this.question, this.answer);

}
```
Before I describe what the `Quiz` class looks like, let's see
how we would like our API to work:
```dart
var question = new Question("The sky is blue", true);
var quiz = new Quiz([question]);
```
Or we can write it more succinctly by instatiating an object
inside the list:
```dart
var quiz = new Quiz([new Question("The sky is blue.", true)]);
```

### The Quiz class 

The `Quiz` class will have the following properties:

* A list/array of questions. This will contain a collection 
(by collection I mean a group of things) of questions objects.

* To keep track of which question the player is working on,
we create the `currentQuestionIndex` property. That will be used
as a list index in our `nextQuestion` getter method.

* We record the player's score with the `score` property. 

```dart
class Quiz {

    var questions;
    var currentQuestionIndex = -1;
    var score = 0;
    
    Quiz(this.questions);
    get length => questions.length;
    
    get nextQuestion {
        currentQuestionIndex++;
        if(currentQuestionIndex >= this.length) return null;
                return questions[currentQuestionIndex];
    } 
  
    answer(bool isCorrect) {
      if(isCorrect) score++;
    }
}
```
##### The constructor and getters
In Dart, we can simply create a constructor with syntax like:
`MyClass(this.myproperty)`. In our case, we initalize 
the `questions` property so it looks like `Quiz(this.questions)`.
For our getter, we use the keyword `get` and the arrow function syntax.
Using the current syntax, using a getter is redundant, but
when we make the variables private, then it will matter.

##### The `nextQuestion` getter method
We create the `nextQuestion` getter method and it takes 
no parameters as you can see. The way it works is:

* Increment `currentQuestionIndex`
* Check whether the question index is greater than length, if so, return `null`
otherwise, we rutern the current item in the questions list.

##### The `answer` method
When the user gets the answer correct, we increment the `score` variable.
The `answer` method takes in a `bool` variable called `isCorrect`.

##### Running a simple example
Now, let's try running the code that we have so far. We can run
our Dart code in the browser using DartPad which is an online REPL: 

https://dartpad.dartlang.org/

Just copy and paste the code below and click "Run" button.
```dart
class Question {
  var question;
  var answer;
  
  // constructor
  Question(this.question, this.answer);

}

class Quiz {

    var questions;
    var currentQuestionIndex = -1;
    var score = 0;
    
    Quiz(this.questions);
    get length => questions.length;
    
    get nextQuestion {
        currentQuestionIndex++;
        if(currentQuestionIndex >= this.length) return null;
                return questions[currentQuestionIndex];
    } 
  
    answer(bool isCorrect) {
      if(isCorrect) score++;
    }
}

main() {
    var question = new Question("The sky is blue", true);
    var quiz = new Quiz([question]);
    var q = quiz.nextQuestion;
    print(q.question);
}
```
You should have gotten the following output:
```
The sky is blue
```
So that was the dynamically typed prototype for our data structure.
In the next section, I will explain how to enhance our code
by refactor our variable type declaration. We can make it easier
to debug, increase code maintainability, and increase program performance
using Dart's static types.
### Refactor for more specific types


Now let's add more specific types to our `Question` and `Quiz` classes.
The nice thing about Dart is you can quickly your prototype up and running
with dynamic variables, and when you are ready to optimize, you can
refactor for more static types. So, when you're first creating your data 
model just use declare variables with `var` or `num`. 

So assuming, we the basic behavior that we want with our data structures,
we now add more specific types to our variables' type declarations.

##### Refactor `Question` class

The first thing we'll do is make `question` a `final String` because tk.
Next we'll, change the type declaration for `answer` to `final bool`.
In Dart, a `final` variable means it is set only once. 

You might be wondering how `final` is different than `const`? Well, `const` 
is more appropriate for numbers whereas `final` can be used for objects or 
instance variables (aka object properties). In our case, we are
declaring object properties so we use `final`.

```dart
class Question {
  final String question;
  final bool answer;
  
  Question(this.question, this.answer);
}
```


##### Refactor `Quiz` class 
One thing I like about Dart is that making variables private
is as easy as putting an underscore in front of the variable name. 
You'll notice that we changed all the instance variables to private.
I also specified `_questions` as a `List` of type `Question`.
The `List<Question>` syntax is a so-called generic (aka parametized)
type. I like calling it parametized because it is more descriptive and 
I can visualize the generic type taking in another type as parameter.

For more details about generic types in Dart checkout out [Dart Tour page](https://www.dartlang.org/guides/language/language-tour#generics).

A tip about refactoring: you'll save time if you use your IDE's "rename variables"
or "factor variable" feature to automatically rename all variables in that file or project.
If you are working in just one file, then you can just use Find/Replace feature of your editor.

##### Refactor `Quiz` constructor
Because we want to randomize the questions given to the user, we 
will use the built-in `shuffle()` method which comes with Dart.
After refactoring, our constructor just increased by one line and a couple of curly brackets
but really the only thing we had to change was running a method on our `_question` variable
upon instantiation. 

##### Full working code
After refactoring, let's now run the code again.


let's run out code. As before, copy and paste tk.
```dart
class Quiz {
  // private because of underscore
  List<Question> _questions;
  int _currentQuestionIndex = -1;
  int _score = 0;

  
  Quiz(this._questions) {
    _questions.shuffle();
  }

  // getters
  List<Question> get questions => _questions;
  int get length => _questions.length;
  int get questionNumber => _currentQuestionIndex+1;
  int get score => _score;

  // getter method
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
Note  that private variables are only accessible in that file but
not if you important that class from another file.


##### Full refactored classes
```dart

void main() {
    var q1 = new Question('The sky is blue', true);
    var q2 = new Question('Summer is hot', true);
    var quiz = new Quiz([q1,q2]);

}
class Question {
  final String question;
  final bool answer;
  
  Question(this.question, this.answer);
}


class Quiz {
  // private because of underscore
  List<Question> _questions;
  int _currentQuestionIndex = -1;
  int _score = 0;

  
  Quiz(this._questions) {
    _questions.shuffle();
  }

  // getters
  List<Question> get questions => _questions;
  int get length => _questions.length;
  int get questionNumber => _currentQuestionIndex+1;
  int get score => _score;

  // getter method
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

#### make private models and 
```
```