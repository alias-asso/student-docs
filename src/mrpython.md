# MrPython

MrPython est un [IDE](https://fr.wikipedia.org/wiki/Environnement_de_d%C3%A9veloppement) ayant pour objectif l'apprentissage de Python et l'initiation aux bonnes pratiques de programmation. Ce logiciel est généralement utilisé au premier semestre du cycle d'intégration.  

Pour télécharger MrPython, vous pouvez télécharger [l'installateur sur le site dédié](http://nohtyprm.github.io/MrPython/install-FR.html).

Ce document est un tutoriel, ayant pour but d'expliquer étape par étape comment installer et lancer MrPython sur votre machine.

## 1. (macOS et Linux) Installer Python

Tout d'abord, ouvrez un terminal.

- **Sur Windows :** tapez `cmd`  dans la barre de recherche Windows et ouvrez l'app. Tapez `python --version` puis faites Entrer (attention aux deux tirets).
- **Sur macOS et Linux :** sur macOS, cherchez l'application intitulée *Terminal* parmi celles installées. Sur Linux, on supposera que vous savez ouvrir un terminal. Tapez `python3 --version` puis faites Entrer (attention aux deux tirets).

Si vous obtenez un message du style `Python 3.12.5`, alors Python est déjà installé et vous pouvez passer à l'étape 2. **Si votre version est inférieure à 3.12.5**, désinstallez Python ([tutoriel Windows](https://support.microsoft.com/en-us/windows/uninstall-or-remove-apps-and-programs-in-windows-4b55f974-2cc6-2d2b-d092-5905080eaf98), [tutoriel macOS](https://support.apple.com/en-us/102610)) et poursuivez avec la suite de l'installation.

Rendez-vous sur [le site officiel de Python, section Téléchargements](https://www.python.org/downloads/) et installez la dernière version. **Assurez-vous de choisir une version ultérieure ou égale à 3.12.5 !**

> ⚠️ Attention ! Vérifiez bien que vous êtes sur le site officiel de Python : python.org dans la barre de recherche.

## 2. Installer MrPython

Rendez-vous sur [le site de MrPython](https://nohtyprm.github.io/MrPython/install-FR.html).

* **Sur Windows**, la vie est bien faite : un installateur est mis à disposition, qui ne nécessite même pas d'installer Python. Rendez-vous dans la [section "Installation sous Windows (installateur)"](https://nohtyprm.github.io/MrPython/install-FR.html#installation-sous-windows-installateur) et téléchargez puis installez le fichier `.exe`. Si votre navigateur se plaint que le fichier n'est pas sûr, cliquez sur les trois petits points > "Conserver" > "Afficher plus" > "Garder quand même". Lors de l'installation, pensez à cocher la case "Créer une icône sur le bureau".
* **Sur macOS :** rendez-vous dans [la section "Installation sous MacOS (Installation manuelle)" Étape 2](https://nohtyprm.github.io/MrPython/install-FR.html#etape-2--r%C3%A9cup%C3%A9ration-des-sources-de-mrpython-1) et ouvrez le lien avec les sources de MrPython : https://github.com/nohtyprm/MrPython/archive/master.zip. Extrayez le fichier `.zip` ainsi téléchargé en cliquant dessus (attention à bien placer le `.zip` dans les Téléchargements).
  * Puis ouvrez le terminal ;
  * Tapez la commande `cd Downloads/MrPython-master` et validez avec Entrer (acceptez l'accès au dossier si on vous le demande)  ;
    * Tapez la commande `bash mrpython.sh`, **en n'oubliant pas le `.sh` à la fin** ;
  * Normalement, l'interface s'ouvre.
* **Sur Linux :** mêmes instructions que sur Mac, mais adaptées à votre système (que ce soit au niveau de la décompression, ou de l'endroit où vous avez téléchargé les sources).

> 💡Sur Mac et Linux, appuyer sur la touche Tab (tabulation, qui se trouve juste au-dessus de Verrouiller majuscules) permet d'autocompléter les dossiers et fichiers. Ca permet d'écrire beaucoup plus vite !

## 3. Lancer MrPython à l'avenir

* Sur Windows, normalement, l'installateur aura placé une icône sur votre bureau. Si elle n'existe pas, vous pouvez utiliser la recherche Windows pour trouver MrPython.
* Sur macOS et Linux, il faudra à chaque fois :
  1. Lancer le terminal ;
  2. Vous rendre dans le répertoire qui contient MrPython (avec la commande `cd Downloads/MrPython-master`) ;
  3. Lancer le programme avec `bash mrpython.sh`, toujours sans oublier le `.sh` à la fin.

## 4. Pour aller plus loin (optionnel, fortement recommandé)

* Nous recommandons d'installer Python, via leur site officiel, même si vous utilisez Windows et que ce n'est pas nécessaire pour vous. C'est un langage extrêmement utile et vous serez très certainement amenés à l'utiliser durant vos études et votre vie active, même si vous ne poursuivez pas en informatique.

* Sur macOS, nous vous invitons à consulter le site de [Homebrew](https://brew.sh/), un gestionnaire de paquets (comprenez une sorte de App Store) qui se gère depuis le terminal. C'est un couteau-suisse extrêmement utile et vous en aurez besoin tôt ou tard.

* Sur Windows [il existe un équivalent à Homebrew appelé WinGet](https://learn.microsoft.com/fr-fr/windows/package-manager/winget/). C'est un programme officiel de Microsoft ; pour les mêmes raisons que pour Homebrew, nous vous recommandons fortement de l'utiliser.

