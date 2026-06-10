# SSRF Lab 1 - Basic SSRF against the local server

## What was the vulnerability
The application was vulnerable to SSRF in the stock checking feature, allowing access to internal resources like localhost via user-controlled URL input.

## Exploit
1. I tested direct access to /admin, which was not reachable externally.
2. I used the “Check stock” feature and intercepted the request in Burp Suite.
3. I identified that the stockApi parameter is used to fetch a URL.
4. I modified stockApi and injected `http://localhost/admin`.
5. The server performed an internal request and returned the admin panel in the HTTP response.
6. Inside the returned HTML, I found /admin/delete?username=carlos.
7. I reused the same SSRF parameter to access this endpoint and delete the user Carlos, solving the lab.

## Why it worked
The application did not validate or restrict the user-controlled stockApi parameter, allowing the backend to perform arbitrary internal HTTP requests.

## How to detect in Real pentest
Look for parameters that accept URLs such as stockApi, url, image, or similar. Replace values with:
- http://127.0.0.1
- http://localhost
- internal IP ranges (e.g. 192.168.x.x, 10.x.x.x)
and observe response differences or internal content exposure.

## Real world impact
Access to internal services, admin panels, and sensitive endpoints, potentially leading to data exposure or internal system compromise.
