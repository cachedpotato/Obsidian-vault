---
tags:
---
# Bootstrap in Web Development
Bootstrap is a community driven CSS file that lets us style html however we want. to use bootstrap, we just add this line to HTML:
```HTML
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
```

To use bootstrap, copy the code above to the HTML file, then using the document, add whatever we want. For example, the document provides this nice red alert box:
```HTML
<div class="alert alert-primary" role="alert">
  A simple primary alert—check it out!
</div>
```
Just paste this into my HTML and voila I have an alert box.

## Notable properties
Bootstrap divides rows into 12 columns. Using this, we can create columns of various sizes, as long as the size of the columns sum up to 12. To access this, use the `class="col-size"` attribute:
```HTML
<div class="row">
	<div class="col-3">column 1</div>
	<div class="col-3">column 2</div>
	<div class="col-3">column 3</div>
	<div class="col-3">column 4</div>
</div>
```

Bootstrap also lets us modify how much screen a column should take up depending on the size of the screen:
```html
<div class="col-lg-3 col-sm-6">column1</div>
```
This tells the webpage that if the screen is large, we take roughly a quarter (3/12) and if the screen is small, take half (6/12).





---
Categories: [[030-Web Development]], [[CS50 - Web Dev]]
References:
