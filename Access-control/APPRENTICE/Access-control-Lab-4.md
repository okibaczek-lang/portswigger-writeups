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
