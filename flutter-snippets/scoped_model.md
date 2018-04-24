

```dart
import 'package:scoped_model/scoped_model.dart';

  Widget build(BuildContext context) {
    // First, create a `ScopedModel` widget. This will provide 
    // the `model` to the children that request it. 
    return new ScopedModel<CounterModel>(
      model: new MyModel(),
      child:     
    );
  }
```


```dart
    new ScopedModelDescendant<CounterModel>(
            builder: (context, child, model) { 
            new Text(
                model.counter.toString()
            }
    );
```