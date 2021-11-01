---
description: display information from object files
---

# objdump

## Introduction

objdump displays information about one or more object files. The options control what particular information to display. This information is mostly useful to programmers who are working on the compilation tools, as opposed to programmers who just want their program to compile and work.

## Syntaxe

### Options

| Paramètre | Description                                                                                                                                                                                                   |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-d`      | Display the assembler mnemonics for the machine instructions from the input file. This option only disassembles those sections which are expected to contain instructions.                                    |
| `-D`      | Like -d, but disassemble the contents of all sections, not just those expected to contain instructions. It is possible for the output of -d and -D to differ if, for example, data is stored in code sections |
| `-t`      | Print the symbol table entries of the file.                                                                                                                                                                   |

## Utilisation
