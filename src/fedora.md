# Fedora

Fedora est une distribution linux utilisable sur un ordinateur personnel, développée de manière à être simple d'utilisation, même par une personne n'ayant jamais touché à linux. C'est cette distribution que nous installons lors de nos install-party.

## Installation

Nous organisons régulièrement des install-party, où nous pouvons vous installer fedora, mais vous pouvez également faire l'installation vous même si vous pensez en être capable.

L'installation de fedora (et de n'importe quelle distribution linux) peut se faire de deux manière : 

- En dual boot : installation en parallèle d'un autre système d'exploitation comme Windows, avec un écran de séléction au démarage de l'ordinateur.

- En tant que seul système d'exploitation de l'ordinateur, en remplaçant l'OS précédemment présent installé (par exemple en remplaçant Windows)

Pour réaliser l'installation, le seul matériel nécessaire est **une clé USB**, d'environs 8 Go ou plus.

> ⚠️ L'installation de linux n'est pas sans risques, et peut vous faire perdre vos données. Pensez bien à faire une sauvegarde avant de vous lancer, et de bien brancher votre ordinateur sur le secteur lors de l'installation, pour éviter que le PC ne s'éteigne lors d'une étape critique.

### 1 - Vérifications à faire

Avant d'installer une districution linux, il y a plusieurs informations à vérifier.

La première chose à faire est de vérifier si on a assez d'espace sur son disque. Pour une utilisation normale sur un ordinateur personnel de linux, environs 50 Go sont suffisant.

> Il est possible que votre ordinateur ait plusieurs disques, ou ait un disque séparé en plusieurs partitions par son constructeur. Il est toujours possible d'installer linux dans ce cas là, mais des manipulations supplémentaires sont souvent nécessaires.

Vous devez ensuite vérifier si votre disque contenant Windows n'est pas chiffré. Pour cela, cherchez "Bitlocker", ou "Chiffrement" dans la barre de recherche. Vous devriez trouver une page du panneau de configuration vous permettant de désactiver *Bitlocker*, le système de chiffrement de Windows. Ce système de chiffrement empêche l'installation d'un autre OS.

TODO: Ajouter une image

*Désactivation de Bitlocker sous [Version windows de l'image] (l'interface peut varier selon les versions de WIndows)*

### 2 - Libérer de l'espace dans la table de partitions

Fedora devra être installé dans une [partition](https://fr.wikipedia.org/wiki/Partition_(informatique)) de votre disque. Un disque dur peut être divisé en plusieurs partitions pouvant contenir différent [systèmes de fichiers](https://fr.wikipedia.org/wiki/Syst%C3%A8me_de_fichiers). Nous devons donc libérer de l'espace dans ce que l'on appelle la **table de partitions**. 
Il est recommandé de le faire depuis windows, pour éviter des perdre des données en libérant de l'espace, en effet Windows ne vous laissera pas supprimer des fichiers sur sa propre partition.

Pour commencer, ouvrez le **Gestionnaire de disques** de Windows (son nom sera probablement **Créer et formater des partitions de disque dur**). Depuis ce gestionnaire, dans la zone du bas (en rouge), vous verrez la liste des partitions de votre disque. 

![gestionnaire de disque windows](./content/windows_disk_editor.png)

Vous pouvez alors réduire la partition où se trouve windows. La plupart du temps, ce sera **C:**. Pour être sur de réduire la bonne partition, vous devez chercher une partition de grande taille (souvent la plus grande), avec **NTFS** comme système de fichier indiqué. 

Faites un clique droit dessus, et cliquez sur **réduire le volume**. Vous devez alors indiquer la taille que vous voulez pour la future partition qui contiendra Linux. Pour cela, renseignez cette taille (en Mo) dans le champ *Quantité d'espace à réduire*.

![réduire taille partition](./content/reduce_partition.png)

Une fois la partition réduite, vous devrize avoir de l'espace libre, sur lequel on pourra installer linux.

### 3 - Création du medium d'installation

Munissez vous de votre clé USB, et téléchargez le [fichier iso](https://fr.wikipedia.org/wiki/Image_disque) de Fedora, disponible sur [leur site](https://fedoraproject.org/fr/workstation/). 

Nous allons ensuite installer **Ventoy** sur la clé. Ventoy est un outil permettant de faciliter le démarrage de fichiers iso contenant un système d'exploitation sur une clé USB. Téléchargez ventoy depuis [leur site](https://www.ventoy.net/en/download.html), et lancez **Ventoy2Disk**. Séléctionnez votre clé USB (vérifier bien que c'est votre clé et pas un disque de votre dordinateur) et cliquez sur **install**.

> ⚠️ Cette opération supprimera tout le contenu de la clé USB.

![Ventoy installation](./content/install_ventoy.png)

Votre clé dvevrait alors apparaitre dans la liste des disques de l'explorateur de fichiers, avec le nom **VENTOY**. Vous pouvez alors placer le fichier iso de Fedora dans la clé.

Les étapes sous windows sont maintenant terminées !

### 4 - Vérification des paramètres dans le BIOS

Cette partie est la plus difficile à expliquer, parce qu'elle dépend du modèle et de la marque de votre PC.

Vous allez devoir acceder au **BIOS** de votre PC. Le BIOS est un micro système d'exploitation vous permettant de modifier des paramètres du matériel de votre ordinateur. Nous allons devoir modifier et/ou vérifier certains paramètres. Selon la marque l'interface du BIOS peut complètement changer, il est donc possible que les indications données ici ne soient pas réalisable chez vous, où que vous ne trouviez pas les choses demandées, pas de panique, le plus souvent une recherche google avec le modèle de votre PC et le paramètre recherché vous expliquera quoi faire dans ce cas.

> ☝️🤓 Sur la plupart des PC récent, le BIOS est remplacé par l'[UEFI](https://fr.wikipedia.org/wiki/UEFI), qui lui succède. Quand on parle de BIOS, c'est très souvent un abus de langage pour dire UEFI.

La première chose à faire est d'éteindre votre PC, puis de l'allumer, et lors du démarrage, quand vous voyez le premier logo (celui de la marque de l'ordinateur), appuyer sur la touche permettant d'accéder au BIOS. Cette touche varie selon les marques et les modèles. Cette image indique les touche des marques les plus populaires. Si votre PC n'est pas sur l'image, ou que la touche ne marche pas, n'hésitez pas à chercher sur internet.

![Bios keys](./content/bios_keys.png)

Une fois dans le BIOS, vous devriez être face à écran, qui peut ressembler à ça (ou non, selon votre PC) :

![Bios main](./content/bios_main.jpg)

Il faut alors trouver la catégorie **boot** (ou un nom similaire), et trouver ce que l'on appelle **l'ordre de boot**. Cet ordre définit que quel disque l'ordinateur va essayer de cherger un système d'exploitation en premier. On veut donc mettre la clé usb contenant Fedora en premier.

![Bios boot](./content/bios_boot.jpg)

Une fois cela fait, vous pouvez sauvegarder et quitter le BIOS.

Il est possible qu'un message d'affiche pour vous prévenir que la clé n'est pas vérifiée. Continuez, et attendez que l'ordinateur démarre sur la clé. L'ISO de Fedora sur la clé sera utilisé comme système d'exploitation pour l'ordinateur. La clé contient un Fedora totalement fonctionnel, avec une application permettant l'installation sur le vrai disque dur de l'ordinateur.

### 5 - Installation

TODO: Continuer :c



