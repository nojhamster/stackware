stackware
=========

Stackware is a basic connect-style middleware handler for **node.js**, used for pushing objects through a list of functions, modifying them and handling errors.

## Installation
 _will come when published on npm_

## Usage

```javascript
  var Stackware = require('stackware');
  var sw        = new Stackware();
  
  sw.use(function middleware1(arg1, arg2, next) {
    arg1.foo = 'bar';
    next();
  });
  sw.use(function middleware2(arg1, arg2, next) {
    arg2.bar = 'foo';
    next();
  });
  sw.use(function middleware2(err, arg1, arg2, next) {
    console.error('An error occured, stop here');
  });
```

## Documentation

### Class: Stackware

Create a Stackware object.

```javascript
var Stackware = require('stackware');
var sw        = new Stackware();
```

### Methods

#### use
 _doc soon_
#### handle
 _doc soon_
