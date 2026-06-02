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

---

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

---

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

---

# Access Control Lab 4 - User role can be modified in user profile

## What was vulnerable
User role stored in JSON response as roleid:1
Role could be modified by sending roleid:2 in request.

## What I did
1. Browsed site and checked HTTP history in Burp Suite
2. Sent requests of directories to Repeater to check for roleid 
3. Found email change request contained roleid:1 in response
4. Added "roleid":2 to the request body
5. Got admin access — navigated to /admin
6. Deleted user Carlos

## Why it worked
Server accepted role change from client request.
No server-side validation of who can change roles.
User could promote themselves to admin.

## How to detect in real pentest
Check all responses for role/privilege parameters:
roleid, role, userType, accessLevel, privilege
Try sending those parameters back in requests
with elevated values.

## Remediation
Never accept role changes from client requests.
Store and manage roles server-side only.
Validate permissions on every sensitive action.

## Real world impact
Any user can promote themselves to admin.
Full access to admin panel, all user data.

---

# Access Control Lab 5 - User ID controlled by request parameter

## What was vulnerable
User ID stored in websites URL
ID could be modified by changing it to another user account name

## What i did
1. Browsed site and checked the URL
2. I saw that the URL parameter had ID=wiener
3. I changed the parameter to ID=carlos
4. Copied the API key and submited it to solve the lab

## Why it worked
Server accepted changing ID without verifying 
if the requesting user owns that account.
Classic IDOR vulnerability.

## How to detect in real pentest
Look for user identifiers in URL:
id=, user=, account=, profile=
Change to another username or number.
If you see another user's data = IDOR confirmed.

## Real world impact
User can get access to another users account and steal their passwords or credentials

---

# Access Control lab 6 - User ID controlled by request parameter, with unpredictable user IDs

## What was vulnerable
User ID stored inside URL in users blogs. 

## What i did
1.ID was unpredictable so i had to find Carlos ID by researching the website
2.I scrolled blogs to find user named Carlos 
3.When i found blog made by this user i clicked on his name
4.After that i saw that the URL contained an users ID
5.I copied it and pasted it into URL on ,,my account" page ID=
6.I succesfully logged in as Carlos and got his API key to solve the lab

## Why it worked
Server accepted changing ID without verification
Another classic IDOR

## How to detect in real pentest
Even unpredictable GUIDs can be found elsewhere on the site.
Check: blog posts, comments, user profiles, public pages.
Authors often expose their ID in public content.
Copy ID from public page → use in authenticated endpoint.

## Real world impact 
User can get another users data 
