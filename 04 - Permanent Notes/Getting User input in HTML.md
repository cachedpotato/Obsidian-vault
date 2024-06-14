---
tags:
---
# Getting User input in HTML
As stated in the [[Hypertext Transfer Protocol]], we can get user inputs with `path?key=value`. But how exactly do we implement this in our HTML file? We need two tags: `<form>` and `<input>`

## `form` tag
Form tag has a lot, and I mean, LOT of use cases, but for now we will focus on getting inputs. `form` has an attribute `action`, where we define what action we want this webpage to do when we submit this form. How we do things is defined under the `method` attribute, like so:
```HTML
<form action = "https://google.com/search" method = "get">
	<input> --....
</form>
```
Here, we can see that the `get` method is used to get user input, and once we submit this form, it will connect to the search engine of google, as described under the `acion` attribute.

## `input` tag
the `<input>` tag is the `key` part is `path?key=value&key=value...`. Whatever input we get, we will store that under this key. google's search engine URL looks something like this:
```
https://www.google.com/search?q=cats
```
so, continuing the HTML file above, to access this exact URL, we can do the following:
```HTML
<form action = "https://www.google.com/search" method = "get">
	<input name="q" placeholder="Query" type = "search">
	<button>Search</button>
</form>
```
This creates an HTML webpage with a small input box with a button with the text "Button" in it that once clicked, will connect to the google URL above.

### `input` attributes
- `name`: the key of the key-value pair
- `placeholder`: placeholder text that appears before user input
- `type`: depending on the type, we can have some cool features added on top of just being a plain text. 
- `autofocus`: Will automatically go into the search bar, removing the need for users to manually click the search bar then input text.
- `pattern`: [[Regex]] pattern for getting only wanted user input. for example, to get only emails that ends with `.edu`:
```html
--snip 
<input autocomplete = "off" placeholder="Email" pattern = ".+@.+\.edu$">
```

---
Categories: [[Hypertext Markup Language]], [[Hypertext Transfer Protocol]], [[CS50 - Introduction]]
References:
Created: 2024-06-14
