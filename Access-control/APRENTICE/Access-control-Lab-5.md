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
User can get access to another users account and steal their passwords or credentia
