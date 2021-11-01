---
description: find files using expression
---

# find

## Introduction

La commande `find` permet de retrouver des fichiers à partir de certains critères. Quelques exemples pratiques, notamment avec des expressions régulières, elles sont trop peu utilisées mais si puissantes.

### Opérateurs logiques

| Opérateur | Syntaxe        |
| --------- | -------------- |
| AND       | \\( P -a Q \\) |
| NOT       | \\( ! P \\)    |
| OR        | \\( P -o Q \\) |

## Syntaxe

```bash
find répertoire critères
```

### Options

| Paramètre | Description                                                    |
| --------- | -------------------------------------------------------------- |
| `-name`   | recherche sur le nom du fichier                                |
| `-perm`   | recherche sur les droits d’accès du fichier                    |
| `-user`   | recherche sur le propriétaire du fichier                       |
| `-group`  | recherche sur le groupe auquel appartient au fichier           |
| `-type`   | recherche sur le type (d=répertoire, l=lien, f=fichier normal) |
| `-size`   | recherche par taille de fichier                                |
| `-mtime`  | recherche par date de dernière modification du fichier         |
| `-ctime`  | recherche par date de création du fichier                      |
| `-L`      | lien symbolique                                                |

## Utilisation

### Recherche par nom de fichier

Rechercher tous les fichiers se terminant par `.c` dans le répertoire `/usr`&#x20;

```bash
find /usr -name *.c -print
```

### Recherche par dates

Rechercher les fichiers `*.js` ou `*.css` modifiés il y a moins de 2 jours :

```bash
find . -mtime -2 -a \( -name "*.js" -o -name "*.css" \)
```

Rechercher les fichiers `*.json` créés il y a plus de 30 jours dans le répertoire `$LOG` :

```bash
find $LOG -ctime +30 -name "*.json" | sort
```

{% hint style="info" %}
L’option `-mtime -2` est en fait équivalente à `-48h`, l’option `-ctime +30` à `+30 × 24h` : `find` se base par défaut sur la date et l’heure courante. Utiliser `daystart` pour se baser réellement sur le nombre de jours sans prendre en compte l’heure courante.
{% endhint %}

### Recherche par taille

Identifier dans une arborescence les fichiers `*.html` dont la taille est supérieure à 50K (soit 100 blocs de 512o) :

```bash
find . -size +100 -name "*.html"
```

Dans la pratique, l’unité (`k | M | G`) est spécifiée pour ne pas calculer les multiples de 512 octets.

```bash
find . -size +50k -name "*.html"
find . -size +100M
find . -size +2G
```

### Redirection des messages d’erreur

Les droits d’accès ne sont pas toujours autorisés pour certains répertoires, par conséquent, la commande `find` peut générer un grand nombre de messages d’erreur (permission denied, etc.). Pour éviter ceci, rediriger les messages d’erreur vers un fichier "poubelle" (ex `/dev/null`), les messages d’erreur sont alors perdus. Il est toutefois possible de sauvegarder ces erreurs dans un fichier régulier. Le `2>/dev/null`à la fin de la commande demande au terminal de rediriger les messages d'erreurs FD #2 dans `/dev/null`.

```bash
find / \( -name a.out -o -name "*.c" \) 2>/dev/null
```

### Expressions régulières (-regex et -regextype)

Option `-regex`

L’exemple précédent n’est pas très élégant ( `-o -name "*.css" -o -name "*.php`… ). Les expressions régulières sont implémentées dans la commande `find` avec l’option `-regex`.

Le code devient bien plus lisible avec cette fonctionnalité.

```bash
find . -regex '.*\.\(css\|htm\|html\|inc\|js\|json\|php\|xml\)' -exec file -i {} \;
```

Plusieurs librairies existent pour les expressions régulières (posix, GNU awk…), librairies pour lesquelles les syntaxes des expressions régulières peuvent différer.

L’option `-regextype` donne la librairie à utiliser pour l’expression régulière : un exemple de recherche des fichiers `*.txt` et `*.inc` avec la librairie `posix-basic`.

```bash
find -regextype posix-basic -regex ".*\(txt\|inc\)" -print
```

Une petite astuce pour retrouver les librairies disponibles sur la plateforme utilisée : appeler une commande `find` avec une option `-regextype` invalide.

```bash
find .-regextype dummyfind: Unknown regular expression type `dummy'; valid types are `findutils-default', `awk', `egrep', `ed',
`emacs', `gnu-awk', `grep', `posix-awk', `posix-basic', `posix-egrep',
`posix-extended', `posix-minimal-basic', `sed'.
```

Pour gérer l’insensibilité à la casse dans les expressions régulières, utiliser option `-iregex`.

```bash
find -iregex ".*\.\(txt\)' -print./README.TXT
```

### Un exemple bien utile : calculer la taille des images dans un répertoire

En une ligne de commande en combinant `find` et `awk`, pour calculer la taille des images dans un répertoire :

```bash
find . -regex '.*\.\(png\|gif\|jpg\|jpeg\)' -exec ls -l {} \; | \
          awk 'BEGIN {sum=0} {sum+=$5} END { printf("%.2f %s\n",sum/1024000,"Mb") }'
```

### Option exec

L’option `-print` est une option que l’on passe à la commande `find` pour afficher les résultats à la sortie standard. L’option `-exec` est disponible dans la commande `find` et elle est exclusive de l’option `-print`.

Lorsque la commande `find` est couplée à l’option `exec`, il est alors possible d’exécuter une commande sur les fichiers trouvés par la commande `find`.

```bash
find repertoire critères -exec commande {} \;
```

La sortie de la commande `find` avec l’option `-print` est très basique, voire trop :

```bash
find . -type f -size +100k -print./sybase-replication-server-guide-pratique.pdf
./images/gimp-supprimer-couleur-arriere-plan-fond-09.jpg
…
```

Avec l’option `-exec`, la commande `find` est usuellement combinée avec la commande `ls` pour afficher plus de détails sur les résultats :

```bash
find . -type f -size +100k -exec ls -lh {} \; 2> /dev/null-rw-r--r-- 1 sqlpac wapp 118K Jun 15 11:34 ./sybase-replication-server-guide-pratique.pdf
-rw-r--r-- 1 sqlpac wapp 104K Jun 15 11:33 ./images/gimp-supprimer-couleur-arriere-plan-fond-09.jpg
…
```

Autres exemples courants :

Supprimer tous les fichiers core avec la commande `rm` :

```bash
find . -name core -exec rm {} \;
```

Supprimer tous les fichiers `*.json` créés il y a plus de 10 jours dans le répertoire `$LOG` avec la commande `rm` :

```csharp
find $LOG -name "*.json" -ctime +10 -exec rm {} \;
```

Des exemples encore plus concrets :

On recherche dans un répertoire et ses sous répertoires la liste des fichiers `*.htm, *.html, *.inc, *.php, *.css, *.json, *.xml` pour lesquels l’encodage est iso-8859-1. L’encodage est donné par la commande `file` et l’option `-i` :

```bash
find . -type f  \( -name "*.html" -o -name "*.htm" -o -name "*.json" -o -name "*.php" -o -name "*.inc" -o -name "*.x
ml" -o -name "*.css" -o -name "*.xml" \) -exec file -i {} \;  | grep -i 'iso-8859-1'./admpmgportal/config.inc: text/x-php; charset=iso-8859-1
./admpmgportal/include/rules.inc: text/x-php; charset=iso-8859-1
./admpmgportal/include/treeview.inc: text/html; charset=iso-8859-1...
```

Pour retrouver tous les fichiers non binaires contenant la chaîne de caractères `'79.13'` :

```bash
find . -type f -exec grep -Il '79\.13' {} \;./redis/dba/srvrdisqlpac/cfg/srvrdisqlpac.conf
...
```

Bien utile pour rechercher des codages (adresses IP, fonctions…) dans une arborescence, quel que soit le type de fichier du moment qu’il ne s’agisse pas d’un fichier binaire. L’option `-I` dans la commande `grep` écarte les fichiers binaires.

[https://www.sqlpac.com/fr/documents/unix-find-grep-commandes.html](https://www.sqlpac.com/fr/documents/unix-find-grep-commandes.html)

Exemple: déplacer tous les fichiers pdf existants dans une hiérarchie dans un dossier:

le + sert à exécuter le moins de move possible

```
find -name *.pdf -exec mv -t ../dst {} + 
```

