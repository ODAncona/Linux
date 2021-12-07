---
description: Cheat Sheet
---

# VIM

### Global

* `:h[elp] keyword` - ouvrir l'aide pour le mot clé
* `:sav[eas] file` - sauvegarder un fichier sous
* `:clo[se]`- fermer le fichier en cours
* `:ter[minal]`- open a terminal window
* `K`- ouvre la page du manuel (man) du mot sous le curseur

**Tip** Run vimtutor in a terminal to learn the first Vim commands.

### Mouvement du curseur

* `h` - déplacer le curseur vers la gauche
* `j` - déplacer le curseur vers le bas
* `k` - déplacer le curseur vers le haut
* `l` - déplacer le curseur vers la droite
* `H` - aller en haut de l'écran
* `M` - aller au milieu de l'écran
* `L` - aller en bas de l'écran
* `w` - aller en avant au début d'un mot
* `W` - aller en avant au début d'un mot (les mots peuvent contenir de la ponctuation)
* `e` - aller en avant à la fin d'un mot
* `E` - aller en avant à la fin d'un mot (les mots peuvent contenir de la ponctuation)
* `b` - aller en arrière au début d'un mot
* `B` - aller en arrière au début d'un mot (les mots peuvent contenir de la ponctuation)
* `ge` - jump backwards to the end of a word
* `gE` - jump backwards to the end of a word (words can contain punctuation)
* `%` - aller au caractère associé (paires par défaut: '()', '{}', '\[]' - utiliser `:h matchpairs` dans vim pour plus d'informations)
* `0` - aller au début de la ligne
* `^` - aller au premier caractère non-espace de la ligne
* `$` - aller à la fin de la ligne
* `g_` - aller au dernier caractère non-espace de la ligne
* `gg` - aller à la première ligne du document
* `G` - aller à la dernière ligne du document
* `5gg or 5G` - aller à la ligne 5
* `gd` - move to local declaration
* `gD` - move to global declaration
* `fx` - atteindre la prochaine occurence du caractère x
* `tx` - atteindre le caractère précédent la prochaine occurence du caractère x
* `Fx` - atteindre la précédente occurence du character x
* `Tx` - atteindre le caractère suivant la précédente occurence du caractère x
* `;` - répéter le dernier f, t, F ou T
* `,` - répéter le dernier f, t, F ou T, dans l'autre sens
* `}` - atteindre le prochain paragraphe (ou function/bloc, en mode édition)
* `{` - atteindre le précédent paragraphe (ou function/bloc, en mode édition)
* `zz` - centre le curseur sur l'écran
* `Ctrl + e` - Descendre l'écran d'une ligne (sans déplacer le curseur)
* `Ctrl + y` - Monter l'écran d'une ligne (sans déplacer le curseur)
* `Ctrl + b` - Descendre d'une hauteur d'écran
* `Ctrl + f` - Monte d'une hauteur d'écran
* `Ctrl + d` - Monte d'une demie-hauteur d'écran
* `Ctrl + u`- Descendre d'une demie-hauteur d'écran

**Tip** Préfixez un mouvement avec un nombre pour le répeter. Par exemple, 4j déplace le curseur de 4 lignes vers le bas.

### Mode insertion - insérer/ajouter du texte

* `i` - insérer avant le curseur
* `I` - insérer au début de la ligne
* `a` - insérer (ajouter) après le curseur
* `A` - insérer (ajouter) à la fin de la ligne
* `o` - ajouter (ouvrir) une nouvelle ligne vers le bas
* `O` - ajouter (ouvrir) une nouvelle ligne vers le haut
* `ea` - insérer (ajouter) a la fin d'un mot
* `Ctrl + h` - delete the character before the cursor during insert mode
* `Ctrl + w` - delete word before the cursor during insert mode
* `Ctrl + j` - begin new line during insert mode
* `Ctrl + t` - indent (move right) line one shiftwidth during insert mode
* `Ctrl + d` - de-indent (move left) line one shiftwidth during insert mode
* `Ctrl + n` - insert (auto-complete) next match before the cursor during insert mode
* `Ctrl + p` - insert (auto-complete) previous match before the cursor during insert mode
* `Ctrl + rx` - insert the contents of register x
* `Ctrl + ox` - Entrez temporairement en mode normal pour émettre une commande de mode normal x.
* `Esc` - quitter le mode insertion

### Éditer

* `r` - remplacer un caractère
* `R` - replace more than one character, until ESC is pressed.
* `J` - joindre la ligne suivante à la ligne en cours en ajoutant un espace
* `gJ` - joindre la ligne suivante à la ligne en cours sans ajouter d'espace
* `gwip` - reflow paragraph
* `g~` - switch case up to motion
* `gu` - change to lowercase up to motion
* `gU` - change to uppercase up to motion
* `cc` - changer (remplacer) une ligne entière
* `C` - changer (remplacer) jusqu'à la fin de la ligne
* `c$` - changer (remplacer) jusqu'à la fin d'une ligne
* `ciw` - changer (remplacer) un mot entier
* `cw or ce` - changer (remplacer) jusqu'à la fin d'un mot
* `s` - supprimer un caractère et le remplacer par du texte
* `S` - supprimer une ligne et la remplacer par du texte (comme cc)
* `xp` - transposer deux lettres (supprimer et coller)
* `u` - annuler
* `U` - restore (undo) last changed line
* `Ctrl + r` - rétablir
* `.` - répéter la commande précédente

### Marquer du texte (mode visuel)

* `v` - passer en mode visuel, marquer du texte, exécuter des commandes (comme y)
* `V` - passer en mode visuel ligne par ligne
* `o` - se déplacer à l'autre extrémité de la zone marquée
* `Ctrl + v` - passer en mode visuel par bloc
* `O` - se déplacer à l'autre angle du bloc
* `aw` - marquer un mot
* `ab` - marquer un bloc avec ()
* `aB` - marquer un bloc avec {}
* `at` - a block with <> tags
* `ib` - marquer par bloc le contenu de ()
* `iB` - marquer par bloc le contenu de {}
* `it` - inner block with <> tags
* `Esc` - quitter le mode visuel

**Tip** Instead of b or B one can also use ( or { respectively.

### Commandes du mode visuel

* `>` - décaler le texte vers la droite
* `<` - décaler le texte vers la gauche
* `y` - copier le texte marqué
* `d` - supprimer le texte marqué
* `~` - modifier la casse
* `u` - change marked text to lowercase
* `U` - change marked text to uppercase

### Registres

* `:reg[isters]` - afficher le contenu des registres
* `"xy` - copier dans le registre X
* `"xp` - coller le contenu du registre X
* `"+y` - yank into the system clipboard register
* `"+p` - paste from the system clipboard register

**Tip** Les registres sont stockés dans \~/.viminfo, et seront encore chargé au prochain démarrage de vim.**Tip** Special registers:

 `0` - last yank\
`"` - unnamed register, last delete or yank\
`%` - current file name\
`#` - alternate file name\
`*` - clipboard contents (X11 primary)\
`+` - clipboard contents (X11 clipboard)\
`/` - last search pattern\
`:` - last command-line\
`.` - last inserted text\
`-` - last small (less than a line) delete\
`=` - expression register\
`_` - black hole register\\

### Marques

* `:marks` - lister des marques
* `ma` - définir la position actuelle pour la marque A
* `` `a `` - accéder à la position de la marque A
* ``y`a`` - copier le texte à la position de la marque A
* `` `0 `` - go to the position where Vim was previously exited
* `` `" `` - go to the position when last editing this file
* `` `. `` - go to the position of the last change in this file
* ` `` ` - go to the position before the last jump
* `:ju[mps]` - list of jumps
* `Ctrl + i` - go to newer position in jump list
* `Ctrl + o` - go to older position in jump list
* `:changes` - list of changes
* `g,` - go to newer position in change list
* `g;` - go to older position in change list
* `Ctrl + ]` - jump to the tag under cursor

**Tip** To jump to a mark you can either use a backtick (\`) or an apostrophe ('). Using an apostrophe jumps to the beginning (first non-blank) of the line holding the mark.

### Macros

* `qa` - enregistre la macro a
* `q` - arrêter l'enregistrement de la macro
* `@a` - exécuter la macro a
* `@@` - re-exécuter la dernière macro executée

### Copier-coller

* `yy` - copier une ligne
* `2yy` - copier 2 lignes
* `yw` - copier un mot
* `yiw` - copier le mot sous le curseur
* `yaw` - copier le mot sous le curseur avec l'espace après ou avant
* `y$` - copier jusqu'à la fin de la ligne
* `p` - coller le presse-papier après le curseur
* `P` - coller le presse-papier avant le curseur
* `gp` - put (paste) the clipboard after cursor and leave cursor after the new text
* `gP` - put (paste) before cursor and leave cursor after the new text
* `dd` - supprimer (couper) une ligne
* `2dd` - supprimer (couper) 2 lignes
* `dw` - supprimer (couper) un mot
* `diw` - supprimer (couper) un mot sous le curseur
* `daw` - supprimer (couper) un mot avec l'espace après ou avant
* `D` - supprimer (couper) jusqu'à la fin de la ligne
* `d$` - supprimer (couper) jusqu'à la fin de la ligne
* `x` - supprimer (couper) un caractère

### Indent text

* `>>` - indent (move right) line one shiftwidth
* `<<` - de-indent (move left) line one shiftwidth
* `>%` - indent a block with () or {} (cursor on brace)
* `>ib` - indent inner block with ()
* `>at` - indent a block with <> tags
* `3==` - re-indent 3 lines
* `=%` - re-indent a block with () or {} (cursor on brace)
* `=iB` - re-indent inner block with {}
* `gg=G` - re-indent entire buffer
* `]p` - paste and adjust indent to current line

### Quitter

* :w - écrire (sauver) le fichier
* :w !sudo tee % - écrire (sauver) le fichier en utilisant sudo
* :wq or :x or ZZ - écrire (sauver) et quitter
* :q - quitter (échoue s'il y a des modifications non sauvegardées)
* :q! or ZQ - quitter et abandonner les modifications non sauvegardées
* :wqa - écrire (sauver) et fermer tous les onglets

### Rechercher et remplacer

* /pattern - chercher le motif
* ?pattern - chercher en arrière le motif
* \vpattern - motif 'très magique': les caractères non alphanumériques sont interprétés comme des caracètres spéciaux regex (pas besoin d'échapper)
* n - répéter la recherche dans la même direction
* N - répéter la recherche dans la direction opposée
* :%s/old/new/g - remplacer toutes les occurrences de old avec new dans tout le fichier
* :%s/old/new/gc - remplacer toutes les occurrences de old avec new dans tout le fichier (demande confirmation)
* :noh\[lsearch] - supprime le surlignage du résultat des recherches

### Rechercher dans plusieurs fichiers

* :vim\[grep] /pattern/ {\`{file}\`} - rechercher un motif dans plusieurs fichiers

e.g. :vim\[grep] /foo/ \*\*/\*

* :cn\[ext] - atteindre le prochain résultat
* :cp\[revious] - atteindre le précédent résultat
* :cope\[n] - ouvre une fenetre contenant une liste des resultats
* :ccl\[ose] - close the quickfix window

### Onglets

* :tabnew or :tabnew {page.words.file} - ouvrir un fichier dans un nouvel onglet
* Ctrl + wT - déplacer la fenêtre en cours dans son propre onglet
* gt or :tabn\[ext] - aller à l'onglet suivant
* gT or :tabp\[revious] - aller à l'onglet précédent
* \#gt - aller à l'onglet #
* :tabm\[ove] # - déplacer l'onglet à la position # (commence à 0)
* :tabc\[lose] - fermer l'onglet en cours et toutes ses fenêtres
* :tabo\[nly] - fermer tous les onglets sauf l'onglet courant
* :tabdo command - exécute la `commande` sur tout les onglets (ex: `:tabdo q` - ferme tout les onglets ouverts)

### Travailler avec plusieurs fichiers

* :e\[dit] file - modifier un fichier dans un nouveau tampon
* :bn\[ext] - aller au tampon suivant
* :bp\[revious] - aller au tampon précédent
* :bd\[elete] - supprimer un tampon (fermer le fichier)
* :b\[uffer]# - go to a buffer by #
* :b\[uffer] file - go to a buffer by file
* :ls or :buffers - liste tout les tampons ouverts
* :sp\[lit] file - ouvrir un fichier dans un nouveau tampon et diviser la fenêtre
* :vs\[plit] file - ouvrir un fichier dans un nouveau tampon et diviser la fenêtre verticalement
* :vert\[ical] ba\[ll] - edit all buffers as vertical windows
* :tab ba\[ll] - edit all buffers as tabs
* Ctrl + ws - diviser la fenêtre
* Ctrl + wv - diviser la fenêtre verticalement
* Ctrl + ww - changer de fenêtre
* Ctrl + wq - fermer la fenêtre
* Ctrl + wx - exchange current window with next one
* Ctrl + w= - make all windows equal height & width
* Ctrl + wh - déplacer le curseur vers la fenêtre de gauche (division verticale)
* Ctrl + wl - déplacer le curseur vers la fenêtre de droite (division verticale)
* Ctrl + wj - déplacer le curseur vers la fenêtre en dessous (division horizontale)
* Ctrl + wk - déplacer le curseur vers la fenêtre au dessus (division horizontale)
* Ctrl + wH - make current window full height at far left (leftmost vertical window)
* Ctrl + wL - make current window full height at far right (rightmost vertical window)
* Ctrl + wJ - make current window full width at the very bottom (bottommost horizontal window)
* Ctrl + wK - make current window full width at the very top (topmost horizontal window)

### Diff

* zf - manually define a fold up to motion
* zd - delete fold under the cursor
* za - toggle fold under the cursor
* zo - open fold under the cursor
* zc - close fold under the cursor
* zr - reduce (open) all folds by one level
* zm - fold more (close) all folds by one level
* zi - toggle folding functionality
* ]c - jump to start of next change
* \[c - jump to start of previous change
* do or :diffg\[et] - obtain (get) difference (from other buffer)
* dp or :diffpu\[t] - put difference (to other buffer)
* :diffthis - make current window part of diff
* :dif\[fupdate] - update differences
* :diffo\[ff] - switch off diff mode for current window

**Tip** The commands for folding (e.g. za) operate on one level. To operate on all levels, use uppercase letters (e.g. zA).**Tip** To view the differences of files, one can directly start Vim in diff mode by running vimdiff in a terminal. One can even set this as git difftool.lobal

* :h\[elp] keyword - ouvrir l'aide pour le mot clé
* :sav\[eas] file - sauvegarder un fichier sous
* :clo\[se] - fermer le fichier en cours
* :ter\[minal] - open a terminal window
* K - ouvre la page du manuel (man) du mot sous le curseur

**Tip** Run vimtutor in a terminal to learn the first Vim commands.
