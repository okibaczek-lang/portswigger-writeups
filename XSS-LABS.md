# XSS Labs

## What is XSS
Injecting JavaScript code into a page that executes 
in other users' browsers. Instead of attacking 
the database like SQLi — you attack the browser.

---

# Lab 1 - Reflected XSS

## Goal
Execute JavaScript alert via search field.

## What I did
Injected payload into search field:
<script>alert(1)</script>

## Why it worked
Page took my input and placed it directly into HTML
without filtering. Browser executed it as code.

## Key difference - Reflected XSS
Works only when victim clicks a malicious link.
Not stored anywhere — executes once.

---

# Lab 2 - Stored XSS

## Goal
Execute JavaScript alert via comment section.

## What I did
Injected same payload into comment field:
<script>alert(1)</script>

## Why it worked
Comment was saved to database and loaded 
every time someone opens the page.

## Key difference - Stored XSS
Payload is stored in database permanently.
Every user who visits the page gets attacked.

# XSS Lab 3 - Breaking out of attribute context

## Why simple <script> didn't work
My input landed inside img src attribute.
Browser treated it as image path, not code.

## Solution
Used "> to break out of the attribute first,
then injected the script after it.

## Key lesson
Always check where your input lands in HTML.
Inside attribute = break out first with ">
Direct in page = simple <script> works

---

# XSS Lab 6 - Reflected XSS into attribute with angle brackets HTML-encoded

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

## Real world impact
Attacker crafts malicious URL with payload.
Victim opens link, hovers over search field,
script executes and steals session cookies.
