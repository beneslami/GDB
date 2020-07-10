# GDB
little dive deep into the GDB

GDB stands for GNU DeBugger which helps us to debug our binary object file created in compilation process. GDB allows to us see what is happening in our program which really helps much when program crashes, especially when segmentation fault occurs. Some uses of gdb are as follow:

1. step through a program line by line
2. set breakpoints that will stop our program
3. make our program stop on specified conditions
4. show the present values of variables
5. examine the contents of any frame on the call stack

To compile a program to use with gdb, we have to use below script:

```
gcc -g -o binaryfile source_code.c

```
-g tells the compiler to store symbol table information in the executable. This includes:

1. symbol names
2. type info for symbols
3. files and line numbers where the symbols came from

```
$ gdb ./source_code
(gdb) run
```
```
$ gdb
(gdb) file ./source_code
(gdb) run
```

gdb with source file compiled without -g option will now work and will give **No debugging symbols found**.

-q or --quiet : show to output without any additional explanation.
