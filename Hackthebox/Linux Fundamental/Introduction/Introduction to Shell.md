## Why learn the shell?
### Many servers especially web servers runs linux, not Windows, because linux trend to be more stable and less-error prone.
### To control these servers you need to master the shell --- Linux's command center.

## What is a Shell?
#### A shell is a text-based input/output (I/O) interface between users and the Linux kernel for computer system. You type command and tell the system what to do .
![[Pasted image 20260620133657.png]]
## Terminal Emulators 
### A terminal emulator lets you run text-based programs inside a graphical window (GUI).

#### CLI within a Terminal
#### You can even run a command-line interface inside another terminal — like having a small office inside a bigger office, each handling its own tasks.

### Terminal Multiplexers (e.g., Tmux)

A **multiplexer** lets you split one terminal into **multiple panes** — like dividing your office floor into separate desks, each working on different projects simultaneously.
![[Pasted image 20260620155440.png]]

Example from the text: a Tmux session with **3 panes**, each showing a different directory:

```
┌─────────────┬─────────────┬─────────────┐
│  BloodHound │  Impacket   │  SecLists   │
│  (files)    │  (files)    │  (files)    │
└─────────────┴─────────────┴─────────────┘
```
## Shell
The most commonly used shell in Linux is the `Bourne-Again Shell` (`BASH`), and is part of the GNU project.