# Bash
[Unix Game, pour apprendre les commandes bash en résolvant des énigmes](https://www.unixgame.io/unix50)
## Introduction
En bash, les commandes ont toutes une structure simple:  
`cmd <arguments> -o <paramètre> --option <paramètre>`  

Ici on a exécuter la commande `cmd` qui peut avoir une option `-o`, cette option prend un paramètre `<paramètre>`  
On a aussi utiliser l'option `--option` qui prend aussi un `<paramètre>` sauf qu'on a utilisé 2 tirets puisque l'option qu'on a utilisé est un mot complet.

## Commandes de bases et arborescence

### Le fonctionnement de l'arborescence UNIX (Linux)

Un chemin est une succession de répertoires séparés par / (e.g. rep1/rep2/rep3), dont l'origine peut être:  
— `<rien>` : le répertoire courant par défaut  
— `./`     : le répertoire courant  
— `../`    : le répertoire parent du répertoire courant  
— `/`      : la racine du système, on parle alors de chemin absolu  
— `~/`     : votre Home, le dossier de départ de toute session bash  

### Contrôle de l'arborescence

- `cd <directory>` (change directory) : va dans le `<directory>` indiqué
- `mkdir <directory>` (make directory) : créer un dossier
**Paramètre**: `-p` : créer les dossiers parents de l'arborescence donnée s'il n'existe pas. (Pour créer une arborescence en une commande)
**Exemple :** 
Si le dossier /parent n'existe pas et que vous lancez la commande : `mkdir -p ./parent/enfant` cela va créer le dossier `/parent` et le dossier `/enfant`

- `rmdir <directory>` (remove directory): destruction du dossier (pas de corbeille !)
- `touch <file>` : créer le fichier file dans le répertoire courant, s'il existe, la commande changera juste la date d'édition du fichier pour maintenant
- `cp <source> <destination>` (copy): copie la `<source>` dans la `<destination>`
***
- `rm <file>` (remove): supprime le fichier `<file>`  

**Paramètres:**  
- `-r` (recursive): Surpprimera le dossier passer en option (comme `rmdir`) !
- `-rf` (recursive force) : force la suppression
- `-i`: demande à l'utilisateur de confirmer l'effacement de chaque fichier. Si la réponse ne commence pas par `y' ou `Y', le fichier est ignoré. Si les options -f et -i sont fournies simultanément, la dernière sur la ligne de commandes a l'avantage.
***
**Deux en un**, la commande `mv`!  

- `mv <source> <target>/` (move): déplace le dossier ou répertoire `<source>` vers le dossier `<target>/`
- `mv <old_name> <new_name>`: renomme le fichier <old_name> vers <new_name>
***
`ls` (liste): liste des fichiers et répertoires du répertoire courant   

**Paramètres:**  
- `-a` (all): affiche tous les fichiers et répertoires cachés ou non 
- `-l` (list): affiche ls dans une liste indiquant également les permission et la date de création des fichiers
***

#### Permissions (chmod)
Chaque dossier et fichier dispose d'une permission qui peut s'écrire `rwxrwxrwx` et s'accompagne d'un `d` devant pour indiquer que c'est un dossier 
Où le premier triplet correspond aux permissions du propriétaire du fichier (l'entité `u` pour _user_), le second au groupe du propriétaire (l'entité `g` pour _groupe_) et le troisième à tous les autres utilisateurs du système (l'entité `o` pour _others_).  
Ces lettres correspondent à:  
- `r` _(read)_: le droit de lecture sur un fichier/dossier
- `w` _(write)_: le droit d'écriture
- `x` _(eXecute)_: le droit d'exécution

On peut changer ces permissions grâce à la commande `chmod`:  
- `chmod <entités>+<permissions> <fichier>` : permet à celui qui possède le fichier de gérer les droits sur celui-ci
**Exemple :**
`chmod u+rx file` : donne la permission de lecture d'exécution à l'utilisateur sur le fichier `file`
***

`echo <text>` : permet d'afficher ce qui lui est donné en paramètre 
- `-n` : empêche le retour à la ligne

*** 

## Encore plus de modularité !

Sachez que vous pouvez rendre un peu plus complexe vos commandes pour affiner le résultats et avoir moins de travail à faire !

### Redirection de flux 
En Bash et dans les autres langages de programmations, il existe des canaux de communications ! Il s'agit de partage explicite d'information. 
Il y a 3 flux standards : `stdin` (clavier = entrée standard), `stdout` (écran = sortie standard), `stderr` (erreur = sortie standard partagée avec stdout). 

Par exemple, quand vous allez exécuter la commande `echo` celle-ci affichera ce qui lui est passé en paramètre sur sa sortie standard (écran du terminal). 
Et si on veut écrire/lire sur un autre flux alors ? C'est ainsi qu'intervient la redirection de flux, on va demander explicitement à l'interpréteur Bash de rediriger l'information ailleurs. Ci-dessous la syntaxe à appliquer : 

- `cmd > fichier`   : la commande écrira dans le fichier __en l’écrasant s’il existe__ ; 
- `cmd >> fichier`  : la commande écrira __à la fin du fichier__ en le créant si nécessaire ;
- `cmd 2> fichier`  : la commande écrira ses erreurs dans le fichier __en l’écrasant s’il existe__ ;
- `cmd 2>> fichier` : la commande écrira ses erreurs __à la fin du fichier__ en le créant si nécessaire ;
- `cmd < fichier`   : la commande ne lira pas sur le clavier, mais dans le fichier.  

__NB :__ Le 2 dans `2>` et `2>>` correspond à l'indice du `stderr` dans la table des descripteurs. 


### Lancer des commandes simultanément  
Il est possible d'écrire une infinité de commande sur la même ligne si on le voulait, voici le schéma à suivre : 
- `A ; B` 	: exécute A puis exécute B
- `A && B` 	: exécute B si A est vraie 
- `A || B` 	: exécute B si A est faux
- `A &` 	: exécute A en arrière-plan

## Automatisation avec les scripts !

Dans un script shell, nous allons faire appelle à de nouveaux éléments nécéssaire pour pouvoir automatiser des actions avec la plus grande liberté possible...

- `#!` dit shebang, se met en tête de fichier et indique à l'exécution où exécuter les lignes de commandes qui suivent.
- `#` est le caractère croisillon (caractère d’échappement pour les commentaires). 
- `$` permet d'accéder à la valeur d’une variable, quelques exemples d'utilisation ([parameter expansion](https://wiki.bash-hackers.org/syntax/pe)) : 
   - `$var` /  `${var}` : accède à la valeur de la variable var 
   - `${#var}`	    : compte le nombre de caractère, peut compter la chaîne de fin si la chaîne de caractère est mise entre guillemets
   - `${var^^}`       : transforme tous les caractères en leur analogue majuscule 
   - `$$`             : valeur du PID 
   - `$!`             : stocke le PID de la dernière commande lancé
   - `$?`             : stocke la valeur de l'avant dernière commande lancé (donc celle qui l'a précède) 

__NB :__ Si le shebang figure ailleurs qu'en début de fichier, il sera pris pour un simple commentaire. 

### Structure de contrôles 
À noter quand Bash les espaces sont très sensible donc n'oubliez pas de mettre des espaces entre la condition. 

#### Les conditions 
```bash
if [ conditions ]; then
   instructions
elif [ autre conditions ]; then
   instructions
else 
   instructions 
fi
```

Une forme condensée : 
`[ condition ]` $\Leftrightarrow$ `[[ condition ]]` $\Leftrightarrow$ test condition : 
- renvoie 0 si le test est vrai 
- renvoie une valeur non nulle sinon

Par exemple pour vérifier qu'il y ait bien un paramètre à l'exécution de la commande : 
`[ $# -ne 2 ] && echo "Usage : $0 <param1> <param2>" && exit 1` 

### Les boucles 
```bash
while [ conditions ]; do
   instructions
done
```

```bash
for i in {debut..fin..pas}; do
   instructions
done
```


