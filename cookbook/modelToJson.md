

```dart
import 'dart:convert';
import 'dart:mirrors';

// abstract class to serialize user
abstract class Serializable {
  
 Map toJson() {
   Map map = new Map();
   InstanceMirror im = reflect(this);
   ClassMirror cm = im.type;
   var decls = cm.declarations.values.where((dm)=> dm is VariableMirror);
   decls.forEach((dm){
     var key = MirrorSystem.getName(dm.simpleName);
     var val = im.getField(dm.simpleName).reflectee;
     map[key] = val;
   });
   return map;
 }
}

class Person extends Object with Serializable {
  String name;
  int age;
}

class User {
  final String name;
  final String email;

  User(this.name, this.email);

  User.fromJson(Map<String, dynamic> json)
      : name = json['name'],
        email = json['email'];

  Map<String, dynamic> toJson() =>
    {
      'name': name,
      'email': email,
    };
}


main() async {

  var c = new Person()
        ..name = 'foo'
    ..age = 3;
  print(c.toJson());

  
  final json = '{"name": "John Smith", "email": "john@example.com"}';
    print(json);
  Map userMap = JSON.decode(json);
    var user = new User.fromJson(userMap);
    print(user.toJson());
  
}
```

#### Sources

https://stackoverflow.com/questions/15866290/the-best-way-to-parse-a-json-in-dart

https://flutter.io/json/#use-manual-serialization-for-smaller-projects