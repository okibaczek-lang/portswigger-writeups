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
