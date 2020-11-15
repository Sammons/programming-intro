## Operating Systems

The term OS also refers to a collection of programs like the file system, and system ui, and some others. For this discussion we are talking about the OS that runs our programs, and which our programs interact with - this is the same boss program which is in charge of the system ui and friends.

The OS has a lot of jobs, but fundamentally it mediates resource allocation for all of the processes. Processes generally have parent processes/programs which launched them. The OS is the ultimate root parent program.

Some OS behavior/facts that should address some random but relevant points:

* The OS has a kernel, which is like the engine for the OS, it handles the complicated parts of the job and is generally almost the same kernel across linux flavors. 
* Drivers are chunks of code that get linked into the OS to interface with Hardware. Drivers are not independent programs.
* If you spawn a child process, and forget to close it before your process ends, then the OS will `reap` that child - also known as a `zombie` at that point.

The operating system manages *everything*
  - you want to allocate memory? the OS mediates that.
  - you want to read a file? the OS determines yes/no.
  - you want to open a socket? (same as a file)
  - want to launch a program? yep the OS owns it.
  - There are too many programs for your CPU? OS chooses who gets time on the CPU.

## But how does it know what's going on?

The Operating System provides an API for programs to ask it to do things. Pretty much everything a program does involves the OS.

For example a C program might do the following:
* allocate memory
* write to that memory
* read from that memory
* write to the stdout

Each of these things is done through a `system call`. which is usually a request to the OS to run some code.

You can see what system calls a program makes with the bash command `strace`

For example:
`strace -o trace.txt ls`

output in the trace.txt file:
```
execve("/bin/ls", ["ls"], 0x7ffc56df6fa0 /* 66 vars */) = 0
brk(NULL)                               = 0x5588be52a000
access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/home/sammons/.steam/ubuntu12_64/gameoverlayrenderer.so", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\360l\0\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0775, st_size=246174, ...}) = 0
mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7f9496ac2000
mmap(NULL, 2343480, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7f949665e000
mprotect(0x7f9496695000, 2093056, PROT_NONE) = 0
mmap(0x7f9496894000, 12288, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x36000) = 0x7f9496894000
...lots of lines...
```

each line is a touchpoint between your program and the OS.

## Scheduling

The operating system can secretly pause/resume your program many times during its execution. It can do this without interfering at all with what it is doing.

Just be aware that even though you have 100 threads in your program, they aren't all running at the same time unless you have at least 100 CPU cores.

This is called a "Context Switch" which the CPU swaps between who is running on a core.

[Next: Low Level Programming](04_low_level_programming.html)