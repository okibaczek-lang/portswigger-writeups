# Authentication Lab 3 - Password reset broken logic

## What was vulnerable
The application did not properly validate password reset tokens.

## Exploitation
1. First I tried changing usernames and testing for IDOR-like behavior, but it did not work.
2. Then I requested a password reset for my own account and observed that the reset link contained a token.
3. This made me investigate whether the token was actually being validated.
4. I intercepted the password reset request in Burp Suite and sent it to Repeater.
5. I changed the username from Wiener to Carlos, but the request failed.
6. After examining the request more closely, I noticed the reset token appeared both in the URL and in the request body.
7. I removed both token values and sent the request again.
8. The application accepted the password change and redirected me to the login page.
9. I logged in as Carlos using the new password.

## Why it worked
The application did not properly validate the password reset token. Removing the token should have caused the request to fail, but the server still processed the password change.

## How to detect in real pentest
Review password reset functionality and intercept reset requests. Test whether reset tokens are required by removing, modifying, or replacing them and observing the server response.

## Real world impact
An attacker could reset another user's password and gain unauthorized access to their account.
