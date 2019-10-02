# Exercice 1. Gestion des utilisateurs et des groupes

1- <b> _Commencez par créer deux groupes groupe1 et groupe2_ </b>

`addgroup group2` 


2- <b> _ Créez ensuite 4 utilisateurs u1, u2, u3, u4 avec la commande useradd, en demandant la création de
leur dossier personnel et avec bash pour shell_ </b>

j'ai fait la commande `useradd u1 -m` <br>
j'ai fait la commande `useradd u2 -m` <br>
j'ai fait la commande `useradd u3 -m` <br>
j'ai fait la commande `useradd u4 -m` <br>


3- <b> _Placez les utilisateurs dans les groupes :_ </b>

Voici toute les commandes que j'ai tappé

`usermod -a -G group1 u1` <br>
`usermod -a -G group1 u2` <br>
`usermod -a -G group1 u4` <br>

`usermod -a -G group2 u2` <br>
`usermod -a -G group2 u3` <br>
`usermod -a -G group2 u4` <br>


4- <b> _Donnez deux moyens d’afficher les membres de groupe2_ </b>

j'ai fait `cat /etc/group | grep group2` <br>
Sinon on peut installer le paquet "members" avec `apt get install members` puis il suffit de faire `members group1` ou `members group2`


5- <b> _Faites de groupe1 le groupe propriétaire de /home/u1 et /home/u2 et de groupe2 le groupe propriétaire
de /home/u3 et /home/u4_ </b>

j'ai fait les commandes suivantes : <br>
```
chown u1:group1 /home/u1
chown u1:group1 /home/u2 
chown u1:group2 /home/u3 
chown u1:group2 /home/u4 
``` 

6- <b> _Remplacez le groupe primaire des utilisateurs :_ </b>

J'ai fait les commandes <br>
```
usermod -g group1 u1 
usermod -g group1 u2
usermod -g group2 u3
usermod -g group2 u4
```

7- <b> _Créez deux répertoires /home/groupe1 et /home/groupe2 pour le contenu commun aux groupes, et
mettez en place les permissions permettant aux membres de chaque groupe d’écrire dans le dossier
associé._ </b>

j'ai fait `mkdir /home/groupe1` et `mkdir /home/groupe2`
j'ai fait `chown u1:groupe1 groupe1` et `chown u2:groupe2 groupe2` 
j'ai fait `chmod 720 groupe1 groupe2` 


8- <b> _Comment faire pour que, dans ces dossiers, seul le propriétaire d’un fichier ait le droit de renommer
ou supprimer ce fichier ?_ </b>

j'ai fait `chmod +t /home/group1` et `chmod +t /home/group2`


9- <b> _Pouvez-vous vous connecter en tant que u1 ? Pourquoi ?_ </b>

j'ai fait la commande `su u1`. Je n'arrive pas a me connecter car je n'ai pas de mot de passe 

10- <b> _Activez le compte de l’utilisateur u1 et vérifiez que vous pouvez désormais vous connecter avec son
compte._ </b>

Pour activer son compte j'ai créer un mot de passe en faisant `passwd u1` 


11- <b> _Quels sont l’uid et le gid de u1 ?_ </b>

id u1
uid=1001(u1) gid=1001(groupe1) groups=1001(groupe1)

12- <b> _Quel utilisateur a pour uid 1003 ?_ </b>

j'ai fait la commande `cat /etc/passwd | grep 1003` 


13- <b> _Quel est l’id du groupe groupe1 ?_ </b>

j'ai fait la commande `cat /etc/group | grep group1`  l'id du groupe 1 est donc 1001


14- <b> _Quel groupe a pour gid 1002 ??_ </b>

j'ai fait commande `cat /etc/group | grep 1002` c'est donc le groupe 2 qui a cette gid

15- <b> _Retirez l’utilisateur u3 du groupe groupe2. Que se passe-t-il ? Expliquez._ </b>

j'ai fait la commande gpasswd -d u3 groupe2. <br>
u3 n'est plus dans le groupe 2 et ne peux donc plus modifier ou acceder au dossier /home/groupe2 . 

16- <b> _Modifiez le compte de u4_ </b>

``` 
usermod --expiredate 06/01/2019 u4 
sudo chage -M 90 u4
sudo chage -m 5 u4
sudo chage -W 14 u4
sudo chage -I 30 u4

``` 

17- <b> _Quel est l’interpréteur de commandes (Shell) de l’utilisateur root ?_ </b>

L'interpréteur de commandes de l'utilisateur est /bin/bash j'ai fait `echo $SHELL` 

18- <b> _à quoi correspond l’utilisateur nobody ?_ </b>

nobody est le nom conventionnel d'un compte d'utilisateur à qui aucun fichier n'appartient, qui n'est dans aucun groupe qui a des privilèges et dont les seules possibilités sont celles que tous les "autres utilisateurs" ont.

19- <b> _Par défaut, combien de temps la commande sudo conserve-t-elle votre mot de passe en mémoire ?
Quelle commande permet de forcer sudo à oublier votre mot de passe ?_ </b>

Le temps par défaut est 15 minute. <br>
la commande pour forcer sudo à oublier son mot de passe est `sudo -k` 

# Exercice 2. Gestion des permissions

1- <b> _Dans votre $HOME, créez un dossier test, et dans ce dossier un fichier fichier contenant quelques
lignes de texte. Quels sont les droits sur test et fichier_ </b>

cd /home/user
mkdir test 
cd test 
nano fichier 

les droits du dossier test sont 755 (droits de base pour un dossier sous linux) et les droits du fichier sont 644 (droits de base pour un fichier sous linux)

2- <b> _Retirez tous les droits sur ce fichier (même pour vous), puis essayez de le modifier et de l’afficher en
tant que root. Conclusion ?_ </b>

j'ai fait `chmod 000 fichier`. J'arrive à le modifier car je suis en root 


3- <b> _Redonnez vous les droits en écriture et exécution sur fichier puis exécutez la commande echo "echo
Hello" > fichier. On a vu lors des TP précédents que cette commande remplace le contenu d’un
fichier s’il existe déjà. Que peut-on dire au sujet des droits ?_ </b>

j'ai fait `chmod 300 fichier | echo "echo hello world" > fichier`. On peut écrire dans le fichier 

4- <b> _Essayez d’exécuter le fichier. Est-ce que cela fonctionne ? Et avec sudo ? Expliquez._ </b>

ça ne va pas marcher car on a pas les droits d'execution. Cependant en Root ça va marcher

5- <b> _Placez-vous dans le répertoire test, et retirez-vous le droit en lecture pour ce répertoire. Listez le
contenu du répertoire, puis exécutez ou affichez le contenu du fichier fichier. Qu’en déduisez-vous ?
Rétablissez le droit en lecture sur test_ </b>
```
sudo chmod u-r ../test
ls 
cannot open directory '.': Permission denied
./fichier 
bash: ./fichier: Permission denied
``` 
ça ne va pas marcher car on a plus les droits d'execution. 

6- <b> _Créez dans test un fichier nouveau ainsi qu’un répertoire sstest. Retirez au fichier nouveau et au
répertoire test le droit en écriture. Tentez de modifier le fichier nouveau. Rétablissez ensuite le droit
en écriture au répertoire test. Tentez de modifier le fichier nouveau, puis de le supprimer. Que pouvez-
vous déduire de toutes ces manipulations ?_ </b>

```
nano nouveau
mkdir sstest
chmod u-w nouveau
chmod u-w ../test
nano nouveau
[ Error writing nouveau: Permission denied ]
chmod u+w ../test
nano nouveau
[ Error writing nouveau: Permission denied ] 
rm nouveau
rm: remove write-protected regular file 'nouveau'? yes
ls fichier  sstest
``` 

On en déduit qu'il n'y pas d'héritage des droits pour les fichiers situé dans les répertoires 


7- <b> _Positionnez vous dans votre répertoire personnel, puis retirez le droit en exécution du répertoire test.
Tentez de créer, supprimer, ou modifier un fichier dans le répertoire test, de vous y déplacer, d’en
lister le contenu, etc...Qu’en déduisez vous quant au sens du droit en exécution pour les répertoires ?_ </b>

``` 
chmod u-x test
 nano test/nouveau
[ Path 'test' is not accessible ]
 cd test/
-bash: cd: test/: Permission denied
ls test
ls: cannot access 'test/sstest': Permission denied
ls: cannot access 'test/fichier': Permission denied
fichier  sstest
``` 

On ne peut rien faire car on a pas les droits.


8- <b> _Rétablissez le droit en exécution du répertoire test. Positionnez vous dans ce répertoire et retirez lui
à nouveau le droit d’exécution. Essayez de créer, supprimer et modifier un fichier dans le répertoire
test, de vous déplacer dans ssrep, de lister son contenu. Qu’en concluez-vous quant à l’influence des
droits que l’on possède sur le répertoire courant ? Peut-on retourner dans le répertoire parent avec ”cd
..” ? Pouvez-vous donner une explication ?_ </b>


j'ai fait la commande `chmod 640 test` 


9- <b> _Rétablissez le droit en exécution du répertoire test. Attribuez au fichier fichier les droits suffisants
pour qu’une autre personne de votre groupe puisse y accéder en lecture, mais pas en écriture._ </b>

j'ai fait la commande `umask 022 test` 

10- <b> _Définissez un umask très restrictif qui interdit à quiconque à part vous l’accès en lecture ou en écriture,
ainsi que la traversée de vos répertoires. Testez sur un nouveau fichier et un nouveau répertoire._ </b>

j'ai fait la commande `umask 037 test` 

11- <b> _Définissez un umask très permissif qui autorise tout le monde à lire vos fichiers et traverser vos réper-
toires, mais n’autorise que vous à écrire. Testez sur un nouveau fichier et un nouveau répertoire._ </b>



12- <b> _Définissez un umask équilibré qui vous autorise un accès complet et autorise un accès en lecture aux
membres de votre groupe. Testez sur un nouveau fichier et un nouveau répertoire._ </b>


13- <b> _Transcrivez les commandes suivantes de la notation classique à la notation octale ou vice-versa (vous
pourrez vous aider de la commande stat pour valider vos réponses)_ </b>

j'ai fait la commande `chmod u=rx,g=wx,o=r fic = chmod 534 -r-x--wx-r--` <br>
j'ai fait la commande `chmod uo+w,g-rx fic = chmod 706 -rwx-x-rw-`

14- <b> _Affichez les droits sur le programme passwd. Que remarquez-vous ? En affichant les droits du fichier
/etc/passwd, pouvez-vous justifier les permissions sur le programme passwd ?_ </b>



