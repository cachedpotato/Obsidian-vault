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




---
Categories: [[Computer Network]]
References:
Created: 2024-05-29