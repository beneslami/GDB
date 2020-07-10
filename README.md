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


The whole purpose of coming to gdb was to pause, observe and proceed. Therefore, gdb provides breakpoints for us. Breakpoints can be used to stop the program run in the middle, at a designated point. Whenever gdb gets to a breakpoint, it halts execution of our program and allows us to examine it. Simplest way of putting a breakpoint is using the function name or a line number.
```
(gdb) break <NAME> | <LINE NUM>
```
```
(gdb) info functions
```
```
(gdb) info breakpoints
```
```
(gdb) list
```
```
(gdb) list <LINE, LINE>
```
```
(gdb) next  /* it is used after setting breakpoints */
```
```
(gdb) finish
```
```
(gdb) delete <breakpoint>
```
```
(gdb) continue
```
```
(gdb) step /* it goes inside the function */
```
Passing parameters in gdb is done via --arg.
```
$ gdb --args <binaryfile> arg1 arg2 arg3
```
```
(gdb) backtrace
(gdb) frame <NUM>
```
x in gdb stands for examining the memory. It comes with a number of formatting commands that provide precise control over how many bytes we would like to examine and how we would like to print them.
```
(gdb) x /4xb &i
```
The flags indicate that I want to examine 4 values formatted as he'x' numerals, one 'b'yte at a time. Note that, on Intel machines, bytes are stored in **Little Endian** order.
