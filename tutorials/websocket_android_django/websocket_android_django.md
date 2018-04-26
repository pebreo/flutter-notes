# A Chat Room App using Flutter and Django-Channels (websockets)

In this tutorial, I will show you how to create a
simple chat application using Django Channels and Flutter for Android.
The concepts you will learn in this tutorial will be:

* Websockets in Django
* Serializing JSON from Django
* Serializing JSON from Flutter
* Sending a websocket messaging using StreamBuilder
* Refreshing the Flutter builder using `setState((){})`

For this tutorial, I will assume you have you development
environment already set up.

## Client

We begin with the most important part which is connecting 
the client to the websockets. Making the connection,
is just a matter of instantationing the `tk` class

Once we connect, we then need to handle any events 
that the client needs to listen to. When something happens,
we then rebuild the widget. Note that only stateful widgets
have this ability, not stateless widgets.

We will use Flutter's built-in streaming API by wrapping
the  `StreamBuilder` class around the widget that will be
updated. Something like this:

```dart
      Widget _myStream() {
        return new StreamBuilder(
              stream: widget.channel.stream,
              builder: (context, snapshot) {
                if(snapshot.hasData) {
                   var msg = json.decode(snapshot.data);
                   // rebuild widget when this happens
                   messages.add(new Message(type: 'chat_type', message: msg['message'], user: msg['user']));
                }
                return new Flexible(
                  child: messages.isEmpty
                      ? new Text(
                          'Nobody has said anything yet... Break the silence!')
                      : _buildTiles(messages),
                );
              },
            );
      }
``` 

The situations where we h

#### The pages involved

#### websocket connection

#### json communication



## Server

#### The views involved



#### The routes involved

Channels routing is similar to URLs routing in Django. 
If you need to use the url parameters in your consumer methods, 
you can use `tk`. 


#### `consumers.py`

Each class is a `tk` and within each class you must define
three methods: connect, disconnect, tk.

