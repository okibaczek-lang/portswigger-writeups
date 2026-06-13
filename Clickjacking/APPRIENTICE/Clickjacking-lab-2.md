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
