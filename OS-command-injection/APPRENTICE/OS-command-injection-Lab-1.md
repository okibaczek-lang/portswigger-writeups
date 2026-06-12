# OS command injection lab 1 - OS command injection, simple case

## What was the vulnerability
Check stock function. Application uses shell command containing productId and storeId.

## Exploit
1. I captured the check stock function in Burp Proxy and sent it to Repeater.
2. The application displayed product and store ID.
3. I tried using command separators and injecting a command.
4. The injection point was between productId and storeId.
5. I injected productId=1|whoami&storeId=1
6. I received output containing the system user, which solved the lab.
## Why it worked
One of the parameters was executed inside a system shell without sanitization.
The | character was interpreted by the shell, allowing execution of an additional command.

## How to detect in real pentest
Look for parameters that are processed server-side and influence system behavior.
Test injection points using payloads like |whoami, ;id, or && id and observe whether the response changes or contains command output.

## Real world impact
An attacker can execute arbitrary system commands, potentially leading to data access, system enumeration, and full remote code execution.
