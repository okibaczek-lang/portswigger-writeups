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
