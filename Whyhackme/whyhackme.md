Hello It's Me Again. We are going to work on a new room on THM. Let's go.
The name of the room is: **WhyHackMe**.
![Alt text](img/1.png)
As usual I always start with a list of ports to know the open ports and the services available.
![Alt text](img/whyhack1.png)
There are 3 ports open on 21, 22 and 80 with the respective services: ftp, ssh and http.
nmap shows us an 'update.txt' file and that we can log in as Anonymous. Let's download the file to our machine to learn more.
![Alt text](img/whyhack2.png)
![Alt text](img/whyhack3.png)
Ok the update.txt container is a note from the admin specifying that the new information for the new account is only accessible via localhost in the pass.txt file.
![Alt text](img/whyhack4.png)
![Alt text](img/whyhack5.png)
![Alt text](img/whyhack6.png)
This is the website that is hosted and is a blog on which we must login.
not having the connection information, I made a small enumeration of the subdirectories with the dirsearch tool. and here are the available directories:
/assets/
/config.php
/login.php
/register.php
![Alt text](img/whyhack7.png)
These directories don't give anything important so I register then I connect to the vulnerability search.
![Alt text](img/whyhack8.png)
![Alt text](img/whyhack9.png)
