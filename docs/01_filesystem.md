## What is a file system

Having read section 00 about binary and humans, a file system and disk format work together to allow programmers to store and access binary files without wasting space and also providing a fast experience to users.

The file system is a program which is alongside, and works with, the operating system.

We have discussed how a text file is just binary numbers in UTF8 or some other encoding. The file extension, the file name, who created the file, the size of the file... all of these details live in the file too. This sort of data is called metadata because it describes other data.

File systems organize files. Just like paper file systems and paper files. The file system is like a librarian. The actual storage format of the library is the disk format.

Here is a pragmatic characterisation of a disk format:
* They usually have an index which explains the partitions of the disk, and some metadata like "this partition is a boot partition"
* Partitions contain folders, which can contain files and other folders
* Partitions also usually have an index which allows fast lookup of files

> Some common disk formats are FAT, exFAT, NFTS but there are many.

> Sometimes folks just refer to all this file stuff as the file system (rather than differentiating the disk format and the file system)

> You can have multiple disks in your computure formatted with different formats, being accessed by the same file system.

### 1.1 File system organization

On linux you usually have something like this in your main disk:

```
/home/yourname (also known as your home, and affectionately "~" in bash)
/mnt (stuff like USB sticks)
/etc (system config)
/opt (system config)
/sys (system data)
/var (system config)
/dev/null (where you can write infinite bytes to throw them away)
/dev/ (lots of system information and i/o devices as file sockets)
/boot
```

When talking about paths `/` separates `<parent path>/<child path>` and if you specify no parent then you go to the root.

__Absolute Paths__

An absolute path is a path including the root. Basically in linux that means it starts with `/`.

> your current absolute path can obtained with `pwd` or `cwd` from the command line

__Relative Paths__

A relative path is a path _relative_ to the absolute path of your current working directory.

Suppose we have a file structure in our home with these files (remember ~ is /home/yourname to bash):
```
~/.bashrc
~/workspace/sample-project/README.md
~/workspace/sample-project/.gitignore
~/workspace/sample-project/src/index.sh
```

You could `cd ~/workspace` to make it your current directory. Some relative paths based on a current directory of `/home/yourname/workspace` are:

```
../ (parent directory)
../.bashrc
sample-project (implicitly ./)
./sample-project
./sample-project/.gitignore
./sample-project/src/index.js

../../../var (same var as "/var" in absolute pathing)
./../ (same as ../)
```

Some common bash examples for navigating the file system from a terminal:

* `ls` to view files in the current directory
* `cd <path>` to change to a directory
* execute a directory with `./<path>` to change to it.
* execute `index.sh` from `~` with `./workspace/sapmle-project/src/index.sh`
* delete a file `rm <path>`
* create a file with nothing in it `touch <path>`
* create a directory `mkdir <path>` 
  * (use mkdir -p to make a nested directory)
* use `rmdir` to delete an empty directory.
* use `rm -r` to delete all files and folders in a directory, as well as the directory
* use `cat` to read a file in the terminal as-if it were plaintext (even if it is not)

When a program runs, it chooses a path to refer to as its current working directory.

> In bash if you run a program, the directory your are currently in is the working directory

## Case sensitivity

Linux uses a case sensitive file system. Windows does not. Mac OS can, but by default does not.

This means the file system is blind to casing when accessing files.

## Permissions

If you run `ls -alch` in `~` on your linux machine, you will see a lot of interesting info about files. A lot of it relates to permissions.

Permissions is a deep topic, but generally speaking you only care if you can do these three things with a specific file or directory:
* read
* write
* execute

In my home, I have this file in my output
```
-rw-r--r--  1 sammons sammons 5.9K Oct  1 12:43 .bashrc
```

This means the owner has read/write access, and others have read access. Hmm maybe I should remove that permission from others!

You should get used to interpreting bash outputs on your own. I recommend googling stack exchange or stack overflow. Here's an example:
*  https://unix.stackexchange.com/questions/103114/what-do-the-fields-in-ls-al-output-mean