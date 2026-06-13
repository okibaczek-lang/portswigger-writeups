# XSS Lab 8 - Stored XSS into anchor href attribute

## What was vulnerable
Comment section — website URL field.
Whatever was typed there landed inside 
an href attribute of the author name link.

## What I did
Instead of a real URL, injected:
`javascript:alert(1)`

Clicked the comment author name — alert fired.

## Why it worked
href accepts javascript: protocol.
Page stored the comment in database = Stored XSS.
Every visitor who clicks the author name triggers the alert.

## Key lesson
Always fill in every field in a form and check 
page source — some fields land in href attributes.
href + javascript: = instant XSS without breaking 
out of any tags.

## Real world impact
Stored in database = affects every visitor.
Replace alert(1) with cookie stealer = 
every user who clicks loses their session.
