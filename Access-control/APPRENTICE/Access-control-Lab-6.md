# Access Control lab 6 - User ID controlled by request parameter, with unpredictable user IDs

## What was vulnerable
User ID stored inside URL in users blogs. 

## What i did
1. ID was unpredictable so i had to find Carlos ID by researching the website
2. I scrolled blogs to find user named Carlos 
3. When i found blog made by this user i clicked on his name
4. After that i saw that the URL contained an users ID
5. I copied it and pasted it into URL on ,,my account" page ID=
6. I succesfully logged in as Carlos and got his API key to solve the lab

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
