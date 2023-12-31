- [[#Intro to symbolic links|Intro to symbolic links]]
- [[#How to see which files are links?|How to see which files are links?]]


## Intro to symbolic links

A symbolic link, often referred to as a symlink or a soft link, is a special kind of file that points to another file or directory. This is a bit like a shortcut in Windows. It can point to a file or a directory on the same or different physical disk drive.

Symbolic links are used for a variety of purposes, including:

1. To create quick access to a deeply nested file or directory.
2. To provide a backward compatibility, i.e., keeping older file paths intact while the files are moved to a new location.
3. To reference files or directories on other partitions or disks.
4. To create shared files or directories among different users.

Here are a few examples of how you might create and use symbolic links:

**Example 1: Basic usage**

To create a symbolic link between an original directory and a link, you'd use the `ln` command with the `-s` option. For example, if you have a directory named `/var/www/mywebsite` and you want to create a symlink to this directory in your home directory, you'd use the following command:

```bash
ln -s /var/www/mywebsite ~/mywebsite_link
```

After this command, `mywebsite_link` in your home directory will serve as a shortcut to `/var/www/mywebsite`.

**Example 2: Symbolic link to a file**

If you have a configuration file, e.g., `config.txt` in the `/home/user/configs/` directory, and you often need to access this from your home directory, you can create a symlink as follows:

```bash
ln -s /home/user/configs/config.txt ~/config_link.txt
```

Now `config_link.txt` in your home directory will act as a shortcut to the `config.txt` file in the `configs` directory.

**Example 3: Invalid/dead symbolic link**

It's important to note that symbolic links are not updated if the original file or directory's location changes. If you create a symlink to a file or directory, and then you move or delete the original, the symlink will still exist, but it will be broken. For instance, if we delete `config.txt` from the previous example, `config_link.txt` will be a dead link.

It's also crucial to remember that the permissions on a symbolic link are not used. Instead, the operating system looks at the permissions on the target file. Therefore, changing the permissions on a symbolic link does not have any effect.

## How to see which files are links?

`ls -la` command, it will display all files, including hidden ones and symbolic links, in the long format.

The long format includes detailed information about the files and directories, including their permissions, the number of links, the owner, the group, the size, and the time of the last modification

Here's how to recognize a symbolic link in the output of `ls -la`:

- The first character of the permissions field will be `l` (which stands for 'link'). For regular files, it will be `-`, and for directories, it will be `d`.
- The filename of the symbolic link will be followed by `->` and then the path to the file or directory it points to.

For example:

```bash
lrwxrwxrwx 1 user group 18 Jun 18 14:34 mywebsite_link -> /var/www/mywebsite
```
In this line:

- `lrwxrwxrwx` are the permissions: `l` denotes a symbolic link, and `rwxrwxrwx` means that the owner, group, and others have read, write, and execute permissions.
- `1` is the number of links (always 1 for symbolic links).
- `user` is the owner of the file.
- `group` is the group owner of the file.
- `18` is the size of the file in bytes.
- `Jun 18 14:34` is the last modification time.
- `mywebsite_link -> /var/www/mywebsite` shows that `mywebsite_link` is a symbolic link that points to `/var/www/mywebsite`.


