# `[Special by John Hammond]` Santa's Bag of Toys

## Story

>McSkidy was notified of some terrible news! Santa's laptop, which he uses to prepare his bag of toys for Christmas, is missing! We believe a minion at the Grinch Enterprise stole it, but we need to find out for sure. It is up to us to determine what actor compromised the laptop and recover Santa's bag of toys!
>
>Unfortunately, The Best Festival Company had minimal monitoring tools on Santa's laptop (he is the boss, after all)! All we have to work with are some PowerShell Transcription Logs we were able to remotely recover just after it went missing. You can find the transcription logs within the SantasLaptopLogs folder on the Desktop of the attached Windows virtual machine.

>*I didn't really have time to document the process, so I will just leave the answers here. Fun challenge though!*

### What operating system is Santa's laptop running ("OS Name")?

<details>
  <summary>Answer:</summary>

```
Microsoft Windows 11 Pro
```
</details>

### What was the password set for the new "backdoor" account?

<details>
  <summary>Answer:</summary>

```
grinchstolechristmas
```
</details>

### In one of the transcription logs,  the bad actor interacts with the target under the new backdoor user account, and copies a unique file to the Desktop. Before it is copied to the Desktop, what is the full path of the original file? 

<details>
  <summary>Answer:</summary>

```
C:\Users\santa\AppData\Local\Microsoft\Windows\UsrClass.dat
```
</details>

### The actor uses a Living Off The Land binary (LOLbin) to encode this file, and then verifies it succeeded by viewing the output file. What is the name of this LOLbin?

<details>
  <summary>Answer:</summary>

```
certutil.exe
```
</details>

### Drill down into the folders and see if you can find anything that might indicate how we could better track down what this SantaRat really is. What specific folder name clues us in that this might be publicly accessible software hosted on a code-sharing platform?

<details>
  <summary>Answer:</summary>

```
.github
```
</details>

### Additionally, there is a unique folder named "Bag of Toys" on the Desktop! This must be where Santa prepares his collection of toys, and this is certainly sensitive data that the actor could have compromised. What is the name of the file found in this folder? 

<details>
  <summary>Answer:</summary>

```
bag_of_toys.zip
```
</details>

### What is the name of the user that owns the SantaRat repository?

<details>
  <summary>Answer:</summary>

```
Grinchiest
```
</details>

### What is the name of the executable that installed a unique utility the actor used to collect the bag of toys?

<details>
  <summary>Answer:</summary>

```
uharc-cmd-install.exe
```
</details>

### What are the contents of these "malicious" files (coal, mold, and all the others)?

<details>
  <summary>Answer:</summary>

```
GRINCHMAS
```
</details>

### What is the password to the original bag_of_toys.uha archive? (You do not need to perform any password-cracking or bruteforce attempts)

<details>
  <summary>Answer:</summary>

```
TheGrinchiestGrinchmasOfAll
```
</details>

### How many original files were present in Santa's Bag of Toys?

<details>
  <summary>Answer:</summary>

```
228
```
</details>