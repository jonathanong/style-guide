
## Use .request and .response

Koa delegates many properties from the `.request` and `.response` objects to `this`.
However, you should use these properties on the `.request` and `.response` objects instead.

The major reason is that it's clear whether the property belongs to the `request` or `response`.

```js
app.use(function* () {
  this.length
})
```

Does `this.length` refer to the `request` or `response` length?

Typing `this.request.length` and `this.response.length` is much clearer and less ambiguous.

```js
app.use(function* () {
  this.request.length
  this.response.length
})
```

## Avoid relying on custom `this.` properties

For example,
some people migrating from Express like to attach `this.request.body`:

```js
app.use(function* (next) {
  this.request.body = yield parse(this)
  yield* next
})
```

This could be a security issue as you might be unnecessarily parsing bodies, storing file, and increasing memory usage.
Instead, use tiny libraries instead and do asynchronous logic only when necessary:

```js
app.use(function* (next) {
  var user = yield User.get(this.session.userid)
  if (!user) this.throw(401, 'you have to login!')

  // parse body only after authentication
  var body = yield parse(this)
  // do stuff with the body
})
```

This is a little more work as now you'll need to `var parse = require('co-body')` everywhere.
However, it's much easier in Koa than other frameworks like Express because you don't have all those nested callbacks.

## Write new libraries in Promises

Now with ES6 Promises in node.js master,
Promises will be commonplace.
The problem with callbacks is that there's no standard behind them.
You don't know whether an arbitrary function is asynchronous.

There are libraries to [thunkify](https://github.com/visionmedia/node-thunkify) other libraries,
but these should only be stopgap solutions.
Write new libraries in promises, not generators, so people not using Koa can still use them.

For using node.js functions in Koa, you'll want to use [mz](https://github.com/visionmedia/node-thunkify).
