## What even am I doing in this black box thing?

Lets get some things straight, the operating system runs programs (we'll talk about that more in the next section) and those programs can run other programs... and so on.

There are two programs to make the whole black-hacker-square-experience:
* What you see and type into, and presentation of feedback to you (Terminal)
* The interpretation of things you type. (Shell)

The visual program is a `terminal`, the interpreter is _a_ `shell`. There are many shells, `zsh`, `sh`, and `bash` are some common ones. Windows uses `powershell`.

The linux-ey shells `sh`, `zsh`, and `bash` can be hard to differentiate when you are going about your business with `cd` and `ls` and typical shell commands, but they have some small differences I will not go into.

So to recap: The terminal launches a shell, which eats your commands. The output from the shell is presented back to you by the terminal.

On linux the terminal program is usually literally called "Terminal" but you can get others.

## There is a difference between shell commands and shell scripting

You can write shell scripts and put them in files, usually ending with `.sh`, since the file extension isn't precise enough folks usually put this line at the top of their files which explains to shells what program to _really_ use to run the file

For example a file named `myscript.sh` with the following contents:

```
#!/bin/sh
echo "HI"
```

Would tell a `bash` shell to run it using the `/bin/sh` program instead of `bash`.

__Shell scripting supports if-statements, while loops, for-loops and variables just like other programming languages!__

[shellscript.sh website](https://www.shellscript.sh/) for learning more about shell scripting.


So everything you write that a shell can run is a shell script, but shell scripts commonly use executable programs designed for use with shell to actually do things.

Some common programs:
* ls
* cd
* mkdir
* cp
* rm
* ssh
* cat
* head
* tail
* wc
* ps
* kill
* git

The list goes on! When you write a program like this, it is usually called a "CLI" or command line interface.

Most programs and compilers provide CLI commands to compile and run code. For example the command `python` is a program, and when you run it in the terminal you are using your shell to execute it.

## Inputs and outputs, and CLI behavior

In linux there are a few ways for every program to give feedback to whoever ran it, and for the program running it to give some instructions:
* stdin: text that the parent program can input
* stderr: conventionally error text that the program can respond with
* stdout: conventionally informational or useful text that the program can respond with
* return signals: failed processes return non-zero exit codes, and successful processes return 0 on completion
* input signals: numeric signals from parent processes which can e.g. tell a program to exit early.

This is a bit confusing, so here are some pertinent examples:

* when you `println` in python, or `console.log` in node.js, or `echo` in your shell, that is going to the stdout
* when you `kill -9 <pid>` you sent a signal to that process
* if you run `cd ~/mydir && echo success` your shell will not echo success if `cd` failed and returned something besides zero.

__Piping__

In linux we use the `|` (pipe) to direct the `stdout` from one program into the `stdin` of another program.

For example:

`cat somefile | wc -l` 

Will direct the `cat` output into `wc`, which will process that and tell us the number of lines in `somefile`.

You can chain these together infinitely and have an equally infinite number of regrets. Ha.

__Writing output to files__

Another common thing to do is to do `>` to write a file, and `>>` to append a file. Some examples:

```
echo *.zip >> .gitignore
echo {} > package.json
python myprogram.py > log.txt # redirects your println/log scripts to a log.txt file
```

> Typically stderr is not captured with `>`, you can do `&2>` to catch it as well (1 is stdout)

## Command Flags

By convention programs in linux use hyphens for config parameters. They are often called flags if they trigger behavior by existing. You never write `ls -h=true`, and instead just include `-h` to trigger that flag. If you don't want `-h` behavior you leave it out.

Flags can often be combined, for example: `ls -a -l -c -h` is the same as `ls -alch`

Options can have a specific value. For example with curl (a utility to make web requests) `curl google.com -o=out.html` will set the `o` parameter to be `out.html`. 

The `=` with options is often optional, for example
`curl google.com -o out.html` has exactly the same behavior.

Often the single hyphen options can be more explicitly expressed, again with curl:
`curl google.com --output out.html`

## Sudo

You will read that sudo is bad. That is not always true.

The `sudo` program changes your current user to `root` while you run the command following `sudo`.

`root` has complete control over your system, with all the risks and advantages that entails. Some gotchas and guidelines:
* It is generally ok when running `sudo apt get install <program>`
  * Generally this is when you are installing programs globally on a computer no one else uses.
* It is usually ok when running `chmod` to grant yourself permissions.
* `chown` is dangerous when running sudo. Usually you find yourself running `chown` to give yourself ownership of files, which in some cases blocks the system from accessing those files, and can cause problems. 
* If you run `sudo` to install something and you should not have used `sudo`, then you may have to `chown` or `sudo` liberally to remove that thing you installed.
  * This happens because `root` owns system folders, you used `sudo` to install something as `root` and now your personal account does not have permission to edit those system folders. This is for your protection.

As a general rule, try to keep all installs and programs inside your home directory, where you own everything and will not need sudo.

## Final notes about shell scripting

* Basic shell scripting is critical for all programmers. Stronger programmers do not memorize all the commands, but get good at learning commands they need for the task at hand.
* Shell scripting is capable of everything normal languages like python/java are, but it is not designed for the same purpose.
* There is a difference between your Terminal and your Shell.
* One day you may be at risk of running `rm -rf . /*` which is a common typo from `rm -rf ./*`. This typo deletes your whole system :) Shell scripting is powerful, small mistakes have consequences.

