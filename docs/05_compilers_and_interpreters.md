## What is a compiler?

In the previous section I showed some C code and the assembly it generated when compiled with `gcc`.

> `gcc` is a widely used CLI command for compiling C programs.

Remember compilers are programs too - they follow all the same rules and have limitations that apply to your own programs. That being said compilers have a some key functions which are important to keep track of:

1. They read and "parse" your source files.
2. They validate that your code is actually real code.
3. They optimize your code to make it faster or more memory efficient.
4. They find libraries and binaries and validate your code uses them correctly.
5. They generate an executable output

So the really obvious parts are 1 and 5:
 - Compilers follow a "grammar" when parsing your code
 - Compilers output assembly derived from your code

## What is an interpreter?

An interpreter is like a compiler but instead of generating assembly, it runs operations as it reads them. (no step 5).

If you wrote a program in C which added up any numbers it read, that could be considered an interpreter for a really primitive language that was just numbers.

Some examples:
* C is compiled
* JavaScript is interpreted
* Python is interpreted
* Java compiles to a fake-assembly which is then interpreted