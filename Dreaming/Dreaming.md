Hi, hope you are well. As you can see, this is the first time I've shared my gym experience on TryHackMe. I hope you like it. The presentation focuses on the new “Dreaming” room of TryHackMe, a very exciting “Easy” level.

![Alt text](img/dreaming1.png)

![Alt text](img/dreaming2.png)

I started by checking for open ports on the IP address I received with the nmap tool using the command **nmap -sV -vv IP** 
The result shows that I have ports 22 and 80 open with the respective ssh and http services. Ok, so it's off to a good start.

![Alt text](img/dreaming3.png)

Here is what the website shows us deploy on port 80.

![Alt text](img/dreaming4.png)

So I run a scan of the site's subfolders with gobuster.

![Alt text](img/dreaming5.png)

Okay, I think searching subfolders led us to an important discovery. The **/app** subfolder which in turn leads us to another website set up with the **pluck CMS**.

![Alt text](img/dreaming6.png)

![Alt text](img/dreaming7.png)

![Alt text](img/dreaming8.png)

**A file upload restriction bypass** vulnerability in **Pluck CMS version 4.7.13**, and with the **searchsploit** command I was able to find some python code that I copied to my working directory to exploit the vulnerability.

![Alt text](img/dreaming9.png)

![Alt text](img/dreaming10.png)

This python code takes as parameters the **IP, the port, the connection password and the path to access the connection page**. I searched for default password on pluck CMS and came across **password**. This python code gives us direct **p0wny shell** access to the server and we access it with the link it generates.
![Alt text](img/dreaming11.png)

To further investigate, I configured my machine to listen on port 9001. Next, I executed a reverse shell command via the P0wny shell.

![Alt text](img/dreaming12.png)

![Alt text](img/dreaming13.png)

After gaining access as user **"www-data"**, I initiated the privilege escalation process. My first success was to locate the flag associated with the user **"Lucien"**. After exploring various files, I finally accessed the **/opt** directory where two files contained the information necessary to recover Lucien's password. Using this data, I managed to connect as Lucien via the SSH service using the password I had discovered... Ouff.

![Alt text](img/dreaming14.png)

![Alt text](img/dreaming15.png)

![Alt text](img/dreaming16.png)

Following the acquisition of Lucien's flag, I noticed that the **getDreams.py** file was present in the directory of the **"death"** user as well as in the **/opt** directory. Although I was able to open it in the latter location, I could not find a password there.

![Alt text](img/dreaming17.png)

![Alt text](img/dreaming18.png)

![Alt text](img/dreaming19.png)

![Alt text](img/dreaming20.png)

![Alt text](img/dreaming21.png)

![Alt text](img/dreaming22.png)

![Alt text](img/dreaming23.png)

![Alt text](img/dreaming24.png)

![Alt text](img/dreaming25.png)

![Alt text](img/dreaming26.png)

![Alt text](img/dreaming27.png)

![Alt text](img/dreaming28.png)

![Alt text](img/dreaming29.png)

![Alt text](img/dreaming30.png)

![Alt text](img/dreaming31.png)

![Alt text](img/dreaming32.png)

![Alt text](img/dreaming33.png)

![Alt text](img/dreaming34.png)

![Alt text](img/dreaming35.png)