# XSS Lab 5 - DOM XSS in jQuery anchor href attribute sink

## What was vulnerable
Submit feedback page — "Back" link used returnPath
parameter from URL and placed it into href attribute
without sanitization.

## What I did
Changed returnPath in URL to:
```
javascript:alert(document.cookie)
```
Clicked "Back" link — alert fired with cookies.

## Why it worked
href attribute accepts javascript: protocol.
jQuery took value from URL and put it directly
into href without checking it.

## Key lesson
Always check URL parameters that end up in href.
Look for: returnPath, redirect, next, url parameters.
Impact: cookie theft = account takeover.
