# Logisim 

Logisim est le logiciel servant à créer des réseaux logiques. Il permet de représenter visuellement des circuits sur ordinateur tout en les rendant interactifs.

Nous vous proposons d'installer une version plus à jour de Logisim que celle utilisée sur les ordinateurs de la PPTI. Cela aura pour principal effet d'avoir un logiciel plus stable et plus joli (yay :D). Cette version s'appelle Logisim-evolution et est maintenu par de nombreuses universités suisses.

Normalement, ce tutoriel fonctionne sur tous les systèmes d'exploitation, que ça soit Windows, MacOS ou n'importe quelle distribution Linux.

## Linux

Logisim-evolution est disponible sur Flatpak (via le Flathub) et sur Snap. Vous pouvez l'installer avec
```bash
flatpak install flathub com.github.reds.LogisimEvolution
```
si vous utilisez Flatpak (comme avec Fedora ou Linux Mint) ou avec
```bash
snap install logisim-evolution
```
si vous utilisez Snap (comme avec Ubuntu).

Si vous utilisez Arch Linux (comme moi, btw), vous pouvez directement build le logiciel sur votre ordinateur depuis le [paquet AUR](https://aur.archlinux.org/packages/logisim-evolution) (la version binaire n'est plus maintenue). Si vous avez une autre version de Java installé, exécuter `archlinux-java set java-21-openjdk` pour bien utiliser Java 21 !

Si aucune de ces solutions ne vous convient, vous pouvez télécharger le fichier `.deb` ou `.rpm` [depuis Github](https://github.com/logisim-evolution/logisim-evolution/releases/latest). Si vous utilisez une distribution Linux n'utilisant pas le format deb ou rpm, sautez à la section ["Autre"](#autre).

## Windows

Logisim-evolution est facilement installable sur Windows à l'aide d'un installateur. Il est disponible [sur GitHub](https://github.com/logisim-evolution/logisim-evolution/releases/latest) : il suffit de télécharger le fichier finissant par `amd64.msi` et de l'exécuter. Si cette version ne fonctionne pas, sautez à la section ["Autre"](#autre).

## Mac

Logisim-evolution est disponible via Homebrew. Vous pouvez l'installer avec
```zsh
brew install --cask logisim-evolution
```

Sinon, vous pouvez télécharger le fichier [sur GitHub](https://github.com/logisim-evolution/logisim-evolution/releases/latest) finissant par `aarch64.dmg` si vous avez une puce Apple (e.g., M1, M2...) ou finissant par `x86_64.dmg` si vous avez une puce Intel (e.g., i5, i7...). Dans la documentation de Logisim-evolution, il est aussi écrit :
> **Note for macOS users**: The Logisim-evolution.app is not signed with an Apple approved certificate.
>
> When launching the application for the first time, you will have to start it via the "Open" entry in the application icon's context menu in the macOS Finder. This is either done by clicking the application icon with the right mouse button or holding down CTRL while clicking the icon with the left mouse button. This will open a panel asking you to verify that you wish to launch the application. On more recent versions of macOS, the panel will only give you a choice of moving the app to the trash or Cancel. On those systems, click Cancel, open System Preferences, and select Security & Privacy. There you may need to click the lock to make changes and authenticate with an administrative acccount. It should show an option to open the app. See [Safely open apps on your Mac](https://support.apple.com/en-us/HT202491) for more information.
>
> Depending on your security settings, you may also get a panel asking if you wish to allow it to accept network connections. You can click "Deny" as we do not need network access currently nor we do request any.

N'utilisant moi-même pas un Mac, je ne peux pas vous donner plus d'informations. Si vous avez besoin d'aide, n'hésitez pas à rejoindre [notre Discord](https://discord.gg/Qq6u8Mz) et si vous avez plus d'information que moi à ce sujet, n'hésitez pas à compléter la doc [en ouvrant une PR](https://github.com/alias-asso/student-docs/) :D

Si cette version ne fonctionne pas, sautez à la section ["Autre"](#autre).

## Autre

Logisim-evolution est une application compilée avec Java 21 (ou une version plus récente). Vous pouvez la télécharger et l'installer depuis [le site d'Oracle](https://www.oracle.com/java/technologies/downloads/#java21) si vous êtes sur Windows ou Mac, ou depuis votre package manager si vous êtes sous Linux (rechercher un paquet qui s'appelle `jdk21-openjdk` ou `java-21-openjdk` ou `openjdk-21-jre`).

Si vous utilisez [Mars](./mars.md), nous vous recommandons fortement de lire la section ["Utiliser une autre version de Java"](./mars.md#utiliser-une-autre-version-de-java).

Vous pouvez ensuite télécharger le fichier finissant par `all.jar` [depuis GitHub](https://github.com/logisim-evolution/logisim-evolution/releases/latest). Pour le lancer, il suffit de double cliquer dessus ou d'exécuter la commande
```bash
java -jar logisim-evolution-4.0.0-all.jar
```
Cette commande présuppose que vous êtes dans le même dossier que Logisim-evolution et que le fichier s'appelle `logisim-evolution-4.0.0-all.jar`. Si ce n'est pas le cas, n'hésitez surtout pas à l'adapter !

