# `[Networking]` Sharing Without Caring

## Story
>Grinch Enterprises has been leaving traces of how their hackers have been accessing data from the system - you’ve found a unique server they use. We need your help to find out what method they’ve been using to extract any data.
>
>We have noticed that `10.10.207.192` is generating unusual traffic. We highly suspect that Grinch Enterprises are using it to access our data. We will use Nmap to discover the services are running on their server.

>Scan the target server with the IP `10.10.207.192`. Remember that MS Windows hosts block pings by default, so we need to add `-Pn`, for example, `nmap -Pn 10.10.207.192` for the scan to work correctly. 
### How many TCP ports are open? `*`

```
$ nmap -Pn 10.10.207.192
Starting Nmap 7.80 ( https://nmap.org ) at 2021-12-12 16:54 GMT
Nmap scan report for 10.10.207.192
Host is up (0.031s latency).
Not shown: 993 filtered ports
PORT     STATE SERVICE
22/tcp   open  ssh
111/tcp  open  rpcbind
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
2049/tcp open  nfs
3389/tcp open  ms-wbt-server
```

Answer: `7`

>Network File System (NFS) is a protocol that allows the ability to transfer files between different computers and is available on many systems, including MS Windows and Linux. Consequently, NFS makes it easy to share files between various operating systems.
>
>In the scan results you received earlier, you should be able to spot NFS or mountd, depending on whether you used the -sV option with Nmap or not. 

### Which port is detected by Nmap as NFS or using the mountd service? `****`

Answer: `2049`

>Now that we have discovered an NFS service is listening, let’s check what files are being shared. We can do this using the command showmount. In the terminal below, we run `showmount -e 10.10.207.192`. The `-e` or `--exports` show the NFS server’s export list.

### How many shares did you find? `*`

```
$ showmount -e 10.10.207.192
Export list for 10.10.207.192:
/share        (everyone)
/admin-files  (everyone)
/my-notes     (noone)
/confidential (everyone)
```

Answer: `4`

### How many shares show “everyone”? `*`

Answer: `3`

>Let’s try to mount the shares we have discovered. We can create a directory on the AttackBox using `mkdir tmp1`, where `tmp1` is the directory’s name. Then we can use this directory  we created to mount the public NFS share using: `mount 10.10.207.192:/my-notes tmp1`.
>
>We can see that the mounting has failed. `my-notes` is not public and requires specific authentication mechanisms that we don’t have access to. Let’s try again with the other folder, `share`.

>There are two text files. We can open the file using any text editor such as nano FILENAME or something quicker such as less FILENAME.

### What is the title of file 2680-0.txt? `***********`

```
$ sudo mount 10.10.207.192:/share tmp1 -o nolock
$ ls tmp1/
132-0.txt  2680-0.txt
$ head tmp1/2680-0.txt
Title: Meditations

Author: Marcus Aurelius

Translator: Meric Casaubon

Release Date: June, 2001 [eBook #2680]
[Most recently updated: March 8, 2021]

Language: English
```

Answer: `Meditations`
>It seems that Grinch Enterprises has forgotten their SSH keys on our system. One of the shares contains a private key used for SSH authentication (id_rsa).

### What is the name of the share? `************`

```
$ sudo mount 10.10.207.192:/confidential tmp1 -o nolock
$ ls tmp1/
ssh
```

Answer: `Confidential`

### We can calculate the MD5 sum of a file using md5sum FILENAME. What is the MD5 sum of id_rsa? `********************************`

```
$ md5sum tmp1/ssh/id_rsa
3e2d315a38f377f304f5598dc2f044de  tmp1/ssh/id_rsa
```

Answer: `3e2d315a38f377f304f5598dc2f044de`