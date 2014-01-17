## Messages and Errors

Errors and messages should be the same. Errors should mimic Javascript's errors, specifically:

- `message`
- `name`

## POST responses

### 303 HTML responses

### 200 JSON responses w/ Location header

Just return the created resource and set the `Location` header.