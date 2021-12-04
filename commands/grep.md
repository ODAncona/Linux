---
description: Globally search for a Regular Expression and Print matching lines
---

# grep

## Introduction

La commande `grep` permet d’explorer un ou une série de fichiers d’un même répertoire à la recherche de texte satisfaisant une expression régulière donnée. `grep` est l’acronyme de "Globally search for a Regular Expression and Print matching lines".

## Syntaxe

```bash
grep -option(s) expression fichier(s)
```

### Options

| Paramètre | Description                                                                   |
| --------- | ----------------------------------------------------------------------------- |
| `-v`      | affiche les lignes ne satisfaisant pas l’expression                           |
| `-c`      | compte le nombre de lignes satisfaisant l’expression sans afficher les lignes |
| `-n`      | affiche la ligne et le numéro de la ligne satisfaisant l’expression           |
| `-i`      | ignorer la casse                                                              |
| `-R`      | récursif                                                                      |
| `-o`      | only matching                                                                 |
| `-E`      | Expressions régulières                                                        |

## Utilisation

### Exemples

Rechercher des tableaux (balises HTML `<table>`) dans les fichiers `*.html` :

```bash
grep "<table" *.html…
```

Avec les numéros de lignes et sans sensibilité à la casse :

```bash
grep -ni "<table" *.html…
```

Juste le nombre d’occurrences en ignorant la casse :

```bash
grep -ci "<table" *.html | \
          awk -F":" 'BEGIN { hf=0; tb=0; } { if ($2 != 0) { hf++; tb +=$2 } } END { print tb" tableaux dans "hf" fichiers"}'
```

Les résultats en sortie de la commande `grep` sont séparés par `:`, bien pratique pour traiter rapidement les résultats avec l’utilitaire `awk`.

#### Lister les adresses IP présentes dans le fichier auth.log

```
grep -E "([0-9]{1,3}[\.]){3}[0-9]{1,3}" auth.log
```

### Expressions régulières

L’option `-E` donne une expression régulière à la commande `grep`.

Pour rechercher la chaîne de caractères `mysql_connect`, `mysql_query` et `mysql_close` dans des fichiers php avec les numéros de ligne :

```bash
grep -ni -E "mysql_connect|mysql_query|mysql_close" *.php
```

La commande `egrep` n’est ni plus ni moins que la commande `grep` avec l’option `-E` :

```bash
egrep -ni "mysql_(connect|query|close)" *.php
```

La liste des termes de l’expression régulière est parfois longue pour une seule ligne de commande, c’est pourquoi les termes peuvent être définis dans un fichier texte, fichier donné à la commande `grep` avec l’option `-f`.

```bash
grep -ni -f regex.txt *.php
```

Comme pour la commande `find`, la commande `grep` autorise l’utilisation de différentes syntaxes d’expressions régulières.

* Option `-E` : expressions régulières étendues (ERE, Extended Regular Expressions)
* Option `-G` : expressions régulières basiques (BRE, Basic Regular Expressions)
* Option `-P` : expressions régulières PERL (PRE, Perl Regular Expressions)

Rechercher des lignes commençant par une étoile, le caractère `^` dans l’expression régulière signifiant "commençant par" :

```bash
grep -ni -E "^ \*" *.php
```

Rechercher des lignes finissant par un point virgule , le caractère `$` dans l’expression régulière correspondant à une fin de ligne :

```bash
grep -ni -E "$;" *.php
```

En reprenant les premiers exemples, rechercher tous les tableaux dans les fichiers `*.html` ayant la classe CSS `rco-` et/ou `r-brdr` :

```bash
egrep -ni "<table.*class.*(rco-|r-brdr).*>" *.html
```

Lister les fichiers `*.html` ne contenant pas de tableaux (option `-L`) :

```bash
grep -L "<table" *.html
```
