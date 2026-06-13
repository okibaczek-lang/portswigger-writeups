# Access Control Lab 3 - User role controlled by request parameter

## What was vulnerable
Admin access controlled by cookie value admin=false.
Client-side cookie = attacker can modify it freely.

## What I did
1. Logged in as wiener:peter
2. Intercepted request in Burp Suite → Repeater
3. Found cookie: admin=false
4. Changed to: admin=true
5. Modified cookie in DevTools → Application → Cookies
6. Navigated to /admin panel
7. Deleted user Carlos

## Why it worked
Server trusted the cookie value sent by the client.
No server-side verification of admin privileges.
Anyone can modify their own cookies in the browser.

## How to detect in real pentest
Intercept requests in Burp Suite.
Look for cookies or parameters like:
admin=false, role=user, isAdmin=0, privileged=false
Try changing them to true/1/admin.

## Remediation
Never trust client-side values for authorization.
Store user roles server-side in the session.
Validate permissions on every request server-side.

## Real world impact
Any user can grant themselves admin access.
Full account takeover, data theft, user deletion.
