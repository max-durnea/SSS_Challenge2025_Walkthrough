# CTF Walkthrough

This document explains the steps and methods used to capture each flag in the CTF challenge.

## FLAG1: SQL Injection (Login Form)

To capture **FLAG1**, I used an **SQL Injection** on the login form. Here’s how I did it:

- **Username**: `admin'--`
- **Password**: `'`
  
I sent the following request using `curl`:

curl -X POST -d "username=admin'--&password=''" http://141.85.224.116:8083/login.php

This allowed me to bypass the login form and retrieve the flag.

## FLAG2: Command Injection (Ping Command)
For **FLAG2**, I exploited a **command injection** vulnerability on the server. I used the following input:

141.85.224.116 -c 1; cat /home/ctf/flag
- The -c 1 flag made the ping command send just one packet.
- The ; operator allowed me to escape the ping command and execute arbitrary commands, in this case, reading the flag from the file /home/ctf/flag.

## FLAG3: Cookie Modification (Burp Suite)
- Intercepted the GET request in Burp Suite
- I set the FLAG cookie to applepie 
- Sent the request and got the flag from the response header 

## FLAG4: Caesar Cipher Decryption
For FLAG4, I discovered the flag in the source code of the site. The following parts were found:
- First Part: FFF{rirel_
- Second Part: svyr_
- Third Part: unf_
- Fourth Part: srryvatf}
Upon noticing that FFF should be SSS (a Caesar cipher shift of 13), I decrypted the flag by shifting each letter back by 13 positions using an online tool.
- Decryption Tool: https://cryptii.com/pipes/caesar-cipher

## FLAG5: Base64 Decoding
For FLAG5, I inspected the source files of the site and found a Base64 encoded string within a comment. I decoded it with the following command:
**echo "U1NTe2NhZ2VfdHJhdm9sdGF9Cg==" | base64 --decode**
This gave me the final flag.