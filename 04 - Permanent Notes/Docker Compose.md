---
tags:
---
# Docker Compose
Docker containers are meant to do only a handful of things. However, there may be instances where we just need to test out a lot of stuff, or even use things outside of what we have. For example, we may want to test out our web application on PostGresQL, but we may not have direct access to the database. What we can do, then, is _compose_ our web application container with PostGres container. This is done through a [[YAML]] file called docker-compose.

```yaml
version: '3'
services:
	db:
		image: postgres

	web:
		build: .
		volumes:
			- .:/usr/src/app
		ports:
			- "8000:8000"
```
Here we compose two containers: `db` and `web`. the `db` uses the PostGres image, and the `web` uses our own Docker File, inside our current directory.

To actually use this file, we do `docker-compose up`. 


---
Categories: [[Docker]], [[030-Web Development]], [[CS50 - Web Dev]]
References:
