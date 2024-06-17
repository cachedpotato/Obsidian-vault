---
tags:
---
# GitHub Actions
When we push changes to our branch, it's best to test things out and see if everything is working correctly. While this can be done manually, thankfully GitHub provides automation to this process with Actions.

To create a GitHub Action, we need a [[YAML]] file:
```yaml
name: Testing
on: push

jobs:
	test_project:
		runs-on: ubuntu-latest
		steps:
			- uses: actions/checkout@v2
			- name: Run Django unit tests
			- run: |
				pip install --user django
				python manage.py test
	
```
Here we created a new job `test_project` in which we run our `python manage.py test` in a `ubuntu-latest` VM. This action will be done when we `push` to the branch.

We can see the results in the "Actions" tab in GitHub. If failed, we'll get a big "X" mark on our commit history.


---
Categories: [[GitHub]], [[CS50 - Web Dev]],
References:

