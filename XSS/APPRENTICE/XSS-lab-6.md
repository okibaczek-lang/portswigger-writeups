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
