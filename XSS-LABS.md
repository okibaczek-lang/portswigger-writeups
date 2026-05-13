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
Much more dangerous than Reflected XSS.

## Real world impact
Attacker stores malicious script once —
it steals cookies from every visitor automatically.
