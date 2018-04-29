

## JSON
```dart
import 'dart:convert';

class Message {
  String user = 'Android';
  final String type;
  final String message;

  Message({this.type, this.message, this.user});

  Message.fromJson(Map<String, dynamic> json)
      : type = json['type'],
        message = json['message'],
        user = json['user'];

  Map<String, dynamic> toJson() =>
    {
      'type': type,
      'message': message,
      'user': user
    };
}

// USAGE
var msg = new Message(type:'chat_message', message:_controller.text, user: widget.user.name);

json.encode(msg)

```

### WEBSOCKET

```dart

import 'package:flutter/foundation.dart';
import 'package:web_socket_channel/web_socket_channel.dart';
import 'package:flutter/material.dart';
import 'package:lyric_maker/chat/globals.dart' as globals;
import 'package:lyric_maker/chat/askroom_page.dart';
import 'dart:convert';

class Message {
  String user = 'Android';
  final String type;
  final String message;

  Message({this.type, this.message, this.user});

  Message.fromJson(Map<String, dynamic> json)
      : type = json['type'],
        message = json['message'],
        user = json['user'];

  Map<String, dynamic> toJson() =>
    {
      'type': type,
      'message': message,
      'user': user
    };
}


class RoomPage extends StatefulWidget {
  final PersonData user;
  final WebSocketChannel channel;
  const RoomPage({Key key, this.user, this.channel}) : super(key: key);
  // connect the widget to the state
  @override
  State createState() => new RoomPageState();
}


class RoomPageState extends State<RoomPage> {

  final List<Message> messages = [
    new Message(type:'chat_type', message:'hello', user:'fred'),
    new Message(type:'chat_type', message:'hola', user:'wilma'),
  ];

 TextEditingController _controller = new TextEditingController();


  @override
  Widget build(BuildContext context) {

    Widget _buildTiles(model) {
       return ListView.builder(
            itemCount: messages.length,
            itemBuilder: (_, int i) {
              return new ListTile(
                // Resolve the path of an image on the server, using the `basePath`
                // of our `restApp`.
                leading: new Image.network(
                    'https://upload.wikimedia.org/wikipedia/commons/4/4a/Profil_licnosti.png'),
                title: new Text(
                  messages[i].user,
                  style: new TextStyle(fontWeight: FontWeight.bold),
                ),
                subtitle: new Text(messages[i].message),
              );
            }); 
                     
    }

      Widget _myStream() {
        return new StreamBuilder(
              stream: widget.channel.stream,
              builder: (context, snapshot) {
                if(snapshot.hasData) {
                   var msg = json.decode(snapshot.data);
                   // rebuild when this happens
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

    Widget _material() {
      // var _model = new ChatModel();
      return new Material(
          // color: Colors.blueAccent,
          child: new Column(
            children: <Widget>[
              _myStream(),
              new Divider(height: 1.0),
              new Container(
                decoration:
                    new BoxDecoration(color: Theme.of(context).cardColor),
                child: new Padding(
                  padding: const EdgeInsets.only(left: 8.0, right: 8.0),
                  child: new TextField(
                    controller: _controller,
                    decoration:
                        new InputDecoration(labelText: 'Send a message...'),
                    onSubmitted: _sendMessage,
                  ),
                ),
              )
            ],
          ),
        );
    }

    return _material();
  }
  void _sendMessage(String msg) {
    if (_controller.text.isNotEmpty) {
      
      var msg = new Message(type:'chat_message', message:_controller.text, user: widget.user.name);
      
      print(json.encode(msg));
      widget.channel.sink.add(json.encode(msg));
      globals.messageHistory.add(msg);
      print(globals.messageHistory);
      _controller.clear();
      setState((){
        messages.add(msg);
      });
    }
  }

  @override
  void dispose() {
    widget.channel.sink.close();
    super.dispose();
  }
}

```