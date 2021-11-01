---
description: pattern scanning and text processing language
---

# awk

## Introduction

mawk is an interpreter for the AWK Programming Language. The AWK lan‐ guage is useful for manipulation of data files, text retrieval and pro‐ cessing, and for prototyping and experimenting with algorithms.

An AWK program is a sequence of pattern {action} pairs and function definitions. Short programs are entered on the command line usually enclosed in ' ' to avoid shell interpretation. Longer programs can be read in from a file with the -f option. Data input is read from the list of files on the command line or from standard input when the list is empty. The input is broken into records as determined by the record separator variable, RS. Initially, RS = “\n” and records are synony‐ mous with lines. Each record is compared against each pattern and if it matches, the program text for {action} is executed.

{% embed url="https://likegeeks.com/awk-command/" %}

### The AWK Language

## Syntaxe

```bash
awk [options] [programme] [fichier]
```

### Options

| Option | Description                                                           |
| ------ | --------------------------------------------------------------------- |
| `-F`   | Séparateur de champs                                                  |
| `-f`   | Lecture depuis un fichier plutôt que directement en ligne de commande |
|        |                                                                       |

## Utilisation

```bash
awk -F : '{print $2}' KALIHash.txt
```

