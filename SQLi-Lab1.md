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
