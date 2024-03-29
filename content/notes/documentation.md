---
title: "documentation"
tags: 
- cosc202
- seng
---

## 1 Who, what where
- Audience
	- users
	- other devs
	- your team members
	- anyone trying to understand you software
	- your future self
- Locations
	- source code
	- project repo
	- emebedding in program
	- hosted separately
- User expectations
	- evolving towards software that _facilitates experimentation_
		- No help docs => everything is self-explanatory
	- high usability
	- users familar with many abstractions
		- e.g., touchscreens, menus, links
- API's
	- for devs writing code to interact with your code
	- typically coupled with docs
	- entirely technical audience --> tool generated docs are okay
	- not self explanatory
	- used by devs unfamiliar with code base
- Project Docs
	- meaningful commit msgs
	- extra mangement with e.g., github
		- issue tracking
		- ensures relevant material is cross linked where possible
		- can easily refer to source code
- Source code docs
	- header comments
		- software licencing
		- support devs
		- indicate code ownership
	- in code comments on fields methods etc
		- keep in sync with code changes
	- descriptive variable/class/other names
	
## 2 Built in language support
- basic
	- syntax for code comments
	- indicate that the compiler should ingnore
	- also more advanced like python "doc strings"
- Structured comments and docs
	- machine parseable comments
		- e.g., javadocs, perl plain old docs
		- creates a doc website
		- uses annotations e.g., @author, @returns, @param
- Literate programming
	- donald knuth suggestions (1984)
		- source code should be primarily natural language documentation
		- executable code snippetrs are included within the description
		- tools are used to:
			- tangle the code snippets
			- weave out the documentation
	- Modern implementations
		- jupyter notebooks
		- swift playgrounds
		- r markdown
