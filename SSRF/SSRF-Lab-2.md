# SSRF LAB - Basic SSRF against another back-end system

## What was vulnerable 
Check stock option, User could change the StockApi to URL of the systems website

## Attack surface
IP range for admin interface and port

## Exploit
1. I captured the check stock function in burps proxy 
2. I sent this to repeater and changed the StockApi to http://192.168.0.1:8080/admin
3. I sent this to intruder and highlighted the final octet of IP adress (1) so i can add payload there
4. In the payload type i clicked on numbers and inserted from:1 to:255 (max number of last octet in IPv4)
5. After this i started the attack and found status code 200
6. I observed the response and found that the delete user carlos function is avaible in http://192.168.0.246:8080/admin/delete?username=carlos
7. I came back to repeater and changed the StockApi to http://192.168.0.246:8080/admin/delete?username=carlos deleting user carlos and solving the lab

## Why it worked
Website didn't check if user is authenticated to view the admin panel by changing StockApi to external servers IP

## How to detect in real pentest
Look for StockApi, image and URL parameters, change it to defeault gateways such as http://192.168.0.X, change the X and observe the response

## Real world impact
User can get access to admin panels and external systems which can lead to data leak
