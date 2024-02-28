# Après le don de PC

Les PC que nous donnons possèdent la distribution Linux [OpenSUSE Leap](https://get.opensuse.org/leap/), avec le gestionnaire de bureau [KDE Plasma](https://kde.org/fr/plasma-desktop/).

## Premier démarrage

Pour vous connecter la première fois, le compte utilisateur s'appelle `user`, et le mot de passe est `password`. Il est important d'immédiatement modifier ce mot de passe en se rendant dans les **paramètres systèmes** (que vous trouverez en cherchant dans la liste des applications, de la même manière que sous Windows), puis dans `Utilisateurs`. Vous pourrez également changer le nom d'utilisateur.

Linux fonctionne avec un compte administrateur appelé `root`. Vous devez changer le mot de passe de ce compte qui est également `password` par défaut. Pour cela, ouvrez un terminal (l'application `Konsole`), et entrez la commande suivante :

```sh
sudo passwd root
```

On vous demandera alors le mot de passe actuel du compte `root`, puis le nouveau mot de passe.

> ℹ️ Quand on vous demande d'entrer votre mot de passe dans le terminal, il est normal que vous ne voyiez pas les caractères que vous tapez au clavier, c'est un mécanisme de protection de linux, pour éviter qu'une personne devine la longueur de votre mot de passe en regardant votre écran derrière vous.

## Maintenance du système

Après avoir connecté votre ordinateur à internet, vous pouvez mettre à jour le système en entrant la commande :

```sh
sudo zypper update
```

Vous pouvez également installer un package avec la commande :

```sh
sudo zypper install [nom du package]
```

Pour chercher dans la liste des packages disponibles, vous pouvez aller sur [le site d'opensuse](https://software.opensuse.org/). La plupart des logiciels nécessaires pour la licence d'informatique sont directement disponible sur les dépots d'OpenSUSE, et installables avec la commande `zypper`. Si ce n'est pas le cas, le site du logiciel vous indiquera les étapes à suivre pour l'installer.

> ☝️🤓 Un package est un ensemble de fichiers qui doivent être installé sur le système. La plupart du temps, c'est un programme mais cela peut être n'importe quoi d'autre comme par exemple un thème de couleur, une police d'écriture... Chaque distribution linux stocke ses packages dans des serveurs appelés **dépots** qui sont hébergés partout dans le monde par des personnes volontaires (Jussieu possède d'ailleurs [ses dépots](https://distrib-coffee.ipsl.jussieu.fr/)), et possède un **package manager** permettant d'installer les packages. C'est les différents packages disponibles et les packages installés par défaut qui différencient chaque distribution Linux. 
