# tar

## Introduction

Vous avez sûrement déjà entendu parler du format `zip`. C'est le plus connu et le plus répandu… du moins sous Windows. On peut l'utiliser aussi sous Linux, de même que le format `rar`.

Cependant, on préférera utiliser des alternatives libres (et souvent plus puissantes) telles que le `gzip` et le `bzip2`. Toutefois, contrairement à `zip` et `rar`, le `gzip` et le `bzip2` ne sont capables de compresser qu'un seul fichier à la fois et ne peuvent donc pas créer un « paquetage » de plusieurs fichiers.

Sous Linux, on a depuis longtemps pris l'habitude de procéder en deux étapes :

1. réunir les fichiers dans un seul gros fichier appelé **archive**. On utilise pour cela le programme `tar` ;
2. compresser le gros fichier ainsi obtenu à l'aide de `gzip` ou de `bzip2`.

![](<../.gitbook/assets/image (3).png>)



## Syntaxe

```bash
tar <option> 
```

### Options

| Paramètre | Description                                          |
| --------- | ---------------------------------------------------- |
| `-c`      | créer une archive tar                                |
| `-v`      | afficher les détails de l'opération (verbose)        |
| `-f`      | assembler l'archive dans un fichier                  |
| `-z`      | compresse l’archive avec gzip (archive.**tar.gz**)   |
| `-j`      | compresse l’archive avec bzip2 (archive.**tar.bz2**) |
| `-J`      | compresse l'archive avec xz (archive**.tar.xz**)     |
| `-x`      | extraire l'archive dans le répertoire courant        |
| `-C`      | extraire l'archive dans un répertoire spécifique     |
| `-tf`     | afficher l'archive sans l'extraire                   |
| `-rvf`    | ajouter un fichier à l'archive                       |

## Utilisation

**Archiver et compresser en gzip**

```bash
tar -zcvf tutoriels.tar.gz tutoriels/
```

pour décompresser, c'est pareil, sauf que le `-c` est remplacé par un `-x` comme tout à l'heure :

```bash
tar -zxvf tutoriels.tar.gz
```

**Archiver et compresser en bzip2**

Le principe est le même avec `-j` à la place de `-z` :

```
tar -jcvf tutoriels.tar.bz2 tutoriels/
```

Et pour extraire :

```
tar -jxvf tutoriels.tar.bz2 tutoriels/
```

### Analyser le contenu

Vous pouvez toujours analyser le contenu de l'archive avant de la décompresser. Avec `-ztf`, vous regarderez à l'intérieur d'une archive « gzippée » et avec `-jtf`, vous regarderez à l'intérieur d'une archive « bzippée-deux ».
