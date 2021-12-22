# `[Blue Teaming]` How It Happened

## Story
> McSkidy has finally gotten around to identifying the first trace of Grinch Enterprises within their network. They're looking at local machines to determine what exactly they did when they first entered the network. Can you help them make sense of what happened?

### What is the username (email address of Grinch Enterprises) from the decoded script? `******.***********.**********.***`

I pulled the `.doc` from their server to work on it locally.

```shell
$ python oledump.py Santa_Claus_Naughty_List_2021.doc -s 8 -d
$H

  @}k�0.(�	�T���GrinchEnterprisesIsComingForYou�����ahNtWnl0cVNHa25EeREaT0BaYRNBWmFid3RlVkJ0ZVp1Tk9aenRURGhkSxNHa2FZbEobVUdrR1NHa3FPQEoWSUERE1VBdGVWQnRlWkdOT1p6dFRTamR5VUBKYRBATk8TQnQWTWprcUxCe25EentHT0ARGld5cGFwcnVyS...
```

I pulled this [string](oleDumpBase64.txt) from the dump and used cyberchef to first decode it from base64, then xor it with the value of 35 (decimal). This then gave another base64 [string](secondStageBase64.txt) which I decoded again to get the [script](decodedScript.txt).

<details>
  <summary>Answer:</summary>

```
Grinch.Enterprises.2021@gmail.com
```
</details>

### What is the mailbox password you found? `*******************`

<details>
  <summary>Answer:</summary>

```
S@ntai$comingt0t0wn
```
</details>

### What is the subject of the email? `********* ********`

<details>
  <summary>Answer:</summary>

```
Christmas Wishlist
```
</details>

### What port is the script using to exfiltrate data from the North Pole? `***`

<details>
  <summary>Answer:</summary>

```
587
```
</details>

### What is the flag hidden found in the document that Grinch Enterprises left behind? `********************` 
>(Hint: use the following command oledump.py -s {stream number} -d, the answer will be in the caption).

```shell
$ python oledump.py Santa_Claus_Naughty_List_2021.doc -s 7 -d 
```

<details>
  <summary>Answer:</summary>

```
YouFoundGrinchCookie
```
</details>

### There is still a second flag somewhere... can you find it on the machine? `****************`

There was an [image](Pictures/Grinch2021/flag2.PNG) in `Pictures\Grinch2021`

<details>
  <summary>Answer:</summary>

```
S@nt@c1Au$IsrEAl
```
</details>