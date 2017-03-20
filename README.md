_templatize
---

Utilities similar to WordPress' wp.template(). Provides option to load from a <prefix><id> script tag,
or to pass in arbitrary html.

Compiled templates are memoized and cached for reuse, based on the tmplName.

### Example usage:

HTML:

```html
<script type="text/html" id="tmpl-your-js-template">
<h1>{{ data.title }}</h1>
<h2>{{ data.description }}</h2>
</script>
```

Javascript:

```js
var template = window._templatize(); // Instantiate the template object to a var.
var tmplData = { title: 'Hello World', description: 'A fancy description' };
var html = template( 'your-js-template', tmplData );

/**
 * html is now:
 * <h1>Hello World</h1>
 *	<h2>A fancy description</h2>
 */
```

### Usage by passing html strings:

```js
var template = window._templatize(); // Instantiate the template object to a var.
var tmplData = { title: 'Hello Github', description: 'A fancy description' };
var html = template( 'hello-world', tmplData, '<h2>{{ data.title }}</h2><h3>{{ data.description }}</h3>' );

/**
 * html is now:
 * <h2>Hello Github</h2>
 *	<h3>A fancy description</h3>
 */
 
// The 'hello-world' template is now cached, so we can simply reference by ID,
// rather than passing the HTML in again.
var html2 = template( 'hello-world', { hello: 'Hello Universe' } );

/**
 * html2 is now:
 * <h2>Hello Universe</h2>
 *	<h3>A fancy description</h3>
 */

```
