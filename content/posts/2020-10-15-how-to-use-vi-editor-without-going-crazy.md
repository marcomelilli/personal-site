---
template: post
title: How to use vi editor without going crazy
slug: vi-basic-commands-cheat-sheet
draft: false
date: 2020-10-15T16:57:16.509Z
description: Start to use vi learning only the basic commands
category: linux
tags:
  - linux
---
Vi has two modes:

* **command** mode
* **insert** mode

In *command mode*, the letters of the keyboard perform editing functions (like moving the cursor, search, replace, copy and paste, etc..). In *insert mode* you can type the text like a classic editor. 

These are the most importart commands to learn:

**BASIC EDITING**

```
 i         insert mode
 ESC       terminate insert mode

 x         delete character
 X         delete character before cursor
 D         delete characters from cursor to end of line

 r         replace character under cursor
 cw        replace a word

 o         insert blank line below cursor (goes into insert mode)      
 O         insert blank line above cursor (goes into insert mode) 
 
 u         undo last change
 U         restore current line
```

**SEARCH**

```
 /         start search, enter the text to search for and press <Return>
 n         repeat last search in forward direction
 N         repeat last search in backward direction
```

**ADVANCED EDITING**

```
 nx        delete n characters
 dw        delete word
 ndw       delete n words
 dd        delete line
 ndd       delete n lines
 
 ncw       replace n words
 C         replace text from cursor to end of line (goes into insert mode)

 J         join succeeding line to current cursor line
 nJ        join n succeeding lines to current cursor line
```

**COPY AND PASTE**

```
v          begin character-based visual selection
V          select whole lines
Ctrl-v     select a block

<Move>     Move the cursor to the end of the text to be cut/copied

d          cut selected text
y          copy selected text

<Move>     Move the cursor to the desired paste location

p          paste after the cursor
P          paste before the cursor
```

**MOVING AROUND IN A FILE**

```
 w            forward word by word
 b            backward word by word
 $            to end of line
 0 (zero)     to beginning of line
 H            to top line of screen
 M            to middle line of screen
 L            to last line of screen
 G            to last line of file
 1G           to first line of file
 <Ctrl>f      scroll forward one screen
 <Ctrl>b      scroll backward one screen
 <Ctrl>d      scroll down one-half screen
 <Ctrl>u      scroll up one-half screen
```

**CLOSING AND SAVING A FILE**

```
 ZZ            save file and then quit
 :w            save file
 :q!           discard changes and quit file
```