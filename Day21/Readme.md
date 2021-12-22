# `[Blue Teaming]` Needles In Computer Stacks

## Story
> Grinch Enterprises have been very sneaky this year - using multiple attack vectors (both know and unknown) to wreak havoc across the Best Festival Company. It's 4 days from Christmas and there's still so much work to do! McBlue, the only technical person, has suggested using automation and tooling to detect malicious files across the network. Can you work with him to remove any malicious files from the network?

This one is basically a tutorial on how to use yara rules.

>We changed the text in the string `$a` as shown in the eicaryara rule we wrote, from `X5O` to `X50`, that is, we replaced the letter O with the number 0. The condition for the Yara rule is `$a` and `$b` and `$c` and `$d`. 

### If we are to only make a change to the first boolean operator in this condition, what boolean operator shall we replace the '`and`' with, in order for the rule to still hit the file? `**`
<details>
  <summary>Answer:</summary>

```
or
```
</details>

### What option is used in the Yara command in order to list down the metadata of the rules that are a hit to a file? `**`

<details>
  <summary>Answer:</summary>

```
-m
```
</details>

### What section contains information about the author of the Yara rule? `********`

<details>
  <summary>Answer:</summary>

```
metadata
```
</details>

### What option is used to print only rules that did not hit? `**`

<details>
  <summary>Answer:</summary>

```
-n
```
</details>

### Change the Yara rule value for the `$a` string to `X50`. Rerun the command, but this time with the `-c` option. What is the result? `*`

<details>
  <summary>Answer:</summary>

```
0
```
</details>
