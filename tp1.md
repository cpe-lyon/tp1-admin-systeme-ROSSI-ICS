# Compte Rendu TP1

## Manuel
__1. A l’aide du manuel, identifiez le rôle de la commande which__

Permet d'afficher l'emplacement d'un executable, un binaire dans les dossiers listés dans le $PATH

__2. Quand on consulte cette page, comment peut-on rechercher, par exemple, le mot option ?__

Il faut taper /option qui se tape en bas, comme sur vi

__3. Comment quitte-t-on le manuel ?__

Il faut appuyer sur la touche q

__4. Chaque section du manuel a une première page, qui présente le contenu de la section. Aﬀicher la première page de la section 6; de quoi parle cette section ?__

Intro - introduction to games

Section 6 of the manual describes the games and funny little programs available on the system.

## Navigation dans l’arborescence des fichiers

__1. allez dans le dossier /var/log__

cd /var/log

__2. remontez dans le dossier parent (/var) en utilisant un chemin relatif__

cd ..

__3. retournez dans le dossier personnel__

cd ~

__4. revenez au dossier précédent (/var)__

cd -

__5. essayez d’accéder au dossier /root; que se passe-t-il?__

Accès refusé car un utilisateur simple ne peut pas accéder a un dossier super utilisateur

__6. essayez la commande sudo cd /root; que se passe-t-il? Expliquez__

La commande n'est pas trouver car cd n'est pas un binaire executable mais une comande uniquement disponible dans le bash

__7. à partir de votre dossier personnel, créez l’arborescence suivante :__

### Commande à taper

cd ~
mkdir Dossier1 && touch Dossier1/Fichier1

mkdir -p Dossier2/Dossier2.1

mkdir -p Dossier2/Dossier2.2

cd Dossier2/Dossier2.2 && touch Fichier2 Fichier3

### Résultat :

```
thomas@ubuntu-server:~$ ls -R
.:
Dossier1  Dossier2

./Dossier1:
Fichier1

./Dossier2:
Dossier2.1  Dossier2.2

./Dossier2/Dossier2.1:

./Dossier2/Dossier2.2:
Fichier2  Fichier3
```

__8. revenez dans votre dossier personnel; à l’aide de la commande rm, essayez de supprimer Fichier1, puis Dossier1; que se passe-t-il ?__

cd ~

rm Dossier1/Fichier1

rm Dossier1

```rm: cannot remove 'Dossier1': Is a directory ```

On ne peut pas supprimer de dossier avec la commande rm

__9. quelle commande permet de supprimer un dossier?__

C'est la commande rmdir

__10. que se passe-t-il quand on applique cette commande à Dossier2 ?__

rmdir Dossier2

```rmdir: failed to remove 'Dossier2': Directory not empty```

On ne peut pas supprimer un dossier si celui ci n'est pas vide

__11. comment supprimer en une seule commande Dossier2 et son contenu__


rm -r Dossier2

## Commandes importantes

__1. Quelle commande permet d’aﬀicher l’heure? A quoi sert la commande time ?__

La commande pour afficher l'heure est "date"

La commande time permet de connaitre le temps CPU utilisé d'une commande

__2. Dans votre dossier personnel, tapez successivement les commandes ls puis la; que peut-on en déduire sur les fichiers commençant par un point ?__

Les fichiers commençant par un point sont des fichiers cachés

__3. Où se situe le programme ls ?__

which ls

```/usr/bin/ls```

__4. Que fait la commande ll ?__

ll est un alias de ls -alF donc permet d'afficher dossiers/fichiers cachés avec -a, permet afficher les détails de chaques éléments avec -l et permet d'afficher les indicateurs comme les / par exemple

__5. Quelle commande permet d’aﬀicher les fichiers contenus dans le dossier /bin ?__

ls /bin

__6. Que fait la commande ls ..?__

La commande ls permet de lister le contenu des dossiers

```ls - list directory contents```

__7. Quelle commande donne le chemin complet du dossier courant ?__

Affiche notre dossier courant avec pwd

__8. Que fait la commande echo 'yo' > plop exécutée 2 fois?__

Elle permet d'écrire yo dans le fichier plop

Si quelque chose est déjà dans le fichier, le contenu sera écrasé.

Donc la commande executée deux fois affiche écrit tout simplement le mot yo dans le fichier plop

__9. Que fait la commande echo 'yo' >> plop exécutée 2 fois?__

Elle écrit deux fois le mot yo sur deux lignes

Car l'opérateur >> permet d'ajouter à la fin du fichier quelque chose, dans ce cas yo qui était déjà dans la première ligne

__10. A quoi sert la commande file? Essayez la sur des fichiers de types différents.__

Elle permet de determiné le type de fichier d'un fichier

```
thomas@ubuntu-server:~$ file Dossier1/
Dossier1/: directory

thomas@ubuntu-server:~$ file Dossier1/Fichier1
Dossier1/Fichier1: empty

thomas@ubuntu-server:~$ file /usr/bin/ls
/usr/bin/ls: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=f1f8e6e0a4db23733fc39914a1f1293ce98ce3aa, stripped

thomas@ubuntu-server:~$ file /etc/hostname
/etc/hostname: ASCII text

```

__11. Créez un fichier toto qui contient la chaîne Hello Toto !; créer ensuite un lien titi vers ce fichier avec la commande ln toto titi. Modifiez à présent le contenu de toto et aﬀichez le contenu de titi: qu’observe-t-on? Supprimez le fichier toto; quelle conséquence cela a-t-il sur titi?__

```
thomas@ubuntu-server:~$ echo 'Hello Toto !;' > toto
thomas@ubuntu-server:~$ ln toto titi

thomas@ubuntu-server:~$ echo 'Bonjour Toto !;' > toto
thomas@ubuntu-server:~$ cat titi
Bonjour Toto !;

thomas@ubuntu-server:~$ rm toto
thomas@ubuntu-server:~$ cat titi
Bonjour Toto !;

```

On peut remarquer que lorsque l'on modifie toto, titi est aussi modifier

Si on supprime le fichier toto, le fichier titi existe toujours avec l'ancien contenu de toto



__12. Créez à présent un lien symbolique tutu sur titi avec la commande ln -s titi tutu. Modifiez le contenu de titi; quelle conséquence pour tutu? Et inversement? Supprimez le fichier titi; quelle conséquence cela a-t-il sur tutu?__

```
thomas@ubuntu-server:~$ ln -s titi tutu
thomas@ubuntu-server:~$ echo 'titi modifié' > titi
thomas@ubuntu-server:~$ cat tutu
titi modifié
thomas@ubuntu-server:~$ echo 'tutu modifié' > tutu
thomas@ubuntu-server:~$ cat titi
tutu modifié
thomas@ubuntu-server:~$ rm titi
thomas@ubuntu-server:~$ cat tutu
cat: tutu: No such file or directory
```

Lorsque titi est modifié, tutu aussi change quand on l'affiche avec cat et vice versa

Quand on supprime titi, on ne peut plus afficher tutu car titi a été supprimé.

__13. Affichez à l’écran le fichier /var/log/syslog. Quels raccourcis clavier permettent d’interrompre et
reprendre le défilement à l’écran ?__

CTRL + S pour arreter et CTRL + Q pour reprendre

__14. Affichez les 5 premières lignes du fichier /var/log/syslog, puis les 15 dernières, puis seulement les
lignes 10 à 20.__

cat /var/log/syslog | head -5

Commande head permet d'afficher les premières lignes d'un fichier

cat /var/log/syslog | tail -15

Commande tail permet d'afficher les dernière lignes d'un fichier

cat /var/log/syslog | head -20 | tail -11

Pour afficher 11 lignes de 10 à 20

__15. Que fait la commande dmesg | less ?__

Affiche la première page de /var/log/syslog grâce à la commande less


