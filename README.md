webwork.js
=======

Execute Web Workers without external files

Usage is as really simple:

```javascript
callableWebworker = webwork(callback);
```
`callback` takes a single data argument and should return the result  
`callableWebworker` is a function that takes the data to send and  
a node style callback ie `function(err, result) {}`

## [JSBin Demo](http://jsfiddle.net/uqcFM/60/)

## Example
```javascipt
var goodWorker = webwork(function (data) {
    return "!!" + data  + "!!";
});
var badWorker = webwork(function (data) {
    return "!!" + data + imNotDefined + "!!";
});

goodWorker("Test123", function(err, result) {
    if (err) return alert("goodWorker Errored with " + err.message);
    alert("first goodWorker returned with " + result);
});
goodWorker("Test123", function(err, result) {
    if (err) return alert("goodWorker Errored with " + err.message);
    alert("second goodWorker returned with " + result);
});
badWorker("Test456", function(err, result) {
    if (err) return alert("badWorker Errored with " + err.message);
    alert("badWorker returned with " + result);
});
alert("Since webworkers are async this should happen first.\nThe callbacks may fire in any order");
```

The astute may realize that they can access the `event` variable inside the callback.  
Also since the callback is stringified and injected into the webworker, you don't have access to any vars in scope
