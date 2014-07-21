
### Don't throw non-errors

Strings are not errors! If `!(err instanceof Error)`, then it's not an error!

### Avoid using event emitters

They are terrible, and the fact that `error` events throw and destroy your process
when there are no listeners is one of the main problems with node.

### Avoid using callbacks

Use promises or generators. Both handle errors correctly, allowing developers
to avoid the pain of uncaught exceptions and no stack traces.

### Don't use domains or any other similar error tool

Domains will be deprecated from node. Any other error handling tool is essentially
unnecessary when you use promises and/or generators.
