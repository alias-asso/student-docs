# [MrPython](http://nohtyprm.github.io/MrPython/install-FR.html)

MrPython est un [IDE](https://fr.wikipedia.org/wiki/Environnement_de_d%C3%A9veloppement) ayant pour objectif l'apprentissage de Python et l'initiation aux bonnes pratiques de programmation.  
Ce logiciel est en général utilisé en première année de cursus informatique.  

Pour télécharger MrPython, vous pouvez télécharger [l'installateur sur le site dédié](http://nohtyprm.github.io/MrPython/install-FR.html). Mais il est aussi préférable de l'installer depuis son [répertoire GitHub](https://github.com/nohtyprm/MrPython), car l'installation est commune à tous les ordinateurs, nous allons voir cette pratique ci-dessous.  

## Installation de git

Premièrement, vous devez être en possession de `git`, la méthode est différente selon vos systèmes d'exploitation...  
> 💡Il est possible que vous connaissiez une site web du nom de [GitHub](https://github.com). Sachez que ces deux outils ne sont pas à confondre:  
Git est un logiciel qui permet entre autre de sauvegarder différentes versions de fichiers dans un repertoire pendant l'évolution d'un projet de programmation.  
GitHub est un service pour stocker sur le cloud un tel repertoire géré par Git.

### Sur Windows

Vous pouvez télécharger `git` sur le [site web officiel](https://git-scm.com/).  

Pendant l'installation, de nombreuses options sont proposées, vous pouvez vous en tenir aux paramètres par défaut, si vous n'êtes pas sûr de ce que vous faites.    
Toutefois, il est recommandé d'essayer de comprendre les options que vous sélectionnez, cela vous permettra de mieux comprendre la logique de `git`.  

⚠️ Faites attention à bien ajouter le logiciel `git` dans le PATH à partir des options d'installations. Cela signifie que git sera un logiciel accessible à partir du terminal, ce qui est fondamental pour la suite, mais aussi pour l'utilisation de git en général. (En effet, `git` est originellement un logiciel de terminal).

### Sur MacOS

Vous pouvez télécharger [Homebrew](https://brew.sh/), un package manager très réputé pour l'environnement MacOS. Nous supposerons d'ailleurs par la suite que vous l'utilisez.  

Après avoir suivi les instructions d'installation disponible sur le site web et attendu que `Homebrew` s'installe, vous pouvez installer `git` via le terminal en utilisant la commande suivante:  
```bash
brew install git
```

### Sur Linux

Utilisez votre package manager courant pour installer `git`, par exemple, sur Ubuntu, vous pouvez utiliser `apt`:

```bash
sudo apt upgrade
sudo apt install git
```

## Installation de Python 3.9

Pour pouvoir coder en Python, et éventuellement utiliser MrPython, vous devez donc posséder [Python](https://www.python.org/). Nous allons voir les différentes étapes pour l'installer sur votre ordinateur.

### Sur Windows

Vous pouvez installer Python sur le [site officiel](https://www.python.org/)   
⚠️**ATTENTION** Installer la version de Python 3.9, et non pas la plus récente. La version 3.9 est la plus courante, mais aussi la dernière version fonctionnelle pour exécuter MrPython.  

### Sur MacOS

En supposant que vous avez installé Homebrew [à l'étape précédente](#sur-macos), nous allons installer Python à partir de celui-ci.  

Pour cela, nous allons exécuter la commande suivante:
```bash
brew install python@3.9
```

### Sur Linux

Installer Python directement à partir de votre package manager. Par exemple pour Ubuntu, vous pouvez utiliser `apt`
```bash
sudo apt upgrade
sudo apt install python3.9
```
## Cloner MrPython

Cloner MrPython ? Et oui, c'est effectivemment le bon terme ! Nous allons cloner le répertoire Git de MrPython disponible sur GitHub sur notre ordinateur et exécuter MrPython directement à partir de son code source !  

Pas de panique, c'est facile, cette fois-ci la démarche est la même pour tous les systèmes d'exploitation ;)  

Nous allons tout d'abord nous mettre dans un repertoire (ou dossier) idéal pour l'installation de MrPython. Prenez n'importe lequel, nous assumerons ici que vous avez choisi le dossier `Documents`

Ouvrez le terminal et utiliser la commande:
```bash
cd Documents
```
Pour vous déplacer dans le repertoire `Documents`.  
Assurez vous que vous êtes bien dans votre dossier personnel, à savoir sur Windows: `C:\Users\NOM`, ou sur Linux/MacOS: `/home/NOM`   

Une fois à l'intérieur nous allons cloner le reprtoire Git disponible sur GitHub. Pour cela utilisons `git` dans le Terminal en exécutant la commande suivante:
```bash
git clone https://github.com/nohtyprm/MrPython.git
```

## Executer MrPython

Une fois fait, un nouveau dossier devrait être créé dans Document: `MrPython-master`.  
Nous allons voir si nous pouvons exécuter MrPython...  

Entrer dans le dossier `MrPython-master` en utilisant la commande `cd`:

- Si vous êtes déjà dans le repertoire Documents sur le terminal: `cd MrPython-master`
- Si vous êtes dans votre dossier personnel: `cd Documents/MrPython-master`

> 💡 Remarquez la syntaxe de la commande `cd`, c'est une commande courante pour manipuler le Terminal. Elle signifie: "Change Directory" et vous y spécifier tujours à côté l'arborescence dans laquelle vous voulez accéder.

Ensuite, exécuter la commande dans le terminal:
```bash
python3.9 mrpython/Application.py
```

Une fenêtre s'affiche ? C'est MrPython, félicitations !

## Post-Installation

MrPython est installé, mais bien difficile d'accès, nous pouvons essayer de simplifier tout ça avec un script.  
Ouvrez un document texte avec votre éditeur favori, ici nous supposons que MrPython a été installé dans votre dossier `Documents` mais vous devez bien évidemmente **adapter** le script pour accéder au programme si ce n'est pas le cas.

Vous pouvez y écrire:
```bash
python3.9 <Chemin d'accès de votre dossier personnel>/Documents/MrPython-master/mrpython/Application.py
```
Remarquez que nous exécutons python3.9 sur le gichier `Application.py` en y indiquant la hiérarchie du chemin d'accès depuis la racine de notre disque dur.

Notez que le chemin d'accès de votre dossier personnel varie selon votre système d'exploitation:
- Sur Windows: `C:\Users\NOM` **ATTENTION** d'ailleurs à utiliser des `\` et non pas des `/` pour les systèmes Windows.
- Sur Linux/MacOS: `/home/NOM`

> ⚠️Pensez à mettre le chemin d'accès entre guillemets si celui-ci contient des dossiers nommés avec des espaces !

Sauvegardez ce fichier sous un format de script, de préférence sur votre Bureau, pour qu'il soit cliquable:

- Sur Windows enregistrez le comme fichier `.bat`
- Sur MacOS/Linux, enregistrez le comme un fichier `.sh`

<u>**NB:**</u> Sur les systèmes Linux/MacOS, vous devrez sans doute rendre ce fichier exécutable en plus: Ouvrez alors le terminal et exécuter la commande `chmod`
```bash
chmod u+x <Chemin d'accès du fichier .sh>
```
Cela aura pour effet de rendre ce script exécutable lorsque vous cliquerez dessus.  

> 💡 Sur Linux, il est possible d'aller plus loins et d'utiliser un `alias` de commande, par exemple, dans votre fichier `.bashrc` que vous retrouverez à la racine de votre dossier personnel vous pouvez y ajouter la ligne suivante:  
`
alias mrpython=python3.9 <Chemin d'accès de votre dossier personnel>/Documents/MrPython-master/mrpython/Application.py
`  
Maintenant, tapez `mrpython` sur votre terminal exécutera cette longue commande directement, super pratique donc !
