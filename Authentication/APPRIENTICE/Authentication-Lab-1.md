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
