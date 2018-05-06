
#### Requirements
rxdart: 0.16.7

```dart
import 'package:flutter/material.dart';
import 'dart:async';
import 'package:rxdart/rxdart.dart';
import 'package:myapp/utils/flutter_stream_callbacks.dart';

void main() => runApp(new MyApp());
 

class MyApp extends StatelessWidget {
  static String appTitle = "Flutter Stream Friends";

  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: appTitle,
      theme: new ThemeData(
        primarySwatch: Colors.purple,
      ),
      home: new StreamBuilder(
          stream: new CounterScreenStream(appTitle),
          builder: (context, snapshot) => buildHome(
              context,
              snapshot.hasData
                  // If our stream has delivered data, build our Widget properly
                  ? snapshot.data
                  // If not, we pass through a dummy model to kick things off
                  : new CounterScreenModel(0, () {}, appTitle))),
    );
  }

  // The latest value of the CounterScreenModel from the CounterScreenStream is
  // passed into the this version of the build function!
  Widget buildHome(BuildContext context, CounterScreenModel model) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text(model.title),
      ),
      body: new Center(
        child: new Text(
          'Button tapped ${ model.count } time${ model.count == 1
              ? ''
              : 's' }.',
        ),
      ),
      floatingActionButton: new FloatingActionButton(
        // Use the `StreamCallback` here to wire up the events to the Stream.
        onPressed: model.onFabPressed,
        tooltip: 'Increment',
        child: new Icon(Icons.add),
      ),
    );
  }
}

class CounterScreenStream extends Stream<CounterScreenModel> {
  final Stream<CounterScreenModel> _stream;

  CounterScreenStream(String title,
      [VoidStreamCallback onFabPressed, int initialValue = 0])
      : this._stream = createStream(
            title, onFabPressed ?? new VoidStreamCallback(), initialValue);

  @override
  StreamSubscription<CounterScreenModel> listen(
          void onData(CounterScreenModel event),
          {Function onError,
          void onDone(),
          bool cancelOnError}) =>
      _stream.listen(onData,
          onError: onError, onDone: onDone, cancelOnError: cancelOnError);

  // The method we use to create the stream that will continually deliver data
  // to the `buildHome` method.
  static Stream<CounterScreenModel> createStream(
      String title, VoidStreamCallback onFabPressed, int initialValue) {
    return new Observable(onFabPressed) // Every time the FAB is clicked
        .map((_) => 1) // Emit the value of 1
        .scan(
            (int a, int b, int i) => a + b, // Add that 1 to the total
            initialValue)
        // Before the button is clicked, kick everything off by emitting 0
        .startWith(initialValue)
        // Convert the latest count and the event handler into the Widget Model
        .map((int count) => new CounterScreenModel(count, onFabPressed, title));
  }
}

class CounterScreenModel {
  final String title;
  final int count;
  final VoidCallback onFabPressed;

  CounterScreenModel(this.count, this.onFabPressed, this.title);

  // If you've got a custom data model for your widget, it's best to implement
  // the == method in order to take advantage the performance optimizations
  // offered by the `Streams#distinct()` method. This will ensure the Widget is
  // repainted only when the Model has truly changed.
  @override
  bool operator ==(Object other) =>
      identical(this, other) ||
      other is CounterScreenModel &&
          runtimeType == other.runtimeType &&
          title == other.title &&
          count == other.count &&
          onFabPressed == other.onFabPressed;

  @override
  int get hashCode => title.hashCode ^ count.hashCode ^ onFabPressed.hashCode;

  @override
  String toString() =>
      'CounterScreenModel{title: $title, count: $count, onFabPressed: $onFabPressed}';
}


```

### myapp/utils/flutter_stream_callbacks.dart

```dart


import 'dart:async';
import 'package:flutter/gestures.dart';
import 'package:flutter/material.dart';

/// It's a stream and a callback in one. It's a StreamCallback!
///
/// This class is meant to convert Flutter events, such as Taps or Drags, into a
/// Stream of those events. This is useful when creating applications that rely
/// more heavily on stream-based architectures.
abstract class StreamCallback<T> extends Stream<T> implements Function {
  /// When creating StreamCallbacks, you can simply implement the correct `call`
  /// method for the given callback you want to support, forwarding all event
  /// data into this streamController via `streamController.add(T)`
  final StreamController<T> streamController =
      new StreamController<T>.broadcast(sync: true);

  @override
  StreamSubscription<T> listen(
    void onData(T event), {
    Function onError,
    void onDone(),
    bool cancelOnError,
  }) {
    if (streamController.onCancel == null) {
      streamController.onCancel = () {
        streamController.close();
      };
    }

    return streamController.stream.listen(
      onData,
      onError: onError,
      onDone: onDone,
      cancelOnError: cancelOnError,
    );
  }
}

/// Handles [VoidCallback] events
///
/// Unfortunately, you cannot create void value streams in Dart, in
/// the same way you can create a callback with no parameters. Therefore, the
/// Null class is used, and should be ignored.
class VoidStreamCallback extends StreamCallback<Null> {
  void call() => streamController.add(null);
}

/// The base single-value implementation
///
/// Extend this class with a simple type parameter to create a new
/// StreamCallback if the callback consists of only a single value.
class ValueStreamCallback<T> extends StreamCallback<T> {
  void call(T value) => streamController.add(value);
}

/// Handles [GestureDragDownCallback] events
class DragDownStreamCallback extends ValueStreamCallback<DragDownDetails> {}

/// Handles [GestureDragStartCallback] events
class DragStartStreamCallback extends ValueStreamCallback<DragStartDetails> {}

/// Handles [GestureDragUpdateCallback] events
class DragUpdateStreamCallback extends ValueStreamCallback<DragUpdateDetails> {}

/// Handles [GestureDragEndCallback] events
class DragEndStreamCallback extends ValueStreamCallback<DragEndDetails> {}

/// Handles [GestureDragCancelCallback] events
class DragCancelStreamCallback extends VoidStreamCallback {}

/// Handles [GestureLongPressCallback] events
class LongPressStreamCallback extends VoidStreamCallback {}

/// Handles [GestureMultiTapDownCallback] events
class MultiTapDownStreamCallback extends StreamCallback<MultiTapDownEvent> {
  void call(int pointer, TapDownDetails details) =>
      streamController.add(new MultiTapDownEvent(pointer, details));
}

/// Encapsulates all parameters of the [GestureMultiTapDownCallback] event
class MultiTapDownEvent {
  final int pointer;
  final TapDownDetails details;

  MultiTapDownEvent(this.pointer, this.details);
}

/// Handles [GestureMultiTapUpCallback] events
class MultiTapUpStreamCallback extends StreamCallback<MultiTapUpEvent> {
  void call(int pointer, TapUpDetails details) =>
      streamController.add(new MultiTapUpEvent(pointer, details));
}

/// Encapsulates all parameters of the [GestureMultiTapUpCallback] event
class MultiTapUpEvent {
  final int pointer;
  final TapUpDetails details;

  MultiTapUpEvent(this.pointer, this.details);
}

/// Handles [GestureMultiTapCallback] events
class MultiTapStreamCallback extends ValueStreamCallback<int> {}

/// Handles [GestureMultiTapCancelCallback] events
class MultiTapCancelStreamCallback extends ValueStreamCallback<int> {}

/// Handles [GestureScaleStartCallback] events
class ScaleStartStreamCallback extends ValueStreamCallback<ScaleStartDetails> {}

/// Handles [GestureScaleUpdateCallback] events
class ScaleUpdateStreamCallback
    extends ValueStreamCallback<ScaleUpdateDetails> {}

/// Handles [GestureScaleEndCallback] events
class ScaleEndStreamCallback extends ValueStreamCallback<ScaleEndDetails> {}

/// Handles [GestureTapDownCallback] events
class TapDownStreamCallback extends ValueStreamCallback<TapDownDetails> {}

/// Handles [GestureTapUpCallback] events
class TapUpStreamCallback extends ValueStreamCallback<TapUpDetails> {}

/// Handles [GestureTapCallback] events
class TapStreamCallback extends VoidStreamCallback {}

/// Handles [GestureTapCancelCallback] events
class TapCancelStreamCallback extends VoidStreamCallback {}

/// Handles [DismissDirectionCallback] events
class DismissDirectionStreamCallback
    extends ValueStreamCallback<DismissDirection> {}

/// Handles [DraggableCanceledCallback] events
class DraggableCanceledStreamCallback
    extends StreamCallback<DraggableCanceledEvent> {
  void call(Velocity velocity, Offset offset) =>
      streamController.add(new DraggableCanceledEvent(velocity, offset));
}

/// Encapsulates all parameters of the [DraggableCanceledCallback] event
class DraggableCanceledEvent {
  final Velocity velocity;
  final Offset offset;

  DraggableCanceledEvent(this.velocity, this.offset);
}

/// Handles generic [ValueChanged] events
class ValueChangedStreamCallback<T> extends StreamCallback<T> {
  void call(T value) => streamController.add(value);
}

/// Handles [RefreshCallback] events
///
/// In order to use a `RefreshIndicator` widget, you must provide a
/// `Future<Null>` to the `onRefresh` callback. When the `Future` completes,
/// the indicator will disappear.
///
/// This callback creates a `Completer<Null>` every time it is called. The
/// Completer is then emitted to any listener. You can then use
/// `completer.complete()` to indicate your async operation is done, and the
/// `RefreshIndicator` will be hidden.
class RefreshStreamCallback extends StreamCallback<Completer<Null>> {
  Future<Null> call() {
    final completer = new Completer<Null>();

    streamController.add(completer);

    return completer.future;
  }
}
```

