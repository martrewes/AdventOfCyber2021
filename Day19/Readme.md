# `[Blue Teaming]` Something Phishy Is Going On

## Story
>McSkidy received reports of multiple phishing attempts from various elves. 
>
>One of the elves shared the email that was sent to her, along with the attachment. The email was forwarded as a .eml file, along with the base64 encoded string in a text file. Is Grinch Enterprises up to their shenanigans? 

### Who was the email sent to? (Answer is the email address) `******************.***`

```bash
$ cat email.eml | grep "Delivered-To"
Delivered-To: elfmcphearson@tbfc.com
```

Answer: `elfmcphearson@tbfc.com`

>Phishing emails use similar domains of their targets to increase the likelihood the recipient will be tricked into interacting with the email. 
### Who does it say the email was from? (Answer is the email address) `********************.****`

```bash
$ cat email.eml | grep "From:"
From: =?utf-8?q?TBFC_Customers_Service?= <customerservice@t8fc.info>
```

Answer: `customerservice@t8fc.info`

### Sometimes phishing emails have a different reply-to email address. If this email was replied to, what email address will receive the email response? `****************.******`
Answer: `fisher@tempmailz.grinch`

### Less sophisticated phishing emails will have typos. What is the misspelled word? `*******`

Answer: `stright`

The email contains a link that will redirect the recipient to a fraudulent website in an effort to collect credentials. 

### What is the link to the credential harvesting website? `*****://*****************/***/*******/`

Answer: `https://89xgwsnmo5.grinch/out/fishing/`

### View the email source code. There is an unusual email header. What is the header and its value? `************** ****`

Answer: `X-GrinchPhish: >;^)`

You received other reports of phishing attempts from other colleagues. Some of the other emails contained attachments. Open attachment.txt. 

### What is the name of the attachment? `***************************.***`

Answer: `password-reset-instructions.pdf`

### What is the flag in the PDF file? `***{***************************}`

```
$ cat attachment-base64.txt | base64 -d > out.pdf
```

Answer: `THM{A0C_Thr33_Ph1sh1ng_An4lys!s}`
