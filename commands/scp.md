---
description: secure copy
---

# scp

## Introduction

`SCP`, également appelé `secure copy`, est un utilitaire de ligne de commande permettant de transférer des fichiers et des répertoires d’un système local vers un système distant et vice-versa. Il nous permet également de transférer des fichiers et des répertoires entre deux systèmes distants. Les fichiers et les mots de passe sont cryptés pendant le transfert, ce qui en fait un moyen de transfert plus sûr.

1. Cette commande utilise la clé `ssh` ou le mot de passe pour authentifier les systèmes distants.
2. Elle reconnaît les systèmes distants avec le symbole `:`.
3. Nous devons regarder les permissions de lecture du fichier ou du répertoire source et les permissions d’écriture du fichier ou du répertoire de destination.
4. Le `scp` écrase les fichiers sans avertissement. Nous devons donc être prudents lors du transfert de fichiers qui partagent le même nom et le même emplacement sur les deux systèmes.

## Syntaxe

```
scp [OPTION] [user@]SRC_HOST:]file1 [user@]DEST_HOST:]file2
```

* `OPTION`: Elle représente les options `scp` telles que le chiffrement, la configuration ssh, le port ssh, la limite, la copie récursive …etc
* `[user@]SRC_HOST:]file1` : fichier ou répertoire source à copier
* `[user@]DEST_HOST:]file2` : chemin d’accès au répertoire où le fichier ou le répertoire source doit être copié

### Options

| Paramètre | Description                                                    |
| --------- | -------------------------------------------------------------- |
| `-P`      | Préciser le port ssh de l’hôte distant                         |
| `-p`      | Préserver les temps de modification et d’accès aux fichiers.   |
| `-q`      | Supprimer l’indicateur de progression et les messages d’erreur |
| `-C`      | Compression des données lors du transfert                      |
| `-r`      | Copiez les fichiers de manière récursive.                      |

## Utilisation

#### Copier un fichier d'un système local vers un système distant <a href="copier-un-fichier-d-un-systeme-local-vers-un-systeme-distant" id="copier-un-fichier-d-un-systeme-local-vers-un-systeme-distant"></a>

```bash
scp file.txt remote_username@11.11.0.200:/Documents/directory
```

Cette commande nous demandera un mot de passe d’utilisateur et le transfert commencera une fois que nous aurons entré le bon mot de passe. Il copie le fichier `file.txt` sur notre système local vers le serveur distant avec le nom d’utilisateur `remote_username` et l’adresse IP `11.11.0.200`. `/Documents/directory` représente le répertoire de destination sur le serveur distant dans lequel le fichier doit être copié. Si le répertoire distant n’est pas spécifié, le fichier sera copié dans le répertoire d’origine de la machine distante.

**Préciser le port**

Si le `SSH` sur la machine distante écoute un autre port que le port par défaut `22`, nous pouvons spécifier le port en utilisant l’option `-P`

```
scp -P 8080 main.py remote_username@11.11.0.200:/Documents/directory
```

**Copier un répertoire local vers un système distant**

```
scp -r /Documents/myapp remote_username@11.11.0.200:/Documents/remote_app
```

Copie le répertoire `myapp` à l’intérieur du répertoire `Documents` de la machine locale dans le répertoire `remote_app` à l’intérieur du répertoire `Documents` de la machine distante.

**Copier un fichier du système distant vers un répertoire local**

```
scp remote_username@11.11.0.200:/remote/main.py /Documents/local
```

Il copie le fichier `main.py` du système distant vers notre système local avec le répertoire de destination `/Documents/local`

**Copie d'un emplacement distant vers un emplacement distant**

```
scp userA@11.11.0.200:/host1/main.py userB@11.11.0.205:/host2
```

Il copie le fichier `/host1/main.py` de l’hôte distant avec l’adresse IP `11.11.0.200` dans le répertoire `host2` de l’hôte avec l’adresse IP `11.11.0.205`.

Pour acheminer le trafic à travers la machine dans laquelle la commande est émise, nous ajoutons l’option `-3` à la commande `scp`.
