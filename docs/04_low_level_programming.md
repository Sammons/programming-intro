### About low-level programs

We have discussed System Calls and how they ask the OS to do things at this point.

The "low" ness of programming has to do with how close you are to the hardware.

High level programmers usually don't worry about hardware at all. Python and JavaScript are popular high level programming languages, even though they both provide ways to do some low-level operations. Java is also a high level programming language.

Common low level programming languages are C, C++, or Rust.

At the cost of writing *more* code, low level programmers *control* resources in their programs more precisely.

The advantage is that the code they write has no "scaffolding" around it, so it can be very fast.

Note that in-memory computations are where low level programs are fastest: a for-loop that counts to 1000 written in C will outpace a higher level programming language for the forseeable future.

On the other hand, if you are making web-requests where the latency is measured in hundreds of milliseconds, then C or C++ may be faster, but it won't matter because they have to wait for the internet just like any other program.

With the rise of more internet-related activities in programs, high level languages have become a more favorable choice for new programmers and businesses.

### A little bit of C ### 

Just to show you what C looks like, and how to compile the simplest program, here is an example program I put in a file `main.c`:
```C
#include "stdio.h" // import library that lets us use printf

int main(int numberOfArgs, char const *listOfArgsMemoryAddress[])
{
  printf("Hello there! I see you have %i args", numberOfArgs);

  /* return signal */
  return 0;
}
```

### Assembly ###

C code compiles to binary assembly for specific CPUs to run. This format can be read by a bash command `objdump` which has a flag `-d` for dissassembly. Since we are l33t hackers we can dissassemble our compiled C to see the assembly language commands.

The output is fairly big, so here's are some parts that are specific to our program, that `#include "stdio.h"` causes a fair amount of code we did not write to take up space.

I ran `objdump -d main.out > main.dump`

And read from main.dump - to be extra clear this is x86 assembly language:
```
000000000000064a <main>:
 64a:	55                   	push   %rbp
 64b:	48 89 e5             	mov    %rsp,%rbp
 64e:	48 83 ec 10          	sub    $0x10,%rsp
 652:	89 7d fc             	mov    %edi,-0x4(%rbp)
 655:	48 89 75 f0          	mov    %rsi,-0x10(%rbp)
 659:	8b 45 fc             	mov    -0x4(%rbp),%eax
 65c:	89 c6                	mov    %eax,%esi
 65e:	48 8d 3d a3 00 00 00 	lea    0xa3(%rip),%rdi        # 708 <_IO_stdin_used+0x8>
 665:	b8 00 00 00 00       	mov    $0x0,%eax
 66a:	e8 b1 fe ff ff       	callq  520 <printf@plt>
 66f:	b8 00 00 00 00       	mov    $0x0,%eax
 674:	c9                   	leaveq 
 675:	c3                   	retq   
 676:	66 2e 0f 1f 84 00 00 	nopw   %cs:0x0(%rax,%rax,1)
 67d:	00 00 00 
```

You can ctrl+f around in [this yale page](http://flint.cs.yale.edu/cs421/papers/x86-asm/asm.html) to get a handle on what some of these commands do.

* `lea` load effective address
* `callq` calls a function
* `mov` move a value in memory to a location
* `%eax` is a register, like a hardware variable inside the CPU to store stuff
* `$0x0` a hexidecimal value of 0

### Ok, so back to System Calls ###

When I run `strace -o trace.txt ./main.out` and search through the records I can find this line:
```
write(1, "Hello there! I see you have 1 ar"..., 34) = 34
```

So when that machine code is run, we can see that our printf ultimately results in that `write` System Call being output.

You can check `strace -c` if you think some disk writes or network reads are the slow thing in your program and want a summary of what's taking all the time.

This stuff is cool, but rarely important to day-to-day work.

[Next: Compilers & Interpreters](05_compilers_and_interpreters.html)