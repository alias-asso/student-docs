# Mars

Mars est le logiciel servant à émuler le processeur MIPS sur nos ordinateurs. Il permet de coder et d'exécuter des codes assembleurs sur des architectures modernes.

Normalement, ce tutoriel fonctionne sur tous les systèmes d'exploitation, que ça soit Windows, MacOS ou n'importe quelle distribution Linux tant que Java est disponible dessus.

## Installation avec la version recommandée de Java

Mars a été compilé avec Java 1.5 (dit Java 5). Il est préférable d'installer cette version spécifiquement pour avoir moins de bugs. Vous pouvez la télécharger sur [le site d'Oracle](https://www.oracle.com/java/technologies/java-archive-javase5-downloads.html).

Mars est téléchargeable sur [GitHub](https://github.com/dpetersanderson/MARS/releases/tag/v.4.5.1). Il est disponible sous le nom de `Mars4_5.jar` dans les assets. Le lien direct est disponible [ici](https://github.com/dpetersanderson/MARS/releases/download/v.4.5.1/Mars4_5.jar).

Après avoir installé Java et téléchargé le fichier `.jar`, il suffit d'exécuter le `.jar` pour lancer Mars.

Si vous n'arrivez pas le lancer avec votre environnement graphique, vous pouvez le lancer en ligne de commande :
```bash
java -jar Mars4_5.jar
```
Attention, vous devez bien être dans le dossier contenant Mars.

## Utiliser une autre version de Java

Durant votre cursus à Sorbonne Université, vous allez être amené⋅es à faire du Java sur des versions beaucoup plus récentes que Java 5 et à utiliser des logiciels demandant des versions plus récentes (comme [Logisim](./logisim.md)).

Pour éviter de devoir jongler, il est possible d'utiliser une version plus récente de Java avec Mars. Il faut bien avoir en tête que cela pourrait créer des bugs lors de votre utilisation de Mars (même si je n'en ai, pour l'instant, rencontré aucun).

Si vous choisissez d'utiliser une version plus récente, nous vous conseillons Java 21 qui est requise par [Logisim](./logisim.md). (Il est impossible de faire tourner Logisim avec une version plus vieille que Java 21, comme celle requise par Mars.)
