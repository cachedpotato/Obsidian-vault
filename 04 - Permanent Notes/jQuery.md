---
tags:
---
# jQuery
If we look at the DOM methods, we can see that the function names are pretty long. In practice, it's even more egregious. Take for an example, a function that changes the background color of a page with the click of a button:
```JS
function changeColorEvent(event) {
	var triggerObject = event.srcElement;
	document.getElementById('colorDiv').style.backgroundColor = \\
		triggerObject.innerHTML.tolowercase();
}
```
All this code just to change colors? This seems too much work. Thankfully, there exists a public API, called jQuery, that simplifies the syntax, at the cost of slightly less interpretability:
```JS
$(document).ready(function() {
	$('.jQButton').click(function() {
		$('#colorDiv').css('background-color',
		 this.innnerHTML.toLowerCase());
	});
});
```

Here's the official API link:
- https://api.jquery.com

---
Categories: [[Document Object Model]], [[JavaScript]], [[CS50 - Introduction]]
References:
Created: 2024-06-14
