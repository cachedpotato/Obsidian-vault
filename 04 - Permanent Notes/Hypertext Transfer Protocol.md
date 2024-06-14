---
tags:
---
# Hypertext Transfer Protocol

## Basic structure of http request
```
Method Request-URI HTTP-Version CRLF
headers CRLF
message-body
```
the CRLF here stands for _carriage return and line feed_, which dates back to the typewriter days. Carriage return is the `\r` character we see from time to time, and line feed equates to newline `\n` nowadays. Add that together, and the request should have `\r\n` at the end.
## Response format
The response format is similar to the request format.
```
HTTP-Version Status-Code Reason-Phrase CRLF
headers CRLF
message-body
```
a blank response format with no header and body would look something like this:
```
HTTP/1.1 200 OK\r\n\r\n
```
the message-body will often be an HTML page.
## Status Line
This is a basic structure of the status line:
```
GET / HTTP/1.1
```
GET is the request command
the `/` after `GET` is the "directory" of the website. If we think of a website consisting of many pages as a filesystem, then the meaning of `/` becomes clear - it's the _root_ of the website, in other words, the _homepage_. Say we have a link of IP `127.0.0.1:7878`, and this link has a page `foo`. If we're trying to access `127.0.0.1:7878/foo`, then the status line would look like this:
```
GET /foo HTTP/1.1
```
## Status Code
Here are some of the more common status codes we see:

| Status code | Meaning               |
| ----------- | --------------------- |
| 200         | OK                    |
| 301         | Moved Permanently     |
| 302         | Found                 |
| 304         | Not Modified          |
| 307         | Temporary Redirect    |
| 401         | Unauthorized          |
| 403         | Forbidden             |
| 404         | Not Found             |
| 500         | Internal Server Error |
| 503         | Service Unavailable   |
Code 300~: Redirects
Code 400~: User is the problem
Code 500~: Server is the problem

## User input with HTTP/HTML
We can actually get user inputs in HTTP, and in URLs it is shown as key-value pairs with a question mark, like so:
```
https://www.google.com/search?q=cats
```
Here, `q` is the key and `cats` is the value (user input). `search` here is the path. To generalize, getting user inputs looks like this:
```
https://huh.website.domain/path?key=value&key=value..
```
as we can see we can get multiple inputs with `&`.


---
Categories: [[Computer Network]]
References:
Created: 2024-05-29