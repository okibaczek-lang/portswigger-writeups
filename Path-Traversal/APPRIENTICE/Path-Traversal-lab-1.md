## Path Traversal LAB 1 - File path traversal, simple case

## What was vulnerable:

images of displayed products - the images are stored on /var/www/images/. Apllication reads the files there.

## What i did:

1. I ,,manipulated" the path by using a bunch off ../ for example .//.//.//.// 

../ = go one directory up

2. I added ../../../etc/passwd into URL after ...loadImage?filename=(payload here) and succesfully managed to get into files in root.

## How to detect in real pentest

If the application accepts a filename and there is no whitelist, and changing the path affects the response → Path Traversal is possible.

## Real world impact

attacker can view files inside an apllication, for example passwords of users.
