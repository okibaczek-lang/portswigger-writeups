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
