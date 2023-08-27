---
title: Linux Cheat Sheet

date: 2023-08-27
type: page
categories:
    - Linux
tags:
    - Tips and tricks
---

## System

### Keyboard shortcuts
I've been using Linux distribution for some time and along the way I found out few neat little trick that help me work with terminal efficiently.

Shortcut | Function
--- | ---
Ctrl + l | Clear the terminal screen, similar to clear command.
Ctrl + d | Close the shell, similar to exit command.
Ctrl + a | Move cursor to the beginning of the line.
Ctrl + e | Move cursor to the back end of the command.
Ctrl + u | Delete all character before the cursor, similar to **BACKSPACE**.
Ctrl + k | Delete all character after the cursor.
Ctrl + Left / Right Arrow | Move cursor to the start and end of the word.
Ctrl + c | Interrupt or stop the current running process in the terminal.
Ctrl + z | Suspend or pause the current running process in the terminal. Use `bg %1` to resume the process.
Ctrl + p | Similar to Up Arrow, go to the previous command in the command history.
Ctrl + n | Similar to Down Arrow, go to the next command in the command history.
Ctrl + r | Search for bash history in reverse, find the desired command, press **ENTER** ro run it.
Ctrl + g | Leave the history searching mode and clear the line.
! + <command> | Run the last command that you typed, e.g: `!sudo`. Careful when using this because you don't know exactly how the command was executed.
! + <command> + :p | Append `:p` and bash will print out the command to the terminal without running it. This is useful to confirm that you've selected the correct command before running it.