See also:

- [Felix's Node.js Style Guide](http://nodeguide.com/style.html)
- [Aaron's JS Style Guide](https://github.com/aheckmann/js-styleguide)

Generally, you should follow their styles unless overridden by these.

## Philosophy

* Prefer the latest ECMAScript syntax available on the target platform(s)
* Prefer JSON styling when defining objects
* Filenames should mimic code structure
* Try to keep lines less than 60 characters wide
* Try to keep functions less than 50 lines long
* No trailing whitespace
* Prefer `'` over `"` - avoid escaping quotations

## Code Order

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

## Syntax

### Two space indentation

Never use tabs. This is so you can actually read code online.

### One var/const per line

Way easier than using commas. You can also type `var ` with your left hand while you do other things with your right. Better diffs, too.

```js
var one = 1
var two = 2
```

### Surround function arguments with a space

This is so the arguments are highlighted in Sublime Text 2. Yes, this is a stupid reason.

```js
function (a, b) {}
function fn(a, b) {}
```

### Surround operators with a space

```js
if () {} else {}
switch () {}
```

No:

```js
if(){}else{}
```

### No unnecessary spaces

This also includes stuff like:

```js
fn( a , b )
```

Now it just looks like boobs with retarded nipples.

### Semicolons are optional

Only rule is that you should not let JSHint warn, "unnecessary semicolon".
In other words, no semicolons after function statements/declarations.
Do not bitch about semicolons or the lack thereof. There are better, more important fights to fight.

### Avoid the required use of semicolons

Avoid the previous rule whenever possible.
Always predefine variables, then use the variables.

Yes:

```js
something()
function something() {}
```

No:

```js
;(function(){})()
```

### Prepend statements starting with a `[` or `(` with a semicolon

You should avoid this in general, anyways.

```js
;[].forEach()
;(function () {})()
```

### Define adjustable arrays in multiple lines

If an array's attributes are likely to change,
define each element on a separate line:

```js
var thingsILike = [
  'coffee',
  'cigarettes',
  'cocaine',
]
```

### Always add a trailing comma to adjustable arrays and objects

```js
var things = [
  'coffee',
  'cigarettes',
  'cocaine',
]

var stuff = {
  coffee: true,
  cigarettes: true,
  cocaine: true,
}
```

If they are not adjustable, then it doesn't matter.
The reason is that it allows you to add/remove elements without messing up the diff.

## Functions

### Avoid closures

Since everything is written using CommonJS, closures are pretty much unnecessary.
Put the code in a separate file instead.

### Avoid function expressions

Avoid the following:

```js
var fn = function () {}
```

Exceptions:

- Exporting - `export.fn = function () {}`
- Conditionals - `var fn = a ? function () {} : function () {}`
- Within a block - `if (true) {let fn = function () {}; this.on('end', fn);}`

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

### Do not define functions within an array

Don't do this:

```js
var fns = [function () {

}, function () {

}]
```

Instead, use function declarations:

```js
parallel([fn1, fn2, fn3], callback)

function fn1() {}
function fn2() {}
function fn3() {}
```

Of course, use actually helpful function names. The same rule could apply to objects, but generally they aren't as difficult to read within objects.

### Always `yield* generator`

Never `yield generator` or `yield generatorfunction`.
Always do `yield* generator` or `yield* generatorfunction()`.

Read morea bout the difference between [yield next vs. yield* next](http://jongleberry.com/delegating-yield.html).

### Put each `yield` in its own separate line

Don't do anything like:

```js
function* () {
  var obj = {
    a: yield 'b'
  }
}
```

Instead, do:

```js
function* () {
  var a = yield 'b'
  var obj = {
    a: b
  }
}
```
