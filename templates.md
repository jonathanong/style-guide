## General

* Use [SUIT naming conventions](https://github.com/suitcss/suit/blob/master/doc/naming-conventions.md) to structure your HTML and CSS.
* Use `id`s.
* Use HTML5 elements like `<section>` and `<main>`.
* Avoid deeply nested selectors - use `id`s, unique tags, or more tags.

## Javascript

* Don't use any type of "on DOM ready" logic.
  It messes with the back button.

## CSS

* Don't use vendor prefixes - depend on autoprefixer.
* For inlined-CSS, use the `scoped` attribute on `<style>`.
* Avoid defining margins - use padding instead.

## HTML

* Assume HTML5 specs
* Don't self-close self-closing tags (as per HTML5 spec)
  * Yes: `<input>`
  * No: `<input />`

### Attributes

* Always wrap attributes around `"`s
* (Boolean) properties should not have `=""`
  * Yes: `<input checked>` or `<input>`
  * No: `<input checked="checked">` or `<input checked="true">`

### Required Attributes

* `a`
  * `href` - If for UI, set `href="#"`, and make this button hidden when `html.no-js`.
    Also, make sure to `event.preventDefault()`.
  * `title=""`
  * `tabindex="-1"` - For any links within the form.
    The exception is when the link is a functional part of the form,
    though that doesn't make any sense.
* `img`
  * `alt=""`
* `input` and `textarea`
  * `maxlength` - if no other validation is used
  * `title` and `placeholder` - these can be the same values
* `input`
  * `type` - even if just `text`
* `textarea`
  * `rows`

### Blacklisted Attributes

* `script`
  * `type` - it should always be Javascript, anyway
