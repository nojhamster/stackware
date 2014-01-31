stackware
=========

Stackware is a basic connect-style middleware handler for **node.js**, used for pushing objects through a list of functions, modifying them and handling errors.

## Installation
 ```
npm install stackware
```

## Usage

```javascript
  var Stackware = require('stackware');
  var sw        = new Stackware();
  
  sw.use(function middleware1(obj1, obj2, next) {
    obj1.foo = 'bar';
    next();
  });
  sw.use(function middleware2(obj1, obj2, next) {
    obj2.bar = 'foo';
    // stop here
  });
  sw.process(obj1, obj2);
```

## Documentation

### Class: Stackware

Create a Stackware object.

```javascript
var Stackware = require('stackware');
var sw        = new Stackware();
```

### Methods

#### use(function)
Add a middleware to the stack. It can be either a function or an object providing a `handle` function. It will be called with the same arguments given to `process` (see below), plus a callback function which can take an error.
```javascript
 function Middleware() {}
 Middleware.prototype.handle = function (obj1, obj2, next) { next(); };
 
 // Object with handle function
 sw.use(new Middleware());
 
 // Function
 sw.use(function (obj1, obj2, next) {
   obj1.foo = 'bar';
   next();
 });
 
 sw.process(obj1, obj2);
```
When the callback is called with an error, further middlewares will be skipped until we reach an error handler. It's basically a middleware with an `error` argument prepended to the others.

```javascript
 sw.use(function middleware1(obj, next) {
   next(new Error('Something happened'));
 });
 sw.use(function errorHandler(err, obj, next) {
   console.log(err);
 });
 sw.process(obj);
```

#### process(obj1, obj2, ...)
Push any number of objects through the middlewares.  
**NB**: only variables passed by reference can be changed inside the middlewares (i.e. objects, arrays).
