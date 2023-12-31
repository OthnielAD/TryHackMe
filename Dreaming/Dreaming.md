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

After gaining access as user *"www-data"*, I initiated the privilege escalation process. My first success was to locate the flag associated with the user *"Lucien"*. After exploring various files, I finally accessed the **/opt** directory where two files contained the information necessary to recover Lucien's password. Using this data, I managed to connect as Lucien via the SSH service using the password I had discovered... Ouff.

![Alt text](img/dreaming14.png)

![Alt text](img/dreaming15.png)

![Alt text](img/dreaming16.png)

Following the acquisition of Lucien's flag, I noticed that the **getDreams.py** file was present in the directory of the *"death"* user as well as in the **/opt** directory. Although I was able to open it in the latter location, I could not find a password there.

![Alt text](img/dreaming17.png)

After obtaining the flag from Lucien, I decided to check the privileges associated with the user by running the **sudo -l** command. This command revealed to me that Lucien had the possibility of executing the **getDreams.py** file located in the directory of the user *"death"*, without providing a password. To further analyze privilege escalation opportunities, I downloaded the **linpeas.sh** script to the machine. This should allow me to get a more detailed view of the system's potential vulnerabilities and weak points.

![Alt text](img/dreaming18.png)

![Alt text](img/dreaming19.png)

![Alt text](img/dreaming20.png)

In an incredible stroke of luck, I identified several interesting commands by running linpeas.sh. However, the one that particularly caught my attention was **"mysql"**, where I discovered the presence of a database named **"library"** containing a table called **"dreams"**.

![Alt text](img/dreaming21.png)

![Alt text](img/dreaming22.png)

![Alt text](img/dreaming23.png)

After a quick re-analysis of the **/opt/getDreams.py file**, I understood more about its functionality. In the for loop, it extracts the data from each row of the two columns of the **"dreams"** table. Then it creates a shell command using this data and executes it using the **"subprocess"** library. The resulting output of each command is then displayed on the screen. This led me to realize that by inserting a command such as **"/bin/sh"** or setting up a **reverse shell command** and then running the file from the *"death"* user's directory, it would be possible to get a shell as user *"death"*.

![Alt text](img/dreaming24.png)

![Alt text](img/dreaming25.png)

![Alt text](img/dreaming26.png)

Finally, I managed to log in as user *"death"* after retrieving his password from the getDreams.py file. Subsequently, I established an SSH connection using the credentials of *"death"*. However, switching to the *"morpheus"* user proved to be a complex challenge. Honestly, I spent a whole evening on this task without really succeeding, but this experience allowed me to acquire valuable knowledge.

![Alt text](img/dreaming27.png)

![Alt text](img/dreaming28.png)

First, I explored the files present in the directory of the user *"morpheus"*. Subsequently, despite some uncertainty about the direction to take, one of my attempts fortunately revived my momentum.

![Alt text](img/dreaming29.png)

I used the **"find"** command to find all files editable by user *"death"*.

![Alt text](img/dreaming30.png)

It turned out that the user *"death"* had the ability to modify the file **"shutil.py"**, a module used to compile the restore.py program from *"morpheus"*.

![Alt text](img/dreaming31.png)

Following this observation, I quickly looked for Python code to establish a reverse shell. I then launched the listen on my machine, knowing that "death" had the possibility of compiling the "restore.py" file of "morpheus". And guess what? It functioned. Yeah...

![Alt text](img/dreaming32.png)

![Alt text](img/dreaming33.png)

![Alt text](img/dreaming34.png)

![Alt text](img/dreaming35.png)

![Alt text](img/dreaming36.png)

Together we assisted Sandman in restoring his kingdom. Congratulations and thank you for following me. It was a real pleasure.