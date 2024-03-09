Salut tous!!!
Today, on s'accroche sur la room **BluePrint** de TryHackMe.

![Alt text](image/blueprint0.png)

Cette salle est constitué de deux questions.

![Alt text](image/blueprint1.png)

Sans plus tarder, lançons-nous dans cette aventure. Nous commençons par une reconnaissance de la machine avec l'outil **nmap**

![Alt text](image/blueprint2.png)
![Alt text](image/blueprint3.png)
![Alt text](image/blueprint4.png)

Grâce à cette reconnaissance on sait qu'il s'agit d'une machine qui tourne avec pour système d'exploitation Windows 7 et de plus on a plusieurs services en cours d'exécution. Explorons rapidement les services web sur les ports 80 et 8080

![Alt text](image/blueprint5.png)

Sur le port 80, nous voilà face à une erreur 404 sautons sur celui du port 8080.

![Alt text](image/blueprint6.png)
