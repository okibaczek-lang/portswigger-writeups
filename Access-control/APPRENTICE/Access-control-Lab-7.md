# Access control Lab 7 - User ID controlled by request parameter with data leakage in redirect

## What was vulnerable 
Body of redirect response - sensitive data leakage

## What i did
1. I changed the ID in the URL to Carlos to see if it directs me into his account
2. After this didnt work and i had to log in after changing it i checked burp HTTP history 
3. I send my account page to burps repeater and in requeset i changed ID from wiener to carlos
4. After this i checked the response and i saw body of response 
5. I searched for word API and found API key of user Carlos which i used to solve the lab

## Why it worked
The server retrieved Carlos's data before performing the authorization check and redirect.
Although the browser followed the redirect, the sensitive data was still present in the response body.

## How to detect in real pentest
Don't trust redirects alone.
Always inspect the full response body of 302/303 responses after modifying user IDs.
Look for leaked data such as API keys, tokens, emails, or personal information.

## Real world impact
Attackers could obtain sensitive information from other users without directly accessing their accounts.
