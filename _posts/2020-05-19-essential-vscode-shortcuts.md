---
layout: post
title: 'Essential VSCode shorcuts'
date: 2020-05-18 22:55:55 +0900
categories: ide vscode
---

[Visual Studio Code](https://code.visualstudio.com/) is one of the most popular IDE's for web development these days and as with any IDE, knowing a few simple keyboard shortcuts can lessen frustration and improve your efficiency greatly. Here are what I consider the essential keyboard shortcuts you should know.

## The Basics

### Go to file

`Ctrl+P` `⌘P`

Opens up a handy file search dialog. Just type in a few characters of a file name or extension and matching files located within your project folder will be displayed. Then just click on the file you want to open it. This is much much faster than using your mouse to navigate the folder structure of your project, especially for larger projects with many files.

![Go to file](/assets/2020-05-19-essential-vscode-shortcuts/go-to-file.png)

### Show command palette

`Ctrl+Shift+P or F1` `⇧⌘P or F1`

Opens up a command palette giving you quick access to perform almost any action. The command palette looks very similar to the file search dialog except for the angled `>` bracket displayed as the first character (in fact from the file search dialog, manually typing in `>` will switch over to the command palette).

![Show command palette](/assets/2020-05-19-essential-vscode-shortcuts/command-palette.png)

It operates in much the same way as the file search dialog, just type in a few characters of the action you want to perform (for example Undo, Git commit, Toggle comments, Open a command terminal and so on) and matching actions will be displayed below.

The really great thing about the command palette is that it works for plugins as well, so for example if you have the **Remote SSH** plugin installed, entering `connect` will bring up a command to connect to a host.

### Toggle line comment / Toggle block comment

`Ctrl+/` `⌘/` / `Shift+Alt+A` `⇧⌥A`

Pretty self explanatory, place the cursor on the line you want to comment/uncomment and enter the shortcut.

For block comments, highlight the block of text first, then enter the shortcut to comment/uncomment the entire block.

### Show search

`Shift+Ctrl+F` `⇧⌘F`

While as is standard `Ctrl+F` `⌘F` will all you to find some specific text within the current file, this shortcut will open VSCode's powerful search panel, allowing you to search for text within any file in your entire project.

### Go back / forward

`Alt+ ← / →` `⌃- / ⌃⇧-`

Have you ever opened a file and then wanted to return to the file you were previously looking at but couldn't find an easy way to do it? The solution to this somewhat common issue is the go back / go forward shortcuts, allowing you to quickly navigate backward and forward through the files you had opened.

<!-- ### Open a new terminal

### Show markdown preview

## Getting a Little More Advanced

### Split terminal

### Navigate between split terminals

### Insert cursor

### Select all occurrences of current selection

### Select all occurrences of current word -->

{% include share-buttons.html %}
