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

#### The pages involved

We will create 3 pages:

* `LandingPage`
* `AskRoomPage`
* `RoomPage`

#### Websocket setup
We begin with the most important part which is connecting 
the client to the websockets. Making the connection,
is just a matter of instantationing the `IOWebSocketChannel` class.

We instatiate and pass it as a parameter like this:
```dart
var chan = new IOWebSocketChannel.connect('ws://10.0.2.2:8000/ws/chat/' + person.room + '/' + person.name);
var route = new MaterialPageRoute(
  builder: (BuildContext context) =>
      new RoomPage(user:person, channel: chan)
);
Navigator.of(context).push(route);
```

Once we connect, we then need to handle any events 
that the client needs to listen to. When something happens,
we then rebuild the widget. Note that only stateful widgets
have this ability, not stateless widgets.

#### Receiving data from the websocket

We will use Flutter's built-in streaming API by wrapping
the  `StreamBuilder` class around the widget that will be
updated. Something like this:

```dart
Widget _myStream() {
    return new StreamBuilder(
          // Here, widget is equivalent to 'this'
          stream: widget.channel.stream,
          builder: (context, snapshot) {
            // Snapshot is from the websocket stream
            if(snapshot.hasData) {
               var msg = json.decode(snapshot.data);
               // rebuild widget when we change the messages List
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

#### Sending data to the websocket

As the user, you want to be able send the message when you 
fill out the form. The property you need to attach a function to
is `onSubmitted` in the `TextField` widget.  

```dart
new TextField(
    controller: _controller,
    decoration:
        new InputDecoration(labelText: 'Send a message...'),
    onSubmitted: _sendMessage,
),
```

The `onSubmitted` property expects a function. For clarity, I like to
put functions that will be used as properties of widgets into
their own functions. In this case, we define a void function 
called `_sendMessage`.

```dart
  void _sendMessage(String msg) {
    if (_controller.text.isNotEmpty) {
      // Create Message instance that will be serialized
      var msg = new Message(type:'chat_message', message:_controller.text, user: widget.user.name);
      
      // Send to websocket via the stream
      //  also, serialize the instance using json.encode()
      widget.channel.sink.add(json.encode(msg));
      
      globals.messageHistory.add(msg);
      _controller.clear();
    
       // trigger rebuild of widget
      setState((){
        messages.add(msg);
      });

    }
  }
```

Finally, when we exit the `RoomPage` stateful widget we must
clean up and close our websocket stream like this:
```dart
@override
void dispose() {
    widget.channel.sink.close();
    super.dispose();
}
```


## Server

#### The views involved


#### The routes involved

Channels routing is similar to URLs routing in Django. 
If you need to use the url parameters in your consumer methods, 
you can use `tk`. 


#### `consumers.py`

Each class is a `tk` and within each class you must define
three methods: connect, disconnect, tk.



Django Channels is the django implementation of the websocket protocol.
In contrast to HTTP, the websocket protocol allows you to broadcast
to clients without a formal request. The only thing that the client
has to do is to "plug in" to the websocket address, usually
something like this `ws://mysite.com/mypath`.

There are 3 files you need to setup in Django to enable websockets
* The `mysite/routing.py`
* The `myapp/routing.py`
* The `myapp/consumers.py`

Be sure to setup you `pyenv` environment to Python 3.6 because
Django Channels needs Python 3.5+. To do that type:
```bash
pyenv install 3.6.0
pyenv virtualenv 3.6.0 dj-channels
pyenv activate dj-channels
```
Then you'll need to `pip install` the following:
```
django==1.11
django-cors-headers==2.2.0
channels==2.1.0
```
I had an issue where installing Django channels would force install Django 2.0
which I didn't want. So had to pip uninstall django 2.0 like this:
```bash
pip unistall django
pip install django==1.11
```


## Chat example

I got the following example from the official tutorial for [Django Channels](https://channels.readthedocs.io/en/latest/tutorial/part_1.html). Below is my abridge digested version of it. If you scroll
down, I also put in the full working code.

#### Abridged server and client code

On the server side, the `message` object is passed to the consumer
which will handle the websocket message. The message object has a
special `reply_channel` that is the name of the socket which
that message was sent. For example `ws://foo.com/users` is a certain
channel and has a certain socket instance associated with it.

##### `chat/routing.py`
```python
# chat/routing.py
from django.conf.urls import url

from . import consumers

websocket_urlpatterns = [
    url(r'^ws/chat/(?P<room_name>[^/]+)/$', consumers.ChatConsumer),
]
```

##### `chat/consumers.py`
```
# chat/consumers.py
from channels.generic.websocket import WebsocketConsumer
import json

class ChatConsumer(WebsocketConsumer):
    def connect(self):
        self.accept()

    def disconnect(self, close_code):
        pass

    def receive(self, text_data):
        text_data_json = json.loads(text_data)
        message = text_data_json['message']

        self.send(text_data=json.dumps({
            'message': message
        }))

```

### client - abridged
```javascript
<script>
var roomName = {{ room_name_json }};

    var chatSocket = new WebSocket(
        'ws://' + window.location.host +
        '/ws/chat/' + roomName + '/');

    chatSocket.onmessage = function(e) {
        var data = JSON.parse(e.data);
        var message = data['message'];
        console.log(message);
    };
</script>
```

## Chat example: complete code

#### server - complete code
```python


```

#### client - complete code
```javascript

```