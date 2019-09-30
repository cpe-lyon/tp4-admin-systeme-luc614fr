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

j'ai fait la commande `su u1`

10- <b> _Activez le compte de l’utilisateur u1 et vérifiez que vous pouvez désormais vous connecter avec son
compte._ </b>

Pour activer son compte j'ai créer un mot de passe en faisant `passwd u1` 


11- <b> _Quels sont l’uid et le gid de u1 ?_ </b>
id u1
uid=1001(u1) gid=1001(groupe1) groups=1001(groupe1)

# Exercice 2

j'ai fait `which -a ls | tail -1 | xargs dpkg -S` 
Le script bash est le suivant <br> `#!/bin/bash 
echo $(which -a $1 | xargs dpkg -s 2>/dev/null)` 

# Exercice 3
le script bash est le suivant, quand je lance le script il suffit d'écrire la commande 

``` 
!/bin/bash
if [ -z "$1" ]; then
        echo "Non installé."
else
        dpkg -S $(which "$1");
        echo "Installé";
fi
``` 

Réponse cours : `dpkg -l "nom_package" | grep "^ii") && echo "Installé" || echo "Non installé"` 
# Exercice 4 
Pour voir les programmes livré avec coreutils on fait `dpkg -L coreutils | grep "bin"`  ```[``` est l'équivalent de test, on doit donc bien mettre un espace après le crochet.
# Exercice 5

j'ai d'abord installé aptitude en faisant `apt install aptitude` ensuite j'ai chercher le paquet emacs en faisant `/` une fois cela fait j'ai fait `+ g g` et le paquet a été installé 

# Exercice 6. Installation d’un paquet par PPA

2- <b> _Vérifiez qu’un nouveau fichier a été créé dans /etc/apt/sources.list.d. Que contient-il ?_ </b>

un fichier .list et un fichier .save

