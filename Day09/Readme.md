# `[Networking]` Where is All This Data Going

## Story
>McSkidy recently found out that a large amount of traffic is entering one system on the network. Use your traffic analysis skills to determine what kind of activities Grinch Enterprises are performing.

This activity had a provided network capture [AoC3.pcap](AoC3.pcap) which we had to analise in WireShark. 

### In the HTTP #1 - GET requests section, which directory is found on the web server? `*****`

Answer: `login`


### What is the username and password used in the login page in the HTTP #2 - POST section? `**********************`

Answer: `McSkidy:Christmas2021!`

### What is the User-Agent's name that has been sent in HTTP #2 - POST section? `***********************{********************************}`

Answer: `TryHackMe-UserAgent-THM{d8ab1be969825f2c5c937aec23d55bc9}`

### In the DNS section, there is a TXT DNS query. What is the flag in the message of that DNS query? `***{********************************}`
THM{dd63a80bf9fdd21aabbf70af7438c257}

### In the FTP section, what is the FTP login password? `**********`

Answer: `TryH@ckM3!`

### In the FTP section, what is the FTP command used to upload the secret.txt  file? `****`

`STOR`

### In the FTP section, what is the content of the secret.txt file? `*********`

Answer: `123^-^321`
