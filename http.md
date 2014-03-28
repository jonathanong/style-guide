
## Request Bodies

Try to avoid using request bodies and body parsers. 
Instead, add the relevant information to the URL and use `PUT` and `DELETE` methods.
You should also prefer setting the CSRF token via header.

## Messages and Errors

Errors and messages should be the same. Errors should mimic Javascript's errors, specifically:

- `message`
- `name`

With optional additional properties:

- `type`
- `code`
- `key`

## Content Negotiation

GET requests should __not__ use content negotiation. 
Assume `html`, and specify different formats using a `.:format` parameter.
This is because most CDNs only respect `Vary: Accept-Encoding`.

## Redirects

JSON APIs should __never__ use redirects.
