
### method 1 - google-services.json
```dart
// Demonstrates configuring to the database using a file
_counterRef = FirebaseDatabase.instance.reference().child('counter');
```

### method 2 - auth parameters
```dart
// Demonstrates configuring the database directly
final FirebaseDatabase database = new FirebaseDatabase(app: widget.app);
_messagesRef = database.reference().child('messages');
```

### flow - counter
```dart


// setup
int _counter;
_counterRef = FirebaseDatabase.instance.reference().child('counter');

// add stream and run setState
_counterSubscription = _counterRef.onValue.listen((Event event) {
  setState(() {
    _error = null;
    _counter = event.snapshot.value ?? 0;
  });

// button
onPressed: _increment,

// display counter
new Text(
  'Button tapped $_counter time${ _counter == 1 ? '' : 's' }.\n\n'
      'This includes all devices, ever.',
)


// update db (and increment counter) in database using runTransaction
final TransactionResult transactionResult =
    await _counterRef.runTransaction((MutableData mutableData) async {
  mutableData.value = (mutableData.value ?? 0) + 1;
  return mutableData;
});


// cleanup
 @override
  void dispose() {
    super.dispose();
    _counterSubscription.cancel();
  }

```

### flow - message
```dart
// setup

// add stream 

// button

// push to db

// display message


```

### Resources

https://raw.githubusercontent.com/flutter/plugins/master/packages/firebase_database/example/lib/main.dart