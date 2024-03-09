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

Okay, on a un indexage de fichier et en continuant plus loin on tombe sur un site web e-commerce.

![Alt text](image/blueprint7.png)
![Alt text](image/blueprint8.png)

Dans le répertoire **docs** vous trouverez plein d'autres fichiers mais je pense que du côté de catalog on trouvera des trucs bien plus interessant.

![Alt text](image/blueprint9.png)

Ne sachant pas ce que c'est **oscommerce** j'ai effectué une peite recherche et le premier article parle déjà d'exploit... Très interessant hihihi.

![Alt text](image/blueprint10.png)
![Alt text](image/blueprint11.png)

Avec la commande **searchsploit** et **locate** bon j'ai le fichier d'exploit plus qu'à tester.

NB: Si vous ne trouvez pas d'exploit avec l'outil searchsploit faites un tour sur internet et fouillez correctement vous allez tomber sur des trucs interessants.

![Alt text](image/blueprint12.png)

Bon voilà, on a eu shell cool...

Bon vite vite, voyons voir les différents comptes sur cette machine.
![Alt text](image/blueprint13.png)

Ok, je me suis accroché rapidement au compte **Administator** et avec un peu de fouille dans tous les répertoires je suis tombé sur le fichier *root.txt.txt*.. good good.

![Alt text](image/blueprint14.png)
![Alt text](image/blueprint15.png)

Ok, Let's go... allons à la recherche du hachage NTLM de l'utilisateur "Lab" déchiffré.

![Alt text](image/blueprint16.png)

A cette étape étant un peu perdu, cet article m'a aidé : https://aas-s3curity.gitbook.io/cheatsheet/internalpentest/active-directory/post-exploitation/extracting-credentials/retrieve-windows-hashes pour l'extraction des credentials des users.

J'ai compris que les hachages NTLM sont stockés dans la base de données SAM sur la machine ou dans la base de données NTDS du contrôleur de domaine. Il existe plusieurs méthodes pour extraire les credentials en voici une:

![Alt text](image/blueprint17.png)
![Alt text](image/blueprint18.png)
![Alt text](image/blueprint19.png)

L'exécutable reg.exe m'a permi de sauvegarder une partie ou l'intégralité de la base de registre. Puis j'ai téléchargé ces fichiers sur ma propre machine et avec l'outil **samdump2** j'ai extraire les hashs LM et NTLM des credentials de connexion des comptes. Il m'a suffit de décrypter celà ici: https://crackstation.net/

![Alt text](image/blueprint20.png)
![Alt text](image/blueprint21.png)

Vous pouvez utiliser ce script: https://github.com/fortra/impacket/blob/master/examples/secretsdump.py au lieu de l'outil **samdump2** si l'installation n'a pas réussir.

![Alt text](image/blueprint22.png)
![Alt text](image/blueprint23.png)

Bon voilà tout est bien qui finit bien à une prochaine fois...😆😆
