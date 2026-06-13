# XSS Lab 9 - Reflected XSS into JavaScript string

## What was vulnerable
Search field — input landed inside a JavaScript string:
var searchTerms = 'USER INPUT HERE';

## What I did
Checked page source after searching random text.
Saw input lands inside single quotes in JS.
Injected:
`'+alert()+'`

## Why it worked
First ' closed the existing string.
+ joined the next element.
alert() executed as code.
+' opened new string to prevent syntax errors.

## Key lesson
In HTML = escape with "
In JS string = escape with '
Always use +' at the end to avoid breaking the code.

## Real world impact
Attacker crafts malicious URL.
Victim opens link, alert fires.
Replace alert() with cookie stealer = session hijack.
