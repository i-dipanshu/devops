
# Linux

Linux is a free open source operating system.

## Basic info

- **Operating system:** intermediary between the applications and the hardware running on your local machine.

    An OS can have GUI or not but usually servers don't have it.

- **KERNEL:** System software which takes command from us and gets the hardware to do it. 

    The `variation in kernel is distro` like ubuntu, fidora and many others

- **GNU:** extensive collection of free software that can be used as operating System

- **Shells:** command language interpreter like `bash, zhc etc.`


## File System
-  `/home` - contains the files related to user and user itself.
- `/bin` - contains all the command binaries like `cat, echo etc`
- `/sbin` - contains system binaries and needs `sudo` 
- `/usr` - user
- `/usr/bin` - contains primary executables that system need to run
- `/usr/local` - files specific to user
- `/lib` - additional libararies for `/bin`
- `/var` - temporary data
- `/var/log` - logs here are stored for 30 days
- `/var/log/sylog` - contains system logs
- `/var/cache` - cached data from programs
- `/opt` - programs that install in one directory not in multiple like `/lib` and `/bin`
- `/etc` - contains system-wide configuration files
- `/etc/fstab` - different fileststem are treated when introduced to System
- `/etc/hostname` - contains the name of system
- `/etc/hosts` - changes hostname to ip-address
- `/etc/sudoers` - contains file about sudo users
- `/tmp` - temporary running process
- `/boot` - contains file to boot the system 
- `/dev` - devices config files like mouse, keyboard etc.
- `/media` - external devices automounts here
- `/mnt` - temporary mountpoints for additional filesystem
## [Basic Commands](https://command-not-found.com/)
- `pwd` - present working directory
- `cd <path> ` - changes directory to specified path  
- `ls <path>` - list the files in directory, it can have flags like `ls -a` for listing hidden file and `ls -al` for detailed listing
- `mkdir <foldername>` - makes a new folder in the directory
- `touch <filename>` - creates a new file 
- `vim <filename>` - opens the file in vim editor
- `cat <filename/path>` - displays the content of the file. 

    We can use pipes to view accordingly, like `cat demo.txt | less` displays line by line.

    We can also `grep` flags to highlight and serch for specific words like `cat demo.txt | grep error`
- `find / -name 'syslog'` - template for finding syslog
- `man <command>` - to open a manual about any command
- `echo` - 

## Creating a new user adding to new group

Check the default shell

```bash
useradd -D
```

Change the default shell from bourne to bourne again shell

```bash
useradd -D -s /bin/bash
echo $SHELL
```

Add new user

```bash
useradd -m dipanshu
```

Create a password for user

```bash
passwd dipanshu
```

Add the user to `sudo` group

```bash
usermod -aG sudo dipanshu
```

Switch to the user

```bash
su - dipanshu
```

Create and add to new group

```bash
# create a new group
sudo groupadd <groupname>

# get info about group
getent group <groupname>

# add our user to group
sudo usermod -aG <username> $USER

# check groups for the user
groups dipanshu

```



