---
layout: post
published: true
title: Learning JavaScript 1 : talk about synchronous and asynchronous
---

The following talk about is at [Trailing commas in function parameter lists and calls](http://www.2ality.com/2015/11/trailing-comma-parameters.html). 
This blog post explains it.

## Synchronously ##
Synchronous sequential execution is built into JavaScript and looks like this:
```
    function func() {
        foo();
        bar();
        baz();
    }
```

## Asynchronously via Promises ##
To execute Promise-based functions sequentially, you need to chain function calls via then(), which is the Promise equivalent of the semicolon:
```
    function func() {
        return foo()
            .then(() => bar())
            .then(() => baz());
    }
```
If you are OK with executing the functions in an arbitrary order (the single-threaded version of “in parallel”), you can use Promise.all():
```
    function func() {
        return Promise.all([foo(), bar(), baz()]);
    }
```

## Asynchronously, via the library co ##
[The library co](https://github.com/tj/co) also works with Promise based functions. 
Let’s look at an example:
```
    const func = co.wrap(function* () {
        yield foo();
        yield bar();
        yield baz();
    });
```
co works very much like [async functions](https://github.com/tc39/ecmascript-asyncawait), a proposed ECMAScript feature.

## Further reading ##
-   [Async Functions for ECMAScript](https://github.com/tc39/ecmascript-asyncawait) (ECMAScript proposal)
-   “[Promises for asynchronous programming](http://exploringjs.com/es6/ch_promises.html)” (chapter in “Exploring ES6”)
        -   “[Asynchronous programming (background)](http://exploringjs.com/es6/ch_async.html)” (background for the chapter on Promises)