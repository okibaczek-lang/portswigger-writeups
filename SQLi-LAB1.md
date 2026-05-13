# SQL Injection - Lab 1

## Goal
Make the application show unreleased products.

## How it works
When user selects a category, the app sends this query:
SELECT * FROM products WHERE category = 'Gifts' AND released = 1

## What I did
Intercepted the request in Burp Suite, sent to Repeater,
changed category to:
lifestyle' OR 1=1--

## Why it worked
OR 1=1 is always true so database returns all products.
-- comments out the rest of the query so released=1 
is ignored.

## Real world impact
Attacker can see hidden products, unpublished content,
or data that shouldn't be visible.

---

# SQL Injection - Lab 2

## Goal
Log in as administrator without knowing the password.

## How it works
Login sends this query:
SELECT * FROM users WHERE username='wiener' AND password='bluecheese'

## What I did
Intercepted login request in Burp Suite, sent to Repeater,
changed username to:
administrator'--

## Why it worked
-- comments out AND password check entirely.
Database finds user 'administrator' and skips password verification.

## Real world impact
Attacker can log in as any user including admin
without knowing their password.
