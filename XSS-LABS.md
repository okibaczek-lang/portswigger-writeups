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

# XSS Lab 4 - XSS into HTML context, blocking common tags

## What was vulnerable
Search field — but common tags were blocked.

## What I did
Tested different tags until img worked:
```
<img src=x onerror=alert(1)>
```

## Why it worked
`<img>` tag was not blocked.
`src=x` points to non-existent image.
Browser triggers onerror event = alert fires.

## Key lesson
When `<script>` is blocked, try other tags.
Always test what is and isn't filtered.

---

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

---

# XSS Lab 6 - DOM XSS via location.hash

## What was vulnerable
Page used location.hash to scroll to a blog post.
If post didn't exist, page created a new element.

## What I did
Injected payload into URL hash:
```
#<img src=x onerror=print()>
```

## Why it worked
Hash value never goes to server — only browser reads it.
Page took hash value and inserted into DOM without
sanitization. Missing image triggered onerror = print().

## Key lesson
location.hash is client-side only.
Page must load first, then JavaScript reads the hash.
Look for pages that scroll or load content based on hash.

---

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

---

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

---

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
