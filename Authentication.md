# Authentication Lab 1 - brute force attack

## What was vulnerable
login page had no brute force defense, which means you could insert bunch of credentials without getting a warning.

## Exploitation
1. First of all i checked if an apllication has brute force security by inserting random keys into username and password table. No warning after 10 failed attempts=we can perform brute force.
2. I inserted random name and password into login page and captured traffic in burp suit. Then sent it to intruder.
3. in intruder i marked username and inserted a payload which contained a list of typical usernames provided by portswigger .
4. after that i searched for world invalid. When i found a username which existed i marked the password and added another payload to it.
5. after i found the password i logged into given credentials and solved the lab

## Why it worked 
Server didn't attempt stoping the payload which inserted tons of invalid usernames, by blocking further actions

## How to detect in real pentest
Look for tables where you can insert credentials and look for a blockage by apllication.
No blockage after many failed attempts=brute force

## Real world impact
brute force can lead to data theft, financial fraud, and system compromise.

---

# Authentication Lab 2 - 2FA simple bypass

## What was vulnerable
The application did not properly enforce 2FA, allowing access to authenticated pages without completing verification.

## Exploitation
1. Logged into the provided account.
2. The application requested a 4-digit 2FA code.
3. I clicked **Home** instead of entering the code.
4. I accessed **My Account** and gained access without completing 2FA.

## Why it worked
The server did not verify whether the 2FA step was completed before granting access to protected pages.

## How to detect in a real pentest
* Attempt to access authenticated pages after partial login (before completing 2FA).
* Try navigating directly to endpoints like `/my-account`.
* Check whether session state changes after the 2FA step is completed.
* Observe if the server enforces 2FA on all protected resources.

## Real world impact
An attacker with valid credentials could bypass 2FA and access user accounts.

---

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
