# Dart and web APIs


### HttpRequest
```dart
import 'dart:html';

main() {
  HttpRequest request = new HttpRequest(); 
}
```


### Websockets (Javascript)
```javascript
var socket = new WebSocket('ws://' + window.location.host + '/users/');

socket.onopen = function open() {
  console.log('WebSockets connection created.');
};
```