---
tags:
---
# DOM Content Loading
Consider this HTML file:
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>Hello</title>
        <script>
            let counter = 0;
            function hello() {
                alert('Hello, world!');
            }
            function count() {
                counter += 1;
                document.querySelector('p').innerHTML = 'Current count: ' + counter;
                if (counter % 10 === 0) {
                    alert(`Count is now ${counter}`);
                }
            }
            document.querySelector('button').onclick = count;
        </script>
    </head>
    <body>
        <h1>Hello!</h1>
        <button>Count</button>
        <p>Current count: 0</p>
    </body>
</html>
```
What we're trying to do here is to update our `<p>` value inside the HTML file whenever we press the `button`. however, if we actually load this, nothing happens when we press the button. This is because `button` is not defined until further down the HTML file, but inside the `<script>` tag we're already looking for it. HTML loads from top to bottom, so this is why the error occurs.

In other words, the DOM content is not fully loaded yet when we reach that line of code. Luckily, we can add something called `addEventListener` to our code to wait until all DOM content has been loaded.
```JS
document.addEventListener('DOMContentLoaded', function() {
	document.querySelector('button').onclick = count;
});
```
the `addEventListener` method takes in two arguments:
- the Event
- the Listener, or the function that will be executed once the event happens.
Here, we passed an anonymous function that will call another function `count` that updates our counter.

Note that we did not add parentheses to `count`, because we're not trying to get the return value. We're literally assigning a function to the `onclick` event.

---
Categories: [[CS50 - Web Dev]], [[Document Object Model]], [[JavaScript]]
References:
