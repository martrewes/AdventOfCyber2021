# `[Web Exploitation]` Pesky Elf Forum

## Story

>The Elf Forum is where all the elves express their joy and excitement about Christmas, but Grinch Enterprises has one bad admin account, and they've installed a plugin that changes all mentions of Christmas to Buttmas!! McSkidy needs to find that admin account and disable the plugin.

Basically, all I had to do was follow the instuctions. Pasted below:

Click the green "Start Machine" button on the top right of this task. Once the machine has loaded, please click the following link:
https://IP_ADDRESS.p.thmlabs.com (if you receive an error, wait 30 seconds and try refreshing the page)

Here you'll find the elves forum where they talk about and spread the joy of Christmas! As you explore the forum and click on the different topics and threads, you'll notice that every mention of Christmas has been changed to Buttmas! This is because the grinch has an admin account and has installed a plugin that changes every mention of Christmas to Buttmas! You'll need to take over the Grinch account and disable the plugin to restore the Christmas joy!

First, click the login link towards the top of the page and log in with the following credentials:

![img](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/e1dcfc1c259cbfee5158eb7906153d54.png)

Username: **McSkidy**

Password: **password**

Now that you're logged in you'll notice the navigation bar has now changed from Login to Settings and Logout.

![img](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/13f9f54f0071831e0cc4427a875616b0.png)

Click on the Settings link, and you'll notice a feature for changing McSkidy's login password. Try changing your password to pass123. When you do this, you'll notice your address bar changes to look like the below screenshot (yours will have the IP address 10.10.152.138 instead). If you can somehow trick the Grinch into visiting this URL, it will change their password to pass123.

![img](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/029984cba68e5c22d9b8caa27249baa5.png)

Let's now go back to the forum and visit one of the threads. If you scroll to the bottom, you'll notice that you are able to leave a comment. Try leaving the following comment:

`hello <u>world</u>`

Once your comment is posted, you'll see that the word world has been underlined.

![img](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/253564d07312e7771461f312c66dbd6d.png)

This means the comment is reflected as you wrote it without the underline HTML tags being stripped out. As this isn't being stripped out, you can try the HTML script tags instead to see if the website will run any JavaScript that is entered.

Using the URL, you found earlier for changing the user's password, you can try the following payload:

```
<script>fetch('/settings?new_password=pass123');</script>
```

The `<script>` tag tells the browser we want to run some JavaScript, and the `fetch` command makes a network request to the specified URL.

After posting the above as a comment, you could view the webpage source to see whether it has been shown correctly. The screenshot below shows us that the script tags aren't being stripped out or disabled and, in fact, are working:

![img](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/da598fccc47887d9e651b3d072da8844.png)

Now that we have this XSS running on the forum, it means that any logged in users viewing the thread will automatically have their password changed to pass123. So let's log out and see if the Grinch has visited the thread by trying to log in as them (It may take up to a minute before the Grinch visits the page and their password changes).

Username: **grinch**

Password: **pass123**

Once logged in, go to the settings page again, and this time, you'll discover another feature with the option to disable the Christmas to Buttmas plugin.

![img](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/9dd7eee4ab8e7cf2acaa48f83843b78a.png)

Disable the plugin, and you'll be awarded a flag which can be entered below.

<details>
  <summary>Answer:</summary>

```
THM{NO_MORE_BUTTMAS}
```
</details>