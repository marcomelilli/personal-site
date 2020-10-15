---
template: post
title: How to use vi editor without going crazy
slug: vi-basic-commands-cheat-sheet
draft: true
date: 2020-10-15T16:57:16.509Z
description: How to use vi editor cheat sheet
category: linux
tags:
  - linux
---
vi has two modes:

* command mode
* insert mode

In command mode, the letters of the keyboard perform editing functions (like moving the cursor, deleting text, etc.). To enter command mode, press the escape <Esc> key.

* **i** - insert mode
* **esc** - terminate insert mode.
* **u** - Undo last change.
* **o** - Open a new line (goes into insert mode)

To cut-and-paste or copy-and-paste:

Position the cursor at the beginning of the text you want to cut/copy.
Press v to begin character-based visual selection, or V to select whole lines, or Ctrl-v or Ctrl-q to select a block.
Move the cursor to the end of the text to be cut/copied. While selecting text, you can perform searches and other advanced movement.
Press d (delete) to cut, or y (yank) to copy.
Move the cursor to the desired paste location.
Press p to paste after the cursor, or P to paste before.


Replacing Characters
To replace one character with another:

Move the cursor to the character to be replaced.
Type r
Type the replacement character.
The new character will appear, and you will still be in command mode.
Moving by Searching
To move quickly by searching for text, while in command mode:

Type / (slash).
Enter the text to search for.
Press <Return>.
The cursor moves to the first occurrence of that text.

To repeat the search in a forward direction, type

     n
To repeat the search in a backward direction, type
BASIC EDITING

     x         delete character
     nx        delete n characters
     X         delete character before cursor
     dw        delete word
     ndw       delete n words
     dd        delete line
     ndd       delete n lines
     D         delete characters from cursor to end of line
     r         replace character under cursor
     cw        replace a word
     ncw       replace n words
     C         change text from cursor to end of line
     o         insert blank line below cursor
                  (ready for insertion)
     O         insert blank line above cursor
                  (ready for insertion)
     J         join succeeding line to current cursor line
     nJ        join n succeeding lines to current cursor line
     u         undo last change
     U         restore current line
MOVING AROUND IN A FILE

     w            forward word by word
     b            backward word by word
     $            to end of line
     0 (zero)     to beginning of line
     H            to top line of screen
     M            to middle line of screen
     L            to last line of screen
     G            to last line of file
     1G           to first line of file
     <Control>f   scroll forward one screen
     <Control>b   scroll backward one screen
     <Control>d   scroll down one-half screen
     <Control>u   scroll up one-half screen
     n            repeat last search in same direction
     N            repeat last search in opposite direction
CLOSING AND SAVING A FILE

     ZZ            save file and then quit
     :w            save file
     :q!            discard changes and quit file

