#Quindar Tutorial

#Logging
This tutorial will demonstrate how to make use of winston, morgan, and file stream rotator to display log information on the console.

##Steps Involved
Use morgan, winston and file-stream-rotator library in server.js.

```javascript
// logging
var syslogger = require('morgan');
var logger = require('winston');
var FileStreamRotator = require('file-stream-rotator');

var logDirectory = __dirname + '/log';
var accessLogStream = FileStreamRotator.getStream({
  date_format: 'YYYYMMDD',
  filename: logDirectory + '/access-%DATE%.log',
  frequency: 'daily',
  verbose: false
});
app.use(syslogger('combined', {stream: accessLogStream}));

```
In this way we can make use of winston, morgan or file stream rotator in our example. For example, now we can use logger to display information on console.

```javascript
// example 1: in-line REST API
app.get('/verifyMe', function(req, res) {
  // Optional: we can add cross-domain support here so that local browser with localhost domain can still access this web service
  //res.setHeader('Content-Type', 'application/json');
  //res.header("Access-Control-Allow-Origin", "*");
  //res.header("Access-Control-Allow-Headers", "X-Requested-With");

  console.log(".../verifyMe is invoked at " + new Date());
  logger.log("info", ".../verifyMe is invoked at " + new Date());
  logger.info("No cross-domain policy (CORS) is enabled yet. Please enable for remote API use.");

  /** example 2: if you add this block, the REST API /verifyMe will always fail because err (handler) is always true
  if (err) {
    return res.status(500).send({"status": 500, "message": "Quindar server is not running due to internal server error",
        "error": err})
  };
  **/
  return res.status(200).send({"status": 200, "message": "Quindar platform is alive"});
});
```
Notice the logger variable is now being used to display information instead of using console.log().



