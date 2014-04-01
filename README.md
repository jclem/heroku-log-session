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
```

### Client

*...*
