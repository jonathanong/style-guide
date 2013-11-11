## Javascript

* If a javascript only occurs on a single page and does not require any external libraries or functions,
  include it inline.
* Don't use any type of "on DOM ready" logic.
  It messes up with the back button.

## CSS

* Don't use vendor prefixes - depend on autoprefixer.
* For inlined-CSS, use the `scoped` attribute on `<style>`.
  Inline the CSS whenever the CSS only pertains to a certain page.
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
  * `type` - It should always be Javascript, anyway