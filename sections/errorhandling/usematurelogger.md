# Use a mature logger to increase errors visibility


### One Paragraph Explainer

We all loovve console.log but obviously a reputable and persisted Logger like Winston, Bunyan or L4JS is mandatory for serious projects. A set of practices and tools will help to reason about errors much quicker – (1) log frequently using different levels (debug, info, error), (2) when logging, provide contextual information as JSON objects, see example below. (3) watch and filter logs using a log querying API (built-in in most loggers) or a log viewer software 
(4) Expose and curate log statement for the operation team using operational intelligence tool like Splunk



### Code Example – Winston Logger in action

```javascript
//your centralized logger object
var logger = new winston.Logger({
 level: 'info',
 transports: [
 new (winston.transports.Console)(),
 new (winston.transports.File)({ filename: 'somefile.log' })
 ]
 });
 
//custom code somewhere using the logger
logger.log('info', 'Test Log Message with some parameter %s', 'some parameter', { anything: 'This is metadata' });

```

### Code Example – Querying the log folder (searching for entries)

```javascript
var options = {
    from: new Date - 24 * 60 * 60 * 1000,    until: new Date,    limit: 10,    start: 0,
    order: 'desc',    fields: ['message']
  };
 
 
  // Find items logged between today and yesterday. 
  winston.query(options, function (err, results) {
    //callback with results
  });

```

### Blog Quote: "Logger Requirements"
 From the blog Strong Loop
 
 > Lets identify a few requirements (for a logger):
1. Time stamp each log line. This one is pretty self explanatory – you should be able to tell when each log entry occured.
2. Logging format should be easily digestible by humans as well as machines.
3. Allows for multiple configurable destination streams. For example, you might be writing trace logs to one file but when an error is encountered, write to the same file, then into error file and send an email at the same time…
 