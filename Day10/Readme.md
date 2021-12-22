# `[Networking]` Offensive is the Best Defensive

## Story
>McSkidy is trying to discover how the attackers managed to penetrate the network and cause damage to the Best Festival Company’s infrastructure. She decided to start doing a security assessment of her systems to discover how Grinch Enterprises managed to cause this damage. She started by conducting a security assessment of her systems to discover how Grinch Enterprises managed to cause this damage and wonders what service they exploited.
>
>Before McSkidy starts firing up Nmap, let’s review some keywords related to her task. If you are familiar with the terms IP address, protocol, server, and port number, feel free to skip the following three sections and start directly with the Nmap section.

Looks to be based around nmap. Just going to follow along.

### Help McSkidy and run nmap -sT 10.10.141.56. How many ports are open between 1 and 100? `*`

```
$ nmap -sT 10.10.141.56
Starting Nmap 7.92 ( https://nmap.org ) at 2021-12-10 14:46 GMT
Nmap scan report for 10.10.141.56
Host is up (0.031s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
```
<details>
  <summary>Answer:</summary>

```
2
```
</details>

### What is the smallest port number that is open? `**`

<details>
  <summary>Answer:</summary>

```
22
```
</details>

### What is the service related to the highest port number you found in the first question? `****`

<details>
  <summary>Answer:</summary>

```
http
```
</details>

### Now run nmap -sS 10.10.141.56. Did you get the same results? (Y/N) `*`

<details>
  <summary>Answer:</summary>

```
Y
```
</details>

### If you want Nmap to detect the version info of the services installed, you can use nmap -sV 10.10.141.56. What is the version number of the web server? `****** ***** *.*.**`

```
Nmap scan report for 10.10.141.56
Host is up (0.030s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.49
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

<details>
  <summary>Answer:</summary>

```
Apache httpd 2.4.49
```
</details>

>By checking the [vulnerabilities related to the installed web server](https://httpd.apache.org/security/vulnerabilities_24.html), you learn that there is a critical vulnerability that allows path traversal and remote code execution. Now you can tell McSkidy that Grinch Enterprises used this vulnerability. 

### What is the CVE number of the vulnerability that was solved in version 2.4.51? `**************`

Used the link provided.

<details>
  <summary>Answer:</summary>

```
CVE-2021-42013
```
</details>

>You are putting the pieces together and have a good idea of how your web server was exploited. McSkidy is suspicious that the attacker might have installed a backdoor. She asks you to check if there is some service listening on an uncommon port, i.e. outside the 1000 common ports that Nmap scans by default. She explains that adding -p1-65535 or -p- will scan all 65,535 TCP ports instead of only scanning the 1000 most common ports. 

### What is the port number that appeared in the results now? `*****`

```
Not shown: 65532 closed tcp ports (conn-refused)
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
20212/tcp open  unknown
```

<details>
  <summary>Answer:</summary>

```
20212
```
</details>

### What is the name of the program listening on the newly discovered port?  `*******`

```
nmap -sV 10.10.141.56 -p20212
Starting Nmap 7.92 ( https://nmap.org ) at 2021-12-10 14:53 GMT
Nmap scan report for 10.10.141.56
Host is up (0.029s latency).

PORT      STATE SERVICE VERSION
20212/tcp open  telnet  Linux telnetd
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```
<details>
  <summary>Answer:</summary>

```
telnetd
```
</details>