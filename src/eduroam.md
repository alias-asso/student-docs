# Eduroam

## Eduroam d'UPMC et la reMarkable 2

Si vous êtes détenteur d'une tablette reMarkable 2, vous aurez sans doute constaté que la connexion à eduroam est difficile.  

Dans cet article, nous développerons la technique vous permettant de vous connecter au réseau.

> ⚠️ Ce tutoriel n'a pas été testé pour le modèle reMarkable 1

> 💡 Il est recommandé de désactiver les mises à jour automatique car une mise à jour est fortement susceptible de supprimer les fichiers nécessaires à la connexion. <br/><br/>Pour se faire, sur votre tablette, aller dans vos paramètres... <br/> General > Software (cliquez sur la version) > Automatic Updates off

### Sources mobilisées
- [r/RemarkableTablet | Can't connect remarkable 2 to eduroam (reddit.com)](https://www.reddit.com/r/RemarkableTablet/comments/kdi0av/comment/istqix7/?utm_source=share&utm_medium=web2x&context=3)

- [Tips Wifi: Configuring wpa supplicant manually](https://remarkablewiki.com/tips/wifi#configuring_wpa_supplicant_manually)

### Se connecter au SSH de la reMarkable

Toutes les tablettes reMarkable 2 possède une clé SSH, vous pouvez vous connecter à votre tablette très simplement

#### Disposer d'un outil de connexion SSH  

Pour cela, vous devrez disposer de l'outil très reconnu pour vous connecter au SSH directement sur le terminal: [Openssh](https://www.openssh.com/)  
Par défaut, ce logiciel est déjà installé sur MacOS, et une version spéciale est aussi disponible directement sur Windows 10.  

Si vous êtes sous Linux, installez le package openssh, sur Ubuntu, utilisez le package manager `apt` (N'oubliez pas de mettre à jour avant d'installer un nouveau packet):
```bash
sudo apt install openssh
```

Pour vérifier si openssh est bien installé, tapez la commande `ssh` dans le terminal.  
Si la commande n'est pas reconnue, renseignez-vous sur l'installation du logiciel [sur le site officiel](https://www.openssh.com/)


#### Connectez votre tablette à votre ordinateur  

Si cela est nécessaire accepter le partage information entre l'ordinateur et la tablette

#### Connectez-vous au `ssh` de votre tablette  
   
Sur votre terminal, tapez la commande suivante:
```bash
ssh root@10.11.99.1
```
>💡 Effectivement, nous nous connectons avec le nom d'utilisateur "root" à l'appareil d'adresse ip 10.11.99.1, l'ip local de la remarkable

Il vous sera demandé de renseigner un mot de passe, celui-ci est disponible dans les paramètres:  
`Help > About > Copyright notices and software licenses > GPLv3 Compliance`

>💡 Quand vous taperez sur votre clavier, rien ne s'affichera à l'écran mais vos touches seront prises en compte ! Il s'agit d'une sécurité visant à ne pas dévoiler la longueur du mot de passe.

⚠️ **_Si vous en générez un nouveau, enregistrez le quelque part, car il sera impossible de vous connecter avec votre tablette si vous ne vous en souvenez plus !_**

### Générer le certificat eduroam
**Sur votre ordinateur**, vous allez générez les certificat nécessaire pour vous connecter au réseau wifi eduroam avec votre identité étudiante.

Nous allons ensuite transférer ces fichiers vers la tablette reMarkable grâce au protocole `scp` en utilisant l'outil intégré de **Openssh**

#### Procurez-vous le script Python pour eduroam sur Linux

>💡 Nous allons récupérer des informations à l'intérieur, l’intégralité du script ne nous intéresse pas. Vous n'avez donc pas besoin d'avoir Python installé sur votre ordinateur.
   
Pour cela, rendez-vous sur le site [cat.eduroam.org](https://cat.eduroam.org/)
* Cliquez sur téléchargez l'installateur
* Choisissez l'université UPMC 
* Cliquez sur *Choisissez un autre installateur à télécharger* 
>💡 Si vous êtes sur une machine Linux, ce n'est pas nécessaire !
* Sélectionnez Linux puis téléchargez le.

#### Extrayez le [CA](https://en.wikipedia.org/wiki/Certificate_authority) public initialisé en fin de script 

Vous le trouverez, à partir de la ligne 1091 *(Lors de l'écriture de cette article)*

Copiez l'intégralité du certificat de, (donc tout ce qu'il y a l'intérieur des triples guillemets (sans les triples guillemets)).

⚠️ Il faut que vous ayez récupéré **3 clés différentes** et donc que vous vous soyez arrêté **au dernier tiret de la 3e mention** `END CERTIFICATE`

Sauvegardez le texte que vous avez copié dans un fichier que vous aurez enregistré sous le nom `ca.pem` pour [sauvegardez la clé publique](https://en.wikipedia.org/wiki/Privacy-Enhanced_Mail)

### Créez le fichier *wpa_supplicant*
   
Afin de faire reconnaître à la reMarkable le réseau wifi eduroam et de s'y connecter, nous devons créer un fichier de configuration [wpa_supplicant](https://wiki.archlinux.org/title/wpa_supplicant).

Actuellement, pendant l'écriture de cette article, vous pouvez utiliser cette configuration.

```conf
network={
        ssid="eduroam"
        key_mgmt=WPA-EAP
        pairwise=CCMP
        group=CCMP TKIP
        eap=TTLS
        ca_cert="/etc/wpa_supplicant/certificate/ca.pem"
        identity="NUMERO ETUDIANT"
        altsubject_match="DNS:radius.upmc.fr;DNS:radius.upmc.fr"
        phase2="auth=PAP"
    password="MOT DE PASSE"
    anonymous_identity="anonymous@upmc.fr"

}
```

Remplacez les lignes `identity` et `password` respectivemment avec votre numéro étudiant et votre mot de passe

>💡 Ce fichier n'étant pas crypté, notez bien que votre mot de passe sera visible pour quiconque peut accéder à ce fichier !

Une fois que tout est fait, vous pouvez sauvegarder ce fichier sous le nom de `eduroam.conf`

### Créez le service système permettant de vous connecter

Nous devrons créer un [fichier de service](https://www.imaginelinux.com/service-in-linux/) que nous activerons pour qu'il s’exécute dès l'allumage de la reMarkable

Ce fichier permettra aussi à la reMarkable de se connecter automatiquement à eduroam dès qu'il sera à porter.

Dans un fichier texte, copiez-collez les informations suivantes.

```service
[Unit]
Description=WPA supplicant daemon for eduroam 
After=network.target

[Service]
Type=simple 
ExecStart=/usr/sbin/wpa_supplicant -c/etc/wpa_supplicant/eduroam.conf -iwlan0 
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

Sauvegardez ensuite le fichier sous le nom de `eduroam.service`

### Créez les dossiers nécessaires sur le `ssh` de la tablette

Nous allons très vite envoyer les fichiers, mais nous avons d'abord besoin de créer les dossiers nécessaire s'il n'existe pas.

[Connectez vous à votre tablette](#connectez-vous-au-ssh-de-votre-tablette) puis ajouter les dossiers suivants.

Vous devez vous trouvez normalement à la racine du HOME de root.
Plus spécifiquement, si vous tapez
```bash
pwd
```
Vous devriez voir:
```bash
/home/root
```
Si ce n'est pas le cas, ce n'est pas bien grave, maintenant, vous savez où vous êtes dans l'arborescence de votre tablette.

Vérifiez l'existence du dossier `/etc/wpa_supplicant`:
```bash
ls /etc/wpa_supplicant
```
S'il n'existe pas, créez le avec la commande
```bash
mkdir -p /etc/wpa_supplicant/certificate
```
Cette commande aura aussi créer un sous dossier `certificate` dans `./wpa_supplicant` que vous devrez créer si vous ne l'avez pas fait.

Et avec ça, nous en avons fini et nous pouvons transférer les fichiers.
Déconnectez-vous du `ssh` avec la commande
```bash
exit
```

### Envoyez les fichiers sur la tablette avec `scp`

Une fois que vous avez confirmé que vous pouvez vous [connecter à la tablette en ssh](#connectez-vous-au-ssh-de-votre-tablette). Nous allons maintenant envoyer les fichiers que nous avons créé directement dessus.

La commande `scp` permet de réaliser un transfert de fichier en utilisant [le protocole de copie de même nom](https://en.wikipedia.org/wiki/Secure_copy_protocol).

Sur votre terminal **_et non pas sur le ssh de votre tablette_** identifiez l'endroit ou vous avez sauvegardé votre fichier [ca.pem](#extrayez-le-ca-public-initialisé-en-fin-de-script) puis renseignez la commande suivante (en remplaçant `/chemin/de/ca.pem` par le chemin d'accès)

```bash
scp /chemin/de/ca.pem root@10.11.99.1:/etc/wpa_supplicant/certificate/
```

⚠️ **Il est très important d'ajouter le / à la fin de la commande pour spécifier que nous envoyons ce fichier _à l'intérieur_ du dossier certificate.**

>💡 Si nous ne le faisons pas, alors nous allons renommer notre fichier `certificate` et allons l'envoyer à l'intérieur du dossier `wpa_supplicant`

Renseignez le mot de passe de la tablette et votre fichier devrait avoir été envoyé avec succès.

Envoyons maintenant le fichier `eduroam.conf` que vous avez dû [créer à cette étape](#créez-le-fichier-wpa_supplicant).
Il s'agit du même principe sauf qu'ici nous l'enverrons dans le dossier `/etc/wpa_supplicant/` et non pas dans le sous dossier `certificate`.

```bash
scp /chemin/de/eduroam.conf root@10.11.99.1:/etc/wpa_supplicant/
```

Finalement, envoyons le [fichier de service](#créez-le-service-système-permettant-de-vous-connecter) `eduroam.service` à la tablette.

```bash
scp /chemin/de/eduroam.service root@10.11.99.1:/lib/systemd/system/
```

### Activez le service, redémarrez et c'est terminé !

[Reconnectez vous au ssh](#se-connecter-au-ssh-de-la-remarkable) de votre tablette puis exécutez les commandes suivantes.

```bash
systemctl enable eduroam.service
```
Cela lancera le service permettant de se connecter à eduroam au démarrage de la tablette.
Vous pouvez maintenant redémarrez votre tablette avec:
```bash
reboot
```
Profitez bien de la connexion eduroam sur votre tablette :D 

> 💡 La connexion ne sera peut être pas instantanée, mais elle devrait se faire dans les prochaines secondes !