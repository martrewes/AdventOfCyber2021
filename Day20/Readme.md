# `[Blue Teaming]` What's the Worst That Could Happen?

## Story

>McPayroll is processing the bonuses for all the hardworking elves. One of the Elves has sent McPayroll a file that they're claiming contains their updated payment information. The only problem is that she doesn't recognize the Elf - could this be a sneaky attack from Grinch Enterprises to cause more havoc? Analyze the file to see if you can determine whether it's malicious or not!
>
>McPayroll provides this file to McSkidy who is a member of the security team. McSkidy is a wise elf. She knows to analyze this file in a sandboxed environment. Therefore, she fired up her Remnux VM to take a look at the suspicious file. She unzipped the archive and saw that there was a folder named 'Samples' and a file named 'testfile' in the zip archive. She copied these files over to her Remnux desktop to begin the analysis.
---
>Open the terminal and navigate to the file on the desktop named 'testfile'. Using the 'strings' command, check the strings in the file. There is only a single line of output to the 'strings' command. 

### What is the output? `**************************}*****************************************`

<details>
  <summary>Answer:</summary>

```
X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*
```
</details>

>Check the file type of 'testfile' using the 'file' command. 

### What is the file type? `***** ***** **** *****`

<details>
  <summary>Answer:</summary>

```
EICAR virus test files
```
</details>

>Calculate the file's hash and search for it on VirusTotal. 

### When was the file first seen in the wild? `********** **:**:**`

<details>
  <summary>Answer:</summary>

```
2005-10-17 22:03:48
```
</details>

### On VirusTotal's detection tab, what is the classification assigned to the file by Microsoft? `*****:***/***************`

<details>
  <summary>Answer:</summary>

```
Virus:DOS/EICAR_Test_File
```
</details>

>Go to [this link](https://www.eicar.org/?page_id=3950) to learn more about this file and what it is used for. 

### What were the first two names of this file? `*******.*** ** ************.***`

<details>
  <summary>Answer:</summary>

```
ducklin.htm or ducklin-html.htm
```
</details>

>The file has 68 characters in the start known as the known string. It can be appended with whitespace characters upto a limited number of characters. 

### What is the maximum number of total characters that can be in the file? `***`

<details>
  <summary>Answer:</summary>

```
128
```
</details>