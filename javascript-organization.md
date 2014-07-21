
Code should philosophically be ordered:

- From high level to lower level
- From public to private

Code in a single file should generally be structured in the following order:

1. Global imports - `require('lib')`
2. Relative imports - `require('./src')`
3. Variables - `var a = 1`
4. Exports - `module.exports = Main`
5. Main - `function Main() {}`
6. Prototype Properties - `Main.prototype.something = true`
7. Utilities - `function add(a, b) {return a + b}`

### Don't hoist variables

There's no need for that.

### Avoid defining (anonymous) functions within functions

```js
function sumArray(arr) {
  return arr.reduce(function (a, b) {
    return a + b
  }, 0)
}
```

should really be:

```js
function sumArray(arr) {
  return arr.reduce(reduceSum, 0)
}

function reduceSum(a, b) {
  return a + b
}
```

However, doing the same in the following example is unnecessary:

```js
function multiplyArray(x) {
  return arr.map(function (y) {
    return x * y
  })
}
```

### Move function declarations to the end of the closure and after the return statement

```js
function () {
  // do this
  // do that
  done()

  function done() {

  }
}
```

```js
function () {
  // do this
  // do that
  done()

  return 'something'

  function done() {

  }
}
```
