## What is Linux?
### Linux is an operating system(OS) , Software that acts as a middleman between you and your computer's hardware. Just like a city mayor manages roads, water, electricity for everyone , the OS manages your CPU , RAM and Storage for all your programs.

>Windows and macOS do the same job ---- Linux is just a different "City" with its own rules and cultures.
## Linux Philosophy (IT "Culture")

- Linux Follows 5 core principles :

| **Principle**                 | **Description**                                                      | Example                                      |
| ----------------------------- | -------------------------------------------------------------------- | -------------------------------------------- |
| Everything is a file          | Hardware ,<br>processes, <br>connection -- all<br>treated as  files. | Your USB drive appears as `/dev/sdb`.        |
| Small, single-purpose program | Each tool does one thing well.                                       | `ls` only lists files. Nothing else.         |
| Chain programs together       | Combine small tools to do big things.                                | `ls \| grep ".txt"` -- list only .txt files. |
| Avoid locked-in interfaces    | Prefer the terminal over the clicking the menus.                     | You can automate anything via scripts.       |
| Config stored in text files   | Settings are readable, editable plain text.                          | `/etc/passwd` stores user accounts.          |
## Linux Components (The City Departments)

| Components               | City Analogy                | Description                                                                                                                |
| ------------------------ | --------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Bootloader               | The alarm clock             | A piece of code that guide the booting process to start the operating system. Parrot OS Linux uses the **GRUB Bootloader** |
| OS Kernel                | The mayor's office          | Controls all hardware resources --CPU, memory, device.                                                                     |
| Daemons                  | Background city worker.     | Run silently in the background (e.g : print services, audio ).                                                             |
| OS Shell                 | The telephone to the mayor. | You type command here; it talk to the kernel (e.g : Bash , Tcsh/Csh, Ksh, Zsh, and Fish).                                  |
| Graphic Server (X)       | The city's display boards.  | Let's graphical app shows windows  on your screen.                                                                         |
| Window Manager <br>(GUI) | The city 's look and feel.  | GNOME , KDE ,MATE , Unity and Cinnamon --what you seen on and click on.                                                    |
| Utilities                | Specialized shops           | Applications or utilities are programs that perform particular functions for the user or another program.                  |
## Linux Architecture 
![[Pasted image 20260619221600.png]]
##  File System Hierarchy
- Linux stores everything in one big tree starting at `/` (called **root** — the top of the tree). Here are the most important "neighbourhoods":

| Path     | Description                                                                                                                                               |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/`      | The top-level directory is the root filesystem and contains all the files required to bootloader an operating system before other filesystem are mounted. |
| `/home`  | Each user on the system has the subdirectory here for storage.                                                                                            |
| `/etc`   | Configuration files or installed application may be saved here as well.                                                                                   |
| `/bin`   | Essential commands (ls, cp) binaries.                                                                                                                     |
| `/var`   | Log files, emails, web data                                                                                                                               |
| `/tmp`   | Temporary files (wiped on reboot)                                                                                                                         |
| `/dev`   | Everything is treated as the file including hardware                                                                                                      |
| `/root`  | Home folder for the admin user                                                                                                                            |
| `/boot`  | Consist of static bootloader, kernel executable and files require to boot the Linux OS.                                                                   |
| `/lib`   | Shared library files that are required for system boot.                                                                                                   |
| `/media` | External removable media  devices such as USB drivers are mounted here.                                                                                   |
| `/mnt`   | Temporary mount point for regular  filesystems.                                                                                                           |
| `/opt`   | Options files such as third party tools can be saved here.                                                                                                |
| `/sbin`  | This directory contains executable used for system administration (binary system files).                                                                  |
| `/usr`   | Contains executable , libraries, man files ,etc.                                                                                                          |
