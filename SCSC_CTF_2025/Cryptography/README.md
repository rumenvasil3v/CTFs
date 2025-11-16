# Think of a number

The problem invloved a program written in C language and I had to guess a random generated number. There was separate executable which made the program to run.

## Tools I used
- gdb (GNU debugger) to inspect the program and its behaviour


This text you see here is **actually- written in Markdown! To get a feel
for Markdown's syntax, type some text into the left window and
watch the results in the right.**

## Vulnerability and Exploitation

The program is an example of how a buffer overflow can be used to modify variables.

```sh
# The variable is initialized to read numbers up to 8 bytes, but the program reads up to 28
char input[8] = {0}; // initialize the variable
...
// the part of the code that allows us to overwrite the random number 
fgets(&input[0], 28, stdin);
guess = strtol(&input[0], NULL, 16);
```

## Solution

We just have to give an input that takes the advantage of the buffer overflow. One such example that works is '58585858XXXXXXXX'. Once the input is read it converts the characters in hex and that in memory is represented as four X's in the EAX register and the buffer at 'esp+0x28' contains four X's as well.