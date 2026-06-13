# Access Control Lab 2 - Unprotected admin functionality with unpredictable URL

## What was vulnerable
Admin panel hidden under unpredictable URL —
security through obscurity only.

## What I did
1. Opened page source / DevTools
2. Searched for "admin" in the code
3. Found JavaScript that revealed the hidden path:
   href="/admin-zduyjl"
4. Navigated directly to that URL
5. Deleted user Carlos

## Why it worked
The URL was random but visible in page source.
Anyone who checks the JavaScript can find it.
No authentication required to access the panel.

## Key lesson
Security through obscurity is not security.
If the path is in the JavaScript — it's public.
Always search page source for "admin", "panel", 
"secret", "hidden", "dashboard".

## How to detect in real pentest
1. View page source — Ctrl+U
2. Search for keywords: admin, panel, secret, config
3. Check JavaScript files for hardcoded paths

## Remediation
- Enforce authentication on admin endpoints
- Never put sensitive paths in client-side JavaScript
