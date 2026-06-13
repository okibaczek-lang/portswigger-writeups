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
