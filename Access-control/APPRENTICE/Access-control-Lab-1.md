# Access Control Lab 1 - Unprotected admin functionality

## What was vulnerable
Admin panel had no access control —
anyone could access it if they knew the URL.

## What I did
1. Checked /robots.txt — found hidden path:
   Disallow: /administrator-panel
2. Navigated to /administrator-panel directly
3. Deleted user Carlos — no authentication required

## Why it worked
robots.txt is public — meant to hide pages from Google
but reveals hidden paths to attackers.
Admin panel had no login check — anyone with the URL
could access full admin functionality.

## How to detect in real pentest
Always check /robots.txt during recon.
Try accessing admin paths directly without logging in.
Common paths: /admin /administrator /admin-panel /backend

## Real world impact
Attacker can delete users, change passwords,
access all user data — full account takeover.

## Remediation
- Never rely on obscurity for security
- Enforce authentication on every admin endpoint
- Remove sensitive paths from robots.txt
