

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

### Class variables


### Final vs. Const 



## Resources
https://www.dartlang.org/guides/language/language-tour

https://dartpad.dartlang.org/

https://flutter.io/cookbook/