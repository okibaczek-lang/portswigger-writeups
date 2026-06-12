# SSRF LAB - Basic SSRF against another back-end system

## What was vulnerable
Check stock functionality. User could modify the StockApi parameter and make the server send requests to arbitrary URLs.

## Attack surface
Internal IP range hosting the admin interface.

## Exploit
1. I captured the check stock request in Burp Proxy.
2. I sent it to Repeater and changed the StockApi value to http://192.168.0.1:8080/admin.
3. I sent the request to Intruder and highlighted the last octet of the IP address (1) as a payload position.
4. In the payload settings I selected numbers and configured a range from 1 to 255.
5. After starting the attack I found a response with status code 200.
6. I reviewed the response and found the delete user function available at http://192.168.0.246:8080/admin/delete?username=carlos.
7. I returned to Repeater and changed StockApi to http://192.168.0.246:8080/admin/delete?username=carlos, deleting Carlos and solving the lab.

## Why it worked
The application did not validate the destination of the StockApi parameter, allowing requests to internal systems and the admin panel.

## How to detect in real pentest
Look for parameters such as StockApi, URL or image. Change them to internal addresses such as http://192.168.0.X and observe the response.

## Real world impact
An attacker may gain access to internal systems, admin panels or sensitive data that should not be exposed externally.

