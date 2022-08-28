
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
- For more datails or more commands `click above`
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
- `echo` - used for displaying a messege or appending a string to files
    
    `echo "Display this"` or `echo "append this into" >> file.txt`

- `alias` - a shortform for a command
    
    `alias d=docker` - now we can use any docker commands with just `d`
- `id` - gives the pid, uid, and different id of current user
- `cat /etc/passwd` -  gives UID
- `lscpu`, `lsmem` gives cpu and disk info resp.
- `cp 1.txt copy.txt` - used to copy a file
- `mv name.txt renamed.txt` - used to rename a file
- `ps` - used to list all running flags, can be used by different flags
    - `ps aux` - list all running process
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
Deleting a user
```bash
# delete the user from machine
userdel dipanshu

# delete a user from a group
gpasswd -d <username> <groupname>
```



## Vim Editor
- `INSERT` - we can write text in `INSERT` mode. This mode is accessed by `i` or `insert` key
- We use `esc` to change to exit from a mode.
- We can copy and paste in `VISUAL`mode. accessed via `v` key while command mode.
- In command mode
    - `:q` - quit
    - `:q!` - quit without saving
    - `:wq` / `:x` - write and quit

## Linux Services
- `ps aux` is used to list running procees
- We can grab a specific procees by `pgrep <processname>`
- We can kill a process by using the PID obtained by above comand and `kill <PID>`
- `htop` - see running with cpu usage
- `jobs` - see the foregrounds process you stop
- `ps -auxw | grep systemd` - systemd is the first process to run with PID = 1
- `systemctl` - through this command we can stop, start any Services. It is the system manager for linux.