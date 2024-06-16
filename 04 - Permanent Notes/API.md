---
tags:
---
# API
Application Programming Interfaces, A.K.A APIs, is a way of web services to exchange data and communicate with each other. Communication requires well structured request-reply relationship, and by structure we mean that the data we send must be well-structured. Very often, this structure comes in the form of a JavaScript Object Notation, or JSON.
```json
{
	"origin": {
		"city": "New York",
		"polulation": 12312983,
	},
	
	"currency": "Dollar",
	
	"destination": {
		"city": "Seoul"
	}
}
```
As long as both sender and receiver agrees upon and knows this exact structure, they can freely communicate with each other and even manipulate values for their own purposes. Using APIs, we can make our site display things that we don't have a "direct" access to (as in we do not generate/own said data).
![[Pasted image 20240615161047.png | 500]]
Because we're getting data from different servers, this is called AJS, or [[Asynchronous JavaScript]]


---
Categories: [[CS50 - Web Dev]], [[030-Web Development]], [[JavaScript]]
References:
