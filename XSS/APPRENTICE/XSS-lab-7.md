# XSS Lab 7 - Reflected XSS into attribute with angle brackets HTML-encoded

## What was vulnerable
Search field — user input was placed inside 
a value attribute of an input tag:
<input value="USER INPUT HERE">
Angle brackets < > were blocked but quotes were not.

## What I did
Broke out of the value attribute using a quote,
then injected a new event handler:
" onmouseover="alert(1)

Result in page source:
<input value="" onmouseover="alert(1)">

## Why it worked
Closing quote escaped the value attribute.
onmouseover fires when victim hovers over the element —
no click required, higher chance of execution.

## Why onmouseover over onclick
onclick requires deliberate action from victim.
onmouseover fires passively — victim just moves 
the mouse near the search field.
In real attacks, passive triggers are more reliable.

## Key lesson
When < > are blocked, look for attribute injection.
You don't need new HTML tags — inject events 
into existing ones.
Always think: will this work on the VICTIM'S browser,
not just mine.
