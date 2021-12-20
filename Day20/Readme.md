# `[Blue Teaming]` What's the Worst That Could Happen?

## Story

>McPayroll is processing the bonuses for all the hardworking elves. One of the Elves has sent McPayroll a file that they're claiming contains their updated payment information. The only problem is that she doesn't recognize the Elf - could this be a sneaky attack from Grinch Enterprises to cause more havoc? Analyze the file to see if you can determine whether it's malicious or not!
>
>McPayroll provides this file to McSkidy who is a member of the security team. McSkidy is a wise elf. She knows to analyze this file in a sandboxed environment. Therefore, she fired up her Remnux VM to take a look at the suspicious file. She unzipped the archive and saw that there was a folder named 'Samples' and a file named 'testfile' in the zip archive. She copied these files over to her Remnux desktop to begin the analysis.
---
>Open the terminal and navigate to the file on the desktop named 'testfile'. Using the 'strings' command, check the strings in the file. There is only a single line of output to the 'strings' command. 

### What is the output? `**************************}*****************************************`

Answer: `X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*`

>Check the file type of 'testfile' using the 'file' command. 

### What is the file type? `***** ***** **** *****`

Answer: `EICAR virus test files`

>Calculate the file's hash and search for it on VirusTotal. 

### When was the file first seen in the wild? `********** **:**:**`

Answer: `2005-10-17 22:03:48`

### On VirusTotal's detection tab, what is the classification assigned to the file by Microsoft? `*****:***/***************`

Answer: `Virus:DOS/EICAR_Test_File`

>Go to [this link](https://www.eicar.org/?page_id=3950) to learn more about this file and what it is used for. 

### What were the first two names of this file? `*******.*** ** ************.***`

Answer: `ducklin.htm or ducklin-html.htm`

>The file has 68 characters in the start known as the known string. It can be appended with whitespace characters upto a limited number of characters. 

### What is the maximum number of total characters that can be in the file? `***`

Answer: `128`