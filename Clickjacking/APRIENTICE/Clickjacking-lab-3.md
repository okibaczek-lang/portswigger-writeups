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
