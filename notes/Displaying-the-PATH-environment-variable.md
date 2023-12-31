<!-- TOC -->

- [Introduction](#introduction)
- [Explanation](#explanation)
- [Output](#output)

<!-- /TOC -->


#### Introduction

The PATH environment variable is a system variable that's used to specify the directories where executable programs are located. It's important for the operating system to know the location of executables.

In Unix or Linux-based systems, directories in the PATH are separated by colons (`:`). It can sometimes be challenging to read the PATH when it's printed out in this manner.

The following command breaks down the PATH into a more readable format, displaying each directory on a separate line and adding line numbers for clarity.

```
echo $PATH | tr ':' '\n' | awk '{print NR "\t" $0}'
```

#### Explanation

This command works in three steps, separated by the pipe (`|`) character:

1. `echo $PATH`: This command prints the value of the PATH variable.
    
2. `tr ':' '\n'`: The `tr` command is used for translating or deleting characters. In this case, it's translating each colon (`:`) into a newline character (`\n`). This effectively separates each directory in the PATH onto its own line.
    
3. `awk '{print NR "\t" $0}'`: `awk` is a programming language that's often used for text processing. Here, it's used to print two values: `NR` (which represents the line number or "record number") and `$0` (which represents the entire line). These two values are separated by a tab character (`\t`), which creates a two-column table-like output. The first column is the line number and the second column is the corresponding directory in the PATH.

#### Output

The output will look something like this:

```
1       /usr/local/sbin
2       /usr/local/bin
3       /usr/sbin
4       /usr/bin
5       /sbin
6       /bin
7       /usr/games
8       /usr/local/games
9       /snap/bin
```

This output is a table-like representation of the PATH variable. The first column is the line number and the second column is the directory.

