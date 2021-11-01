---
description: disk usage
---

# du

## Introduction

Summarize disk usage of the set of FILEs, recursively for directories.

## Syntaxe

```
du [parameter] [argument]
```

### Options

| Paramètre              | Description                                                                             |
| ---------------------- | --------------------------------------------------------------------------------------- |
| `-a`                   | write counts for all files, not just directories                                        |
| `-B = SIZE`            | scale sizes by SIZE before printing them                                                |
| `-c`                   | produce a grand total                                                                   |
| `-d`                   | max depth                                                                               |
| `-h`                   | human readable                                                                          |
| `-S`                   | For directories do not include size of subdirectories                                   |
| `-s`                   | Display only a total for each argument                                                  |
| `-t = SIZE`            | exclude entries smaller than SIZE if positive, or entries greater than SIZE if negative |
| ` --exclude = PATTERN` | exclude files that match PATTERN                                                        |

### Pattern

PATTERN is a shell pattern

&#x20;The pattern:

* **?** matches any one character
* **\*** matches any string (composed of zero, one or multiple characters).&#x20;

## Utilisation

```
du --exclude='*.o'
```

&#x20;Will skip all files and subdirectories ending in **.o** (including the file **.o** itself).

```
du -sh
```

Will print the size of current directory
