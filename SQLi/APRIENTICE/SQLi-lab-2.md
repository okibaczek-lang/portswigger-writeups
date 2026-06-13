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
