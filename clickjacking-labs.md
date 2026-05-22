# Clickjacking Lab 1 - Basic clickjacking with CSRF attack

## What was vulnerable
Delete account button — no clickjacking protection.
Page could be embedded in an iframe on another site.

## How clickjacking works
Attacker overlays invisible iframe (real page) 
over a fake button (decoy).
Victim clicks decoy button = actually clicks 
the real button inside hidden iframe.

## What I did
Created HTML page with:
- iframe pointing to victim's account page (opacity: 0)
- div "Click me" positioned exactly over Delete Account button

Key CSS:
- iframe z-index: 2 (on top, invisible)
- div z-index: 1 (below iframe, visible to victim)
- opacity: 0 = iframe invisible but still clickable

## Steps
1. Set opacity: 0.5 to see both layers
2. Adjusted top/left values to align "Click me" 
   over "Delete Account" button
3. Set opacity: 0 to make iframe invisible
4. Delivered to victim — they clicked "Click me" 
   and deleted their account

## How to detect in real pentest
Try embedding the target page in an iframe.
If it loads = potentially vulnerable to clickjacking.
Check for X-Frame-Options or CSP frame-ancestors headers.

## Real world impact
Force victim to: delete account, make payment,
change email, approve transaction — one click.
