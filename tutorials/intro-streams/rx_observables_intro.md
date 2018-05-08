

### Stream of numbers
```javascript
var source = Rx.Observable.range(1,5);

// create a callback in 
var subscription = source.subscribe(
    x => console.log('onNext: ' + x),
  e => console.log('error: ' + e.message),
  () => console.log('onComplete')
);
```
### Stream of numbers style#2
```javascript
console.clear();

var source = Rx.Observable.range(1,10);

var observer = Rx.Observer.create(
    x => console.log('onNext: ' + x),
  e => console.log('onError' + e.message),
  () => console.log('onCompleted')
);

source.subscribe(observer);
```

### Stream of numbers - convert from array
```javascript
console.clear();

var myarray = [1,2,3,4,5];

var source = Rx.Observable.from(myarray);

var subscription = source.subscribe(
    x => console.log('onNext: ' + x),
  e => console.log('error: ' + e.message),
  () => console.log('onComplete')
);
```

### Time stream
```javascript
// initial delay of 5 seconds, then 1 second intervals
var source = Rx.Observable.timer(5000,1000).timestamp();

var subscription = source.subscribe(
    x=> console.log(x.value + ': ' + x.timestamp)
);

```


### UI Streams
This example shows how we can use an observable to handle
mouse clicks by the user
```javascript

// create button 
var closeButton1 = document.querySelector('.close1');


// create observable 
var close1ClickStream = Rx.Observable.fromEvent(closeButton1, 'click');

// merge with another stream

var suggestion1Stream = createSuggestionStream(close1ClickStream);

function createSuggestionStream(closeClickStream) {
    return closeClickStream.startWith('startup click')
        .combineLatest(responseStream,             
            function(click, listUsers) {
                return listUsers[Math.floor(Math.random()*listUsers.length)];
            }
        )
        .merge(
            refreshClickStream.map(function(){ 
                return null;
            })
        )
        .startWith(null);
}

// attach observer
suggestion1Stream.subscribe(function (suggestedUser) {
    renderSuggestion(suggestedUser, '.suggestion1');
});

```

# Sources

playground:
https://jsfiddle.net/jgoemat/g5pj065m/

https://xgrommx.github.io/rx-book/content/getting_started_with_rxjs/exploring_major_concepts_in_rxjs.html

https://github.com/ReactiveX/RxPY

sandbox
http://jsfiddle.net/staltz/8jFJH/48/



# Full example
This demo lists people and when the user
clicks the 'X' button, the person is replaced.

It uses observables for button clicks and 
demonstrates how to combine stream information.
### javascript
```javascript
var refreshButton = document.querySelector('.refresh');
var closeButton1 = document.querySelector('.close1');
var closeButton2 = document.querySelector('.close2');
var closeButton3 = document.querySelector('.close3');

var refreshClickStream = Rx.Observable.fromEvent(refreshButton, 'click');
var close1ClickStream = Rx.Observable.fromEvent(closeButton1, 'click');
var close2ClickStream = Rx.Observable.fromEvent(closeButton2, 'click');
var close3ClickStream = Rx.Observable.fromEvent(closeButton3, 'click');

var requestStream = refreshClickStream.startWith('startup click')
    .map(function() {
        var randomOffset = Math.floor(Math.random()*500);
        return 'https://api.github.com/users?since=' + randomOffset;
    });

var responseStream = requestStream
    .flatMap(function (requestUrl) {
        return Rx.Observable.fromPromise($.getJSON(requestUrl));
    });

function createSuggestionStream(closeClickStream) {
    return closeClickStream.startWith('startup click')
        .combineLatest(responseStream,             
            function(click, listUsers) {
                return listUsers[Math.floor(Math.random()*listUsers.length)];
            }
        )
        .merge(
            refreshClickStream.map(function(){ 
                return null;
            })
        )
        .startWith(null);
}

var suggestion1Stream = createSuggestionStream(close1ClickStream);
var suggestion2Stream = createSuggestionStream(close2ClickStream);
var suggestion3Stream = createSuggestionStream(close3ClickStream);


// Rendering ---------------------------------------------------
function renderSuggestion(suggestedUser, selector) {
    var suggestionEl = document.querySelector(selector);
    if (suggestedUser === null) {
        suggestionEl.style.visibility = 'hidden';
    } else {
        suggestionEl.style.visibility = 'visible';
        var usernameEl = suggestionEl.querySelector('.username');
        usernameEl.href = suggestedUser.html_url;
        usernameEl.textContent = suggestedUser.login;
        var imgEl = suggestionEl.querySelector('img');
        imgEl.src = "";
        imgEl.src = suggestedUser.avatar_url;
    }
}

suggestion1Stream.subscribe(function (suggestedUser) {
    renderSuggestion(suggestedUser, '.suggestion1');
});

suggestion2Stream.subscribe(function (suggestedUser) {
    renderSuggestion(suggestedUser, '.suggestion2');
});

suggestion3Stream.subscribe(function (suggestedUser) {
    renderSuggestion(suggestedUser, '.suggestion3');
});

```

### html
```html
<div class="container">
    <div class="header">
         <h2>Who to follow</h2><a href="#" class="refresh">Refresh</a>
    </div>
    <ul class="suggestions">
        <li class="suggestion1">
            <img />
            <a href="#" target="_blank" class="username">this will not be displayed</a>
            <a href="#" class="close close1">x</a>
        </li>
        <li class="suggestion2">
            <img />
            <a href="#" target="_blank" class="username">neither this</a>
            <a href="#" class="close close2">x</a>
        </li>
        <li class="suggestion3">
            <img />
            <a href="#" target="_blank" class="username">nor this</a>
            <a href="#" class="close close3">x</a>
        </li>
    </ul>
</div>
<script src="http://cdnjs.cloudflare.com/ajax/libs/rxjs/2.2.26/rx.js"></script>
<script src="http://cdnjs.cloudflare.com/ajax/libs/rxjs/2.2.26/rx.async.js"></script>
<script src="http://cdnjs.cloudflare.com/ajax/libs/rxjs/2.2.26/rx.coincidence.js"></script>
<script src="http://cdnjs.cloudflare.com/ajax/libs/rxjs/2.2.26/rx.binding.js"></script>
<script src="http://cdnjs.cloudflare.com/ajax/libs/rxjs/2.2.26/rx.time.js"></script>
<script src="http://cdnjs.cloudflare.com/ajax/libs/rxjs-dom/2.0.7/rx.dom.js"></script>
```

### CSS
```css
body {
    font-family: sans-serif;
    padding: 10px;
}
h2 {
    font-weight: bold;
    display: inline-block;
}
.refresh {
    font-size: 80%;
    margin-left: 10px;
}
.header {
    background: #ECECEC;
    padding: 5px;
}
.suggestions {
    border: 2px solid #ECECEC;
}
li {
    padding: 5px;
}
li img {
    width: 40px;
    height: 40px;
    border-radius: 20px;
}
li .username, li .close {
    display: inline-block;
    position: relative;
    bottom: 15px;
    left: 5px;
}
```
