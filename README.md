# heroku-log-session

## Usage

### Server

```javascript
var express    = require('express');
var logSession = require('heroku-log-session');
var app        = express();

app.get('/:app', function(req, res) {
  var token   = process.env.HEROKU_API_TOKEN;
  var session = logSession(token);
  session.sse(req.params.app, req, res);
});

app.listen(process.env.PORT || 5000);
```

### Client

```javascript
var source      = new EventSource('/my-app-name');
var linesLogged = 0;

source.addEventListener('message', function(message) {
  document.writeln(message.data);
  linesLogged++;

  // At some point, you'll also want to close the event source when
  // you're done with it. We're closing it after logging 100 lines.
  if (linesLogged === 100) {
    source.close();
  }
});
```
