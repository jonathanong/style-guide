
See also:

- https://github.com/petkaantonov/bluebird/wiki/Optimization-killers

### Avoid `.bind()`

If you need to use `.bind()`, then you're probably doing something wrong.

### Avoid creating closures within functions

However, this is the lesser of other evils, such as `.bind()`.

### Always `yield* generator`

Never `yield generator` or `yield generatorfunction`.
Always do `yield* generator` or `yield* generatorfunction()`.

Read morea bout the difference between [yield next vs. yield* next](http://jongleberry.com/delegating-yield.html).

### Avoid wrapping generator functions in generator functions

For example, if you have this:

```js
function* wrapper(arg) {
  return yield* fn(arg)
}

function* fn(arg) {
  return arg
}
```

Can be simplified to:

```js
function wrapper(arg) {
  return fn(arg)
}
```
