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
