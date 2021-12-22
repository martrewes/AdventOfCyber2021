# `[Networking]` Where is All This Data Going

## Story
>McSkidy recently found out that a large amount of traffic is entering one system on the network. Use your traffic analysis skills to determine what kind of activities Grinch Enterprises are performing.

This activity had a provided network capture [AoC3.pcap](AoC3.pcap) which we had to analise in WireShark. 

### In the HTTP #1 - GET requests section, which directory is found on the web server? `*****`

<details>
  <summary>Answer:</summary>

```
login
```
</details>


### What is the username and password used in the login page in the HTTP #2 - POST section? `**********************`

<details>
  <summary>Answer:</summary>

```
McSkidy:Christmas2021!
```
</details>

### What is the User-Agent's name that has been sent in HTTP #2 - POST section? `***********************{********************************}`

<details>
  <summary>Answer:</summary>

```
TryHackMe-UserAgent-THM{d8ab1be969825f2c5c937aec23d55bc9}
```
</details>

### In the DNS section, there is a TXT DNS query. What is the flag in the message of that DNS query? `***{********************************}`
THM{dd63a80bf9fdd21aabbf70af7438c257}

### In the FTP section, what is the FTP login password? `**********`

<details>
  <summary>Answer:</summary>

```
TryH@ckM3!
```
</details>

### In the FTP section, what is the FTP command used to upload the secret.txt  file? `****`

`STOR`

### In the FTP section, what is the content of the secret.txt file? `*********`

<details>
  <summary>Answer:</summary>

```
123^-^321
```
</details>
