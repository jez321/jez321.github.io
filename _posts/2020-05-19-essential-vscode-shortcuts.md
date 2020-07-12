---
layout: post
title: 'Essential VSCode shorcuts'
date: 2020-05-19 23:59:30 +0900
categories: ide vscode
---

[Visual Studio Code](https://code.visualstudio.com/){:target="\_blank"} is one of the most popular IDE's for web development these days and as with any IDE, knowing a few simple keyboard shortcuts can lessen frustration and improve your efficiency greatly. Here are what I consider the essential keyboard shortcuts you must know.

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

While as is standard `Ctrl+F` `⌘F` will allow you to find some specific text within the current file, this shortcut will open VSCode's powerful search panel, allowing you to search for text within any file in your entire project.

### Go back / forward

`Alt+ ← / →` `⌃- / ⌃⇧-`

Have you ever opened a file and then wanted to return to the file you were previously looking at but couldn't find an easy way to do it? The solution to this somewhat common issue is the go back / go forward shortcuts, allowing you to quickly navigate backward and forward through the files you had opened.

### Show terminal

`` Ctrl+` `` `` ⌃` ``

The terminal in VSCode quite handy for running all kinds of commands such as git, starting up the development server and so on.
This command will bring it up, ready for input.

### Split terminal

`Shift+Ctrl+5` `⇧⌘F`

You can never have too many terminals, this command will create another terminal side by side the existing one(s), displaying them in columns.
I prefer this to having them as competely separate windows so I can see what's going on in all of them at once. The columns can make things a little cramped but 3 or 4 shouldn't really be a problem for general terminal duties on a decently wide screen.

### Open markdown preview to the side

`Ctrl+K V` `⌘K V`

_Note: The space means press the first key combination, release it, and then press the second key._

If you're writing documentation or even just a simple Readme file, you will very likely need to write in markdown.
If this is the case and especially if you are still a relative beginner, being able to visually check the output of your .md in real time while you write is a huge help.

![Markdown preview](/assets/2020-05-19-essential-vscode-shortcuts/markdown-preview.png)

## Getting a Bit More Advanced With Multiple Cursors

Multiple cursors is something many programmers don't use, but once you get used to them, you'll start to realize when you come across situations where they are useful and get nice boost to your coding efficiency.
By placing multiple cursors throughout your code, you can perform the same modifications on multiple locations simultaneously, greatly cutting down on the time needed to perform repetitive edits.

### Insert cursor

`Alt+Click` `⌥ + Click`

The most basic incarnation, simply hold down `Alt` or `⌥` and click anywhere to create a new cursor there.

### Select all occurrences of current selection

`Ctrl+Shift+L` `⇧⌘L`

Select a piece of text, then input this shortcut to also select all other pieces of matching text within the file.

### Select all occurrences of current word

`Ctrl+F2` `⌘F2`

This shortcut allows you to simplely place your cursor somewhere on a word, and then select all identical words within the file.

![Select all occurrences of current word](/assets/2020-05-19-essential-vscode-shortcuts/multiple-word.gif)

## In Closing

I hope you learnt a couple of new shortcuts and they help to make your coding more efficient and more importantly more enjoyable!
Don't forget you can always input `Ctrl+K Ctrl+S` `⌘K ⌘S` to display the full list of available VSCode shortcuts as well.

{% include share-buttons.html %}
