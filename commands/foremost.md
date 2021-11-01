---
description: Récupération de fichier
---
# foremost

## Introduction

**Foremost** est une application en ligne de commande qui donne la possibilité de récupérer simplement des fichiers qui ont été effacés où encore des fichiers "disparus" suite à un "formatage rapide" (reconstruction de l'index de la [partition](https://doc.ubuntu-fr.org/partitions)) La récupération d'un fichier effacé part d'un concept simple… quand vous supprimez un fichier, c'est uniquement le pointeur vers celui-ci qui est brisé mais il n'est pas immédiatement écrasé par d'autres données. Le fichier est donc toujours physiquement présent sur le disque dur. Évidement, plus vous attendez avant de récupérer un fichier, plus celui-ci a de chance de disparaître à jamais…

À noter que **Foremost** ne reconstruit pas l'index de la partition.

## Syntaxe

```bash
foremost -w -i <partition> -o <destination>
```

### Options

| Paramètre | Description                                             |
| --------- | ------------------------------------------------------- |
| `-w`      | Activation du mode audit                                |
| `-i`      | Choix de la partition où se trouve les fichiers effacés |
| `-o`      | Répertoire de destination de la récupération            |
| `-t`      | Choix du type de fichier                                |

## Utilisation

### Récupération de toutes les données effacées

La partition  `/dev/sdaX`  (avec  X  comme numéro de partition) définit de quel volume de disque il s'agit. Il est donc nécessaire d'adapter ce paramètre selon le cas. À noter que le répertoire de destination doit obligatoirement être vide.

```bash
foremost -t all -i /dev/sdaX o /root/Desktop/recovery/
```

Il est également possible de choisir le type de chier à récupérer (jpeg, png ou gif) :

```bash
foremost -t jpeg,gif -i /dev/sdaX -o /root/Desktop/recovery/
```

### Lister les fichiers <a href="lister_les_fichiers" id="lister_les_fichiers"></a>

Si vous souhaitez connaître la liste des fichiers qu'il est possible de récupérer sur votre partition sans les extraire (argument **-w**)

```
sudo foremost -w /dev/sdc
```

_La liste nommée "audit.txt" sera déposé dans le dossier "output" de votre dossier personnel)._

Si vous souhaitez connaître la liste des fichiers qu'il est possible de récupérer dans un répertoire spécifique (argument **-o**) sans les extraire (argument **-w**)

```
sudo foremost -w -i /dev/sdc -o /home/user/Documents
```

