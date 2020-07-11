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

### Frames

A running application maintains a call stack that contains information about its functions that have been called. Each item in the stack is a call frame, and each frame contains both the information needed to return to its caller and the information needed to provide the local variables of the function. When our program starts, the call stack has only one frame, that of the function main. Each function call pushes a new frame onto the stack, and each function return removes the frame for that function from the stack. Recursive functions can generate many frames.
```
(gdb) info frame <NUM>
```
```
(gdb) info variables /*list all global and static variables */
```
```
(gdb) info locals /* list local variables values of current stack frame */
```
```
(gdb) info args /* list argument values of current stack frame */
```
```
(gdb) info registers
```

* There is one keyword in C called **register** which comes before variable definition. It stores the value of the variable in the CPU registers.  

As long as a breakpoint is enabled, the debugger always stops at that breakpoint. However, sometimes, it's useful to tell the debugger to stop at a break point only if some condition is met, like the when a variable has a particularly interesting value. We can specify a break condition when we set a breakpoint by appending the keyword if to a normal statement.
```
(gdb) break [position] if <expression>
```
In the above syntax, position can be a function name or line number. If we already set a breakpoint at the desired position, we can use the condition command to add or change its break condition:
```
condition bp_number [expression]
```

### Watchpoint

Watchpoints are similar to breakpoints. Watchpoints are set on variables. When those variables are read or written, the watchpoint is triggered and program execution stops. The argument to the watch command is an expression that is evaluated. This implies that the variable we want to set a watchpoint on must be in the current scope. So, to set a watchpoint on a non-global variable, we must have set a breakpoint that will stop our program when the variable is in scope. We must set the watchpoint after the program breaks.  
```
(gdb) watch <variable> /* check if someone is writing to the variable */
```
```
(gdb) rwatch <variable> /* identical to above command */
```
```
(gdb) awatch <variable> /* check for read and write */
```
```
$ gdbtui ./source_code
```

We might want to save the output of gdb commands to a file. There are several commands to control gdb's logging.
```
(gdb) set logging on/off  /* enable/disable logging*/
(gdb) set logging file <FILE>
```
gdb saves all output from this point in a text file called gdb.txt that resides in the directory which we are running gdb. Note that, by turning on and off, gdb will concatenate output to the gdb.txt file.

In order to see the assembly code of the running program:
```
(gdb) breakpoint main (simply b main)
(gdb) run (simply r)
(gdb) disassemble main
```
