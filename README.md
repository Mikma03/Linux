# Linux


# Table of content

- [Introduction](#introduction)

- [Resources](#resources)

- [Linux Operating System - Crash Course](#linux-operating-system---crash-course)

- [Examining Linux in a Network Automation Context](#examining-linux-in-a-network-automation-context)

- [Notes and introduction](#notes-and-introduction)

# Introduction


# Resources

- WSL2 Ubuntu GUI
    - https://www.youtube.com/watch?v=IL7Jd9rjgrM&list=PLhfrWIlLOoKNMHhB39bh3XBpoLxV3f0V9&index=7

- Installing Ubuntu 20.04 LTS
    - https://www.youtube.com/watch?v=fLiZxubnBFs

- Linux as app on Windows 10/11
    - https://www.youtube.com/watch?v=4emmQuY25aY

# Linux Operating System - Crash Course

- https://www.youtube.com/watch?v=ROjZy1WbCIA

# Examining Linux in a Network Automation Context

- https://learning.oreilly.com/library/view/network-programmability-and/9781491931240/ch03.html#idm139936295705504

# Notes and introduction to Linux

## Navigating the Filesystem


Linux uses what’s known as a single-root filesystem, meaning that all of the drives and directories and files in a Linux installation fall into a single namespace, referred to quite simply as /. (When you see / by itself, say “root” in your head.) This is in stark contrast to an OS like Microsoft Windows, where each drive typically has its own root (the drive letter, like C:\ or D:\). Note that it is possible to mount a drive in a folder under Windows, but the practice isn’t as common.


**EVERYTHING IS TREATED LIKE A FILE**


Linux follows in UNIX’s footsteps in treating everything like a file. This includes storage devices (which are treated as block devices), ports on the computer (like serial ports), or even input/output devices. Thus, the importance of a single-root filesystem—which encompasses devices as well as storage—becomes even greater.


Like most other OSes, Linux uses the concept of directories (known as folders in some other OSes) to group files in the filesystem. Every file resides in a directory, and therefore every file has a unique path to its location. To denote the path of a file, you start at the root and list all the directories it takes to get to that file, separating the directories with a forward slash. For example, the command ```ping``` is often found in the bin directory off the root directory. The path, therefore, to `ping` would be noted like this: /bin/ping.


In the bash shell, the tilde is a shortcut that refers to the user’s home directory. Each user has a home directory that is their personal location for storing files, programs, and other content for only that user. To make it easy to refer to one’s home directory, bash uses the tilde as a shortcut.


    mikma@DESKTOP-UPA4L3K:~$


1. The first part of the prompt, before the `@` symbol, tells you the current user (in this case, `mikma`).

2. The second part of the prompt, directly after the `@` symbol, tells you the current hostname of the system on which you are currently operating (in this case, `DESKTOP-UPA4L3K` is the hostname).

3. Following the colon is the current directory, noted in this case as ~ meaning that this user (`mikma`) is currently in his or her home directory.

4. Finally, even the `$` at the end has meaning—in this particular case, it means that the current user (`mikma`) does not have root permissions. The `$` will change to a hash sign (the `#` character, also known as an octothorpe) if the user has root permissions.


In situations like this where you need to determine the full path to your current location, bash offers the `pwd` (print working directory) command.

The `pwd` command simply returns the directory where you’re currently located in the filesystem (the working directory).

When you know where you are located in the filesystem, you can begin to move around the filesystem using the `cd` (change directory) command along with a path to a destination.

For example, if you were in your home directory and wanted to change into the bin subdirectory, you’d simply type cd bin and press Enter (or Return).


Note the lack of the leading slash here. This is because `/bin` and `bin` might be two very different locations in the filesystem:

- Using `bin` (no leading slash) tells bash to change into the bin subdirectory of the current working directory.

- Using `/bin` (with a leading slash) tells bash to change into the bin subdirectory of the root (/) directory.


To move up one level in the filesystem (for example, to move from /usr/local/bin/ to /usr/local/), you can use the `..` shortcut. Every directory contains a special entry, named `.. `(two periods), that is a shortcut entry for that directory’s parent directory (the directory one level above it). So, if your current working directory is /usr/local/bin, you can simply type `cd ..` and press Enter (or Return) to move up one directory.


All these examples are using relative paths—that is, paths that are relative to your current location. You can, of course, also use absolute paths—that is, paths that are anchored to the root directory. As we mentioned earlier, the distinction is the use of the forward slash (/) to denote an absolute path starting at the root versus a path relative to the current location. For example, if you are currently located in the root directory (/) and need to move to /media/cdrom, you don’t need the leading slash (because media is a subdirectory of /). You can type `cd media/cdrom` and press Enter. This will move you to /media/cdrom, because you used a relative path to your destination.


The notation `cd -` (using a hyphen after the `cd` command) tells bash to switch back to the last directory you were in before you switched to the current directory. (If you need a shortcut to get back to your home directory, just enter `cd` with no parameters.)

## Manipulating Files and Directories

To create files or directories, you’ll work with one of two basic commands: `touch`, which is used to create files, and `mkdir` (make directory), which is used—not surprisingly—to create directories.


The `touch` command just creates a new file with no contents (it’s up to you to use a text editor or appropriate application to add content to the file after it is created).

    touch config.txt

Here’s an equivalent command:

    touch ./config.txt

Every directory also has an entry noted by a single period (`.`) that refers to the current directory. Therefore, the commands `touch config.txt` and `touch ./config.txt` will both create a file named config.txt in the current working directory.


When you want to be sure that the file you’re referencing is the file in the current working directory, use `./` to tell bash you want the file in the current directory.

    touch /config.txt

The `mkdir` command is very simple: it creates the directory specified by the user.

    mkdir bin

This command creates a directory named bin in the current working directory. It’s different than this command (relative versus absolute paths!):

    mkdir /bin

Like most other Linux commands, `mkdir` has a lot of options that modify its behavior, but one you’ll use frequently is the `-p` parameter. When used with the `-`p` option, mkdir will not report an error if the directory already exists, and will create parent directories along the path as needed.

For example, let’s say you had some files you needed to store, and you wanted to store them in /opt/sw/network. If you were in the /opt directory and entered `mkdir` sw/network when the sw directory didn’t already exist, the `mkdir` command would report an error. However, if you simply added the `-p` option, `mkdir` would then create the sw directory if needed, then create network under sw. This is a great way to create an entire path all at once without failing due to errors if a directory along the way already exists

## Deleting files and directories**

Similar to the way there are two commands for creating files and directories, there are two commands for deleting files and directories. Generally, you’ll use the `rm` command to delete (remove) files, and you’ll use the `rmdir` command to delete directories.

To remove a file, you simply use `rm filename`. For example, to remove a file named config.txt in the current working directory, you’d use one of the two following commands:

    rm config.txt

or

    rm ./config.txt


To remove a directory, you use `rmdir` directory. Note, however, that the directory has to be empty; if you attempt to delete a directory that has files in it, you’ll get this error message:

    rmdir: failed to remove 'src': Directory not empty

When you use `rm -r` directory, though, bash will remove the entire directory tree. Note that, by default, `rm` isn’t going to prompt for confirmation — it’s simply going to delete the whole directory tree. No Recycle Bin, no Trash Can…it’s gone. (If you want a prompt, you can add the `-i` parameter.)

## Moving, copying, and renaming files and directories

When it comes to moving, copying, and renaming files and directories, the two commands you’ll need to use are `cp` (for copying files or directories) and `mv` (for moving and renaming files and directories).

To copy a file, it’s just `cp source destination`. Similarly, to move a file you would just use `mv source destination`. Renaming a file, by the way, is consider moving it from one name to a new name (typically in the same directory).

Moving a directory is much the same; just use `mv source-dir destination-dir`. This is true whether the directory is flat (containing only files) or a tree (containing both files as well as subdirectories).

Copying directories is only a bit more complicated. Just add the `-r` option, like `cp -r source-dir destination-dir`. This will handle most use cases for copying directories, although some less common use cases may require some additional options.


## Changing permissions

Linux permissions are built around a couple of key ideas:

- Permissions are assigned based on the user (the user who owns the file), group (other users in the file’s group), and others (other users not in the file’s group).

- Permissions are based on the action (read, write, and execute).

Here’s how these two ideas come together. Each of the actions (read, write, and execute) is assigned a value; specifically, read is set to `4`, write is set to `2`, and execute is set to `1`. (Note that these values correspond exactly to binary values.) To allow multiple actions, add the values for each underlying action. For example, if you wanted to allow both read and write, the value you’d assign is `6` (read = `4`, write = `2`, so read+write = `6`).

These values are then assigned to user, group, and others. For example, to allow the file’s owner to read and write to a file, you’d assign the value `6` to the user’s permissions. To allow the file’s owner to read, write, and execute a file, you’d assign the value `7` to the user’s permissions. Similarly, if you wanted to allow users in the file’s group to read the file but not write or execute it, you’d assign the value `2` to the group’s permissions. User, group, and other permissions are listed as an octal number, like this:

- 644 (user = read+write, group = read, others = read)

- 755 (user = read+write+execute, group = read+execute, others = read+execute)

- 600 (user = read+write, group = none, others = none)

- 620 (user = read+write, group = write, others = none)

You may also see these permissions listed as a string of characters, like `rxwr-xr-x`. This breaks down to the read (`r`), write (`w`), and execute (`x`) permissions for each of the three entities (user, group, and others). Here are the same examples as earlier, but written in alternate format:

- 644 = rw-r--r--

- 755 = rwxr-xr-w

- 600 = rw-------

- 620 = rw--w----

A couple of different Linux tools are used to view and modify permissions. The `ls` utility, used for listing the contents of a directory, will show permissions when used with the `-l` option, and is most likely the primary tool you’ll use to view permissions


To change or modify permissions, you’ll need to use the `chmod` utility. This is where the explanation of octal values (`755`, `600`, `644`, etc.) and the `rwxr-wr-w` notation (typically referred to as symbolic notation) comes in handy, because that’s how `chmod` expects the user to enter permissions. As with relative paths versus absolute paths, the use of octal values versus symbolic notation is really a matter of what you’re trying to accomplish:

- If you need (or are willing) to set all the permissions at the same time, use octal values. Even if you omit some of the digits, you’ll still be changing the permissions because chmod assumes missing digits are leading zeros (and thus you’re setting permissions to none).

- If you need to set only one part (user, group, or others) of the permissions while leaving the rest intact, use symbolic notation. This will allow you to modify only one part of the permissions (for example, only the user permissions, or only the group permissions).

Examples:

Set the bin directory in the current working directory to mode 755 (owner = read/write/execute, all others = read/execute):

    chmod 755 bin

Add read/write permissions to the user that owns the file config.txt in the current working directory, while leaving all other permissions intact:

    chmod u+rw config.txt

Here’s an even more complex example—this adds read/write permissions for the file owner, but removes write permission for the file group:

    chmod u+rw,g-w /opt/share/config.txt

The `chmod` command also supports the use of the `-R` option to act recursively, meaning the permission changes will be propagated to files and subdirectories (obviously this works only when you’re using `chmod` against a directory).

## Running Programs

In order to run a program, here’s what’s needed:

- A file that is actually an executable `file` (you can use the file utility to help determine if a file is executable)

- Execute permissions (either as the file owner, as a member of the file’s group, or with the execute permission given to others)

What makes up an “executable file”? It could be a binary file, compiled from a programming language such C or C++. However, it could also be an executable text file, such as a bash shell script (a series of bash shell commands) or a script written in a language like Python or Ruby. (We’ll be talking about Python extensively in the next chapter.) The `file` utility (which may or may not be installed by default; use your Linux distribution’s package management tool to install it if it isn’t already installed) can help here.

Every Linux system has a search path, which is a list of directories on the system that it will search when the user enters a filename. You can see the current search path by entering `echo $PATH` at your shell prompt.

    echo $PATH

To help with this potential gotcha when you have multiple programs with the same name, you can use the `which` command. For example, suppose you have a Python script named `uptime` that gathers uptime statistics from your network devices. Most Linux distributions also ship with a command called `uptime` (it displays information about how long the Linux system has been up and running). By typing `which uptime`, you can ask the Linux system to tell you the full path to the first `uptime `executable it found when searching the search path. (This is the one that would be executed if you just typed `uptime` at the prompt.)

## Working with Daemons

In the Linux world, we use the term daemon to refer to a process that runs in the background. (You may also see the term service used to describe these types of background processes.) Daemons are most often encountered when you’re using Linux to provide network-based functionality.

**Ubuntu**

The primary command you’ll use to interact with Upstart for the purpose of stopping, starting, restarting, or checking the status of background services (also referred to as “jobs” in the Upstart parlance) is `initctl`, and it is used in a fashion very similar to `systemctl`.

For example, to start a daemon you’d use `initctl `like this:

    initctl start service-name

Likewise, to stop a daemon you’d replace `start` in the previous command with `stop`, like this:

    initctl stop service-name

The `restart` and `status` subcommands to `initctl `work in much the same way. Here’s an example of restarting and checking the status of the VMware Tools daemon (VMware Tools is a background service often installed in VMware-based virtual machines):

    initctl restart vmware-tools

and

    initctl status vmware-tools

And, as with `systemctl`, there is a way to get the list of service names, so that you know the name to supply when trying to start, stop, or check the status of a daemon:

    initctl list


