---
description: word count
---

# wc

## Introduction

Afficher le décompte de lignes, de mots et d’octets pour chaque FICHIER et le nombre total de lignes si plus d’un FICHIER est indiqué. L’entrée standard est lue quand FICHIER est omis ou quand FICHIER vaut « - ».

## Syntaxe

```
wc <OPTIONS> <FICHIER>
```

### Options

| `-c` | bytes |
| ---- | ----- |
| `-m` | chars |
| `-l` | lines |
| `-w` | words |

## Utilisation

### Compter le nombre de lignes

Compte le nombre de lignes du fichier auth.log

```
wc /var/log/auth.log -l
```

### Compter le nombre de mots

Compte le nombre de mots du fichier ./bashrc

```
wc .bashrc -w
```
