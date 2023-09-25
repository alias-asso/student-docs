# Installer la lib Cini

## Introduction
*Cini* est une bibliothèque graphique simplifiée pour le C, vous permettant de comprendre les fondamentaux graphiques d'une bibliothèque plus avancée: *SDL2* dont *Cini* dépend    

⚠️ **Prérequis**: 
1. Ce tutoriel est dédié aux utilisateurs de machines ayant un fonctionnement basé sur UNIX dont MacOS, Linux ou Windows avec WSL. 
Pour les utilisateurs Windows n'ayant pas WSL, [apprenez comment l'installer ici](env_c.md#le-wsl-pour-windows)  

2. Nous admetterons qu'un environnement de programmation C a été configuré sur votre machine. Si ce n'est pas le cas, [apprenez comment le faire facilement sur cet article](env_c.md).
   
3. Vous devez maîtriser les fondamentaux de Bash, vous pourrez en apprendre plus sur les commandes de bases [avec cet article](bash.md)

## Cloner le repo git

Vous devez disposer de l'application git sur votre machine.  

### Pour MacOS
Si vous ne disposez pas d'un package manager, vous pouvez l'installer directement [via le site officiel](https://git-scm.com/).  

Si au contraire vous en avez un, n'hésitez pas à l'utiliser pour installer git.  
Par exemple avec HomeBrew, vous pouvez utiliser la commande:
```zsh
brew install git
```

### Pour WSL et Linux
Installez git avec le package de manager de votre distribution.  
Par exemple, pour Ubuntu ce sera:
```bash
sudo apt install git
```

### Et après...

Une fois que vous disposez de git, vous pouvez cloner [le répertoire Github de Cini](https://github.com/wegank/libcini).
Le mieux est de le faire dans un nouveau dossier `local` à la racine de votre dossier HOME `~`:
```bash
mkdir local
cd local
git clone https://github.com/wegank/libcini
``` 

⚠️ **NB** N'utilisez pas ce fichier comme stockage personnel, il vous servira notamment à installer les dépendances d'autres langages de programmation, alors il est important de le laisser tel quel

Une fois le téléchargement terminé, vous devriez avoir un nouveau dossier nommé `libcini` dans le dossier `local`, faites `ls` pour le constater !

## Installer CMake pour le compiler

Bien qu'on aurait pu se passer de compiler le code de *Cini* depuis sa source, il est toujours mieux de le faire soit même quand on en a l'occasion pour en comprendre la logique.  

Ainsi, afin de mener à bien la compilation de *Cini* nous avons besoin de *CMake*

### Pour MacOS

Vous pouvez [télécharger CMake depuis le site officiel](https://cmake.org/)...  
...Ou bien utiliser un package manager tel qu'HomeBrew:
```zsh
brew install cmake
```

### Pour WSL et Linux
Installez CMake à partir de votre gestionnaire de paquet.  
Par exemple pour Ubuntu:
```bash
sudo apt install cmake
```
## Installer les dépendances de Cini

Pour fonctionner, *Cini* va avoir besoin des bibliothèques *SDL2*. Pas de panique ! l'installation se fera plus rapidement que pour *Cini* !

### Pour MacOS

Vous devez vous procurer un package manager tel qu'[HomeBrew](https://brew.sh/index_fr) pour installer efficacement cette nouvelle librairie.

Grâce à *HomeBrew*, vous serez en mesure d'installer rapidement différents outils pratiques pour la programmation en une ligne de commande dans le terminal.  

Une fois fait, vous pouvez exécuter les commandes suivantes:
```zsh
brew install sdl2
brew install sld2_ttf
```

### Pour Linux et WSL

Avant d'installer un package, n'oubliez pas de mettre à jour votre système pour avoir les derenières versions compatibles.  
Pour ubuntu par exemple:
```bash
sudo apt update
sudo apt upgrade
```

Utilisez le package manager de votre distribution pour vos procurer SDL2.  
Par exemple, pour Ubuntu.
```bash
sudo apt install libsdl2-dev
sudo apt install libsdl2-ttf-dev
```

## Compiler Cini

Afin de pouvoir compiler *Cini* il faut que vous retourniez sur le repertoire `~/local/libcini/` que vous avez obtenu en [clonant le repo Github](#cloner-le-repo-git).  
A l'aide de la commande `cd` placez vous à l'intérieur et exécutez:
```bash
mkdir build
cd build
cmake ..
cpack ..
```

Une fois fait, Cini devrait être compilé. Pour autant vous ne pourrez pas encore l'utiliser...

## Ajouter Cini à C

Finalement, vous devrez modifier quelques variables afin d'avoir Cini de disponible pour vos programmes C

### Pour Linux et WSL

Le processus est simple. Si vous n'avez pas agit sur le shell, vous devrez modifier votre fichier `~/.bashrc`.  
Le code à l'intérieur de ce fichier s'exécutera à chaque fois que vous ouvrirez le terminal.  

💡 Vous remarquerez que ce fichier se trouve **à la racine de votre repertoire HOME**: `~` et que ce **fichier est caché** car il commence par un `.`

> *Pour les utilisateurs ayant modifié leur shell, un fichier avec un nom similaire devrait se trouver à la racine de votre répertoire HOME `~`. Normalement nommé `.<nom_du_shell>rc`  
> Par exemple, si vous utilisez `zsh`, le nom de ce fichier sera `.zshrc`*

Vous pouvez modifier rapidement ce fichier avec le logiciel `nano` qui est un éditeur de texte à l'intérieur du terminal.

```bash
nano ~/.bashrc
``` 

Une fois à l'intérieur, allez à la toute fin puis copiez collez ce code (avec clique droit sur le terminal):  
💡 Vous pouvez vous déplacer à l'aide des flèches sur votre clavier !
```bash
# On ajoute Cini à l'include de C pour éviter l'erreur de compilation
export C_INCLUDE_PATH=$HOME/local/libcini/include/:$C_INCLUDE_PATH
# On ajoute la possibilité d'utiliser -lcini et donc d'utiliser la librairie cini à la compilation
export LIBRARY_PATH=$HOME/local/libcini/build/src/:$LIBRARY_PATH
# On ajoute Cini au gestionnaire de librairie LD
export LD_LIBRARY_PATH=$HOME/local/libcini/build/src/:$LD_LIBRARY_PATH
```

Si vous êtiez sur `nano`, appuyez sur `CTRL+X` pour fermer le fichier et sauvegardez en appuyant sur `Y` puis `Entrée`  
💡 Comme vous avez pu probablement le constater: le caractère `^` sert à indiquer la pression de la touche `CTRL`. Vous serez amener à rencontrer cette notation plus tard !

⚠️**NB:** Si vous avez mis le fichier de *libicini* autre part que dans le dossier `~/local/` veillez à bien modifier le chemin d'accès spécifié pour correspondre à votre arborecence. (on a `$HOME=/home/<nom_utilisateur>/`)

Vous pouvez exécuter la commande suivante pour appliquer les changements immédiatement:
```bash
source ~/.bashrc
```

### Pour MacOS

D'après [ce post de StackOverflow](https://stackoverflow.com/questions/6442364/running-script-upon-login-in-mac-os-x)

Vous devez vous rendre dans l'application `Automator.app`  
Ensuite vous devez ajouter un nouveau script shell dans `Application > Librairies > Ajouter un script shell`  

Vous pouvez ensuite copier coller le code ci dessous
```bash
# On ajoute Cini à l'include de C pour éviter l'erreur de compilation
export C_INCLUDE_PATH=$HOME/local/libcini/include/:$C_INCLUDE_PATH
# On ajoute la possibilité d'utiliser -lcini et donc d'utiliser la librairie cini à la compilation
export LIBRARY_PATH=$HOME/local/libcini/build/src/:$LIBRARY_PATH
# On ajoute Cini au gestionnaire de librairie LD
export LD_LIBRARY_PATH=$HOME/local/libcini/build/src/:$LD_LIBRARY_PATH
```

Sauvegardez ceci sous le format Application dans le repertoire de votre choix. Le mieux est de le conserver dans un dossier fixé que vous ne risquez pas de supprimer.  

Rendez-vous ensuite dans les *Paramètres*, puis dans *Utilisateurs et groupes* (ou *Comptes*), et enfin cliquez sur *Exécuter au démarrage*. Vous n'avez plus qu'à ajouter l'Application précédemment créée !

## Vérifiez que tout fonctionne !

Si tout se passe bien, vous serez en mesure d'utiliser *Cini* sur votre machine ! Pour vous en convaincre, vous pouvez copier le code du fichier Exemple de *Cini* disponible [sur le répertoire GitHub](https://github.com/wegank/libcini/blob/master/examples/hello.c):
```c
#include <cini.h>

int main() {
    CINI_print_string("Test\n");
    CINI_open_window(250, 100, "Test");
    CINI_fill_window("white");
    CINI_draw_disc(125, 50, 38, "red");
    CINI_draw_string(12, 30, "black", "Cini vous dit bonjour !" );
    CINI_loop();
    return 0;
}
```

Compilez le à l'aide de gcc avec  
```bash
gcc hello.c -o hello.out -lcini
```

Puis exécutez le avec
```bash
./hello.out
```

Alors ? Voyez-vous apparaître la fenêtre à l'écran ? ;)
