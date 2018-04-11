


## Animation

1. Create the controller
2. Create the animation object
3. Utilize the animation object to transform text value or sizing of an element on the screen


#### Setup

First we add the `SingleTickerProviderStateMixin` mixin to the Widget class and declare the
a `Animation` object and a `AnimationController` object. The animation object returns a 
double from 0.0 to 1.0. So when we transform something, it will be from 0 percent to 100%.
```dart

class MyTextState extends State<MyText> with SingleTickerProviderStateMixin {
  Animation<double> _animation;
  AnimationController _controller;
  // ...
}
```

Next we instatiate the animation and controller objects.
```dart
@override
void initState() {
super.initState();
    _controller = new AnimationController(duration: new Duration(milliseconds: 500), vsync: this);
    _animation = new CurvedAnimation(parent: _controller, curve: Curves.bounceOut);
    _animation.addListener(() => this.setState(() {})); 
    _controller.forward(); 
}
```
Note that we must define the listener callback that does nothing. The `setState()` method affects all instance variables, that is, usually instances of the widget that you call it in.

#### Usage 

To add animation, simply insert the animation object 
```dart
new TextStyle(fontSize: _animation.value * 15),
```
This works because we add the special mixin `SingleTickerProviderStateMixin` which will increment
the `_animation.value` from 0.0 to 1.0, in other words from 0 to 100%.


#### Resetting 
The animation will only run once if we do not override the `didUpdateWidget`. The controller
has to be rest like this:
```dart
  @override
  void didUpdateWidget(QuestionText oldWidget) {
    super.didUpdateWidget(oldWidget);
    if(oldWidget._question != widget._question) {
      _animation.reset();
      _controller.forward();
    }
  }
```



## TODO

Stateful vs Stateless widget

