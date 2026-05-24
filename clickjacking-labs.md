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
Created HTML page with: (I used an template but changed most of the things)
- iframe pointing to victim's account page (opacity: 0.0001)
- div "Click me" positioned exactly over Delete Account button

Key CSS:
- iframe z-index: 2 (on top, invisible)
- div z-index: 1 (below iframe, visible to victim)
- opacity: 0 = iframe invisible but still clickable

## Steps
1. Set opacity: 0.5 to see both layers
2. Adjusted top/left values to align "Click me" 
   over "Delete Account" button
3. Set opacity: 0.0001 to make iframe invisible
4. Delivered to victim — they clicked "Click me" 
   and deleted their account

## How to detect in real pentest
Try embedding the target page in an iframe.
If it loads = potentially vulnerable to clickjacking.
Check for X-Frame-Options or CSP frame-ancestors headers.

---

# Clickjacking Lab 2 - Clickjacking with form input data prefilled from a URL parameter (Same as first lab but i had to trick the victim to change his email not deleting their account)

## What was vulnerable
Update email button — no clickjacking protection.
Page could be embedded in an iframe on another site.

## What I did
Created HTML page with: (I used an template but changed most of the things)
- iframe pointing to victim's account page (opacity: 0)
- div "Click me" positioned exactly over update email button
- an email automatically pasted into the field where you can change the email

Key CSS:
- iframe z-index: 2 (on top, invisible)
- div z-index: 1 (below iframe, visible to victim)
- opacity: 0.0001 = iframe invisible but still clickable

## Steps
1. Set opacity: 0.5 to see both layers
2. Adjusted top/left values to align "Click me" 
   over "update email" button
3. Set opacity: 0.0001 to make iframe invisible
4. Delivered to victim — they clicked "Click me" 
   and changed their email to the one in HTML code

---

# Clickjacking Lab 3 - Clickjacking with a frame buster script

## What was vulnerable
Email button - sandbox clickjacking protection which can be exploited

## What I did
Created HTML page with: (I used an template but changed most of the things)
- iframe pointing to victim's account page (opacity: 0)
- div "Click me" positioned exactly over update email button
- an email automatically pasted into the field where you can change the email
- a HTML line of code which let me go around the frame buster protection

Key CSS:
- iframe z-index: 2 (on top, invisible)
- div z-index: 1 (below iframe, visible to victim)
- opacity: 0 = iframe invisible but still clickable
- used this code <iframe sandbox="allow-forms" src=".....

## Steps
1. Set opacity: 0.5 to see both layers
2. Adjusted top/left values to align "Click me" 
   over "update email" button
3. Set opacity: 0.0001 to make iframe invisible
4. Delivered to victim — they clicked "Click me" 
   and changed their email to the one in HTML code





