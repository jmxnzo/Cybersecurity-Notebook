multitasking operating system: concurrent threads with access to the same resources:
- interrupts possible anytime
- interrupt handler

- critical section= code sequence that must not be interrupted



## exploit race conditions to get root access
- check permissions (TOC: time of check)
- appends new entry (TOU: time of use)
- Attack is always between TOC and TOU
- use interrupt to execute another program, which replaces the filename by a soft link to /etc/passwd
![[Pasted image 20230723155228.png]]![[Pasted image 20230723155435.png]]
### Heap (lower addresses, filled upward)
• Dynamic allocation
• Global variables
### Stack (upper addresses, is filled downward)
• Stores local variables, e.g., return address, inputs, etc.
• This is necessary when a task is interrupted. Stack
stores current state of the task so that it can be
recovered afterwards


Overflows guiding: 
- is the length of input even checked?
- can the length of the buffer be inputted by the user himself or somehow be manipulated?
- offset-by-one: are all loop conditions and ranges correct?

[[Unsafe and safe C-Functions]]


## Format string problem
```C
int func(char * user){
	fprintf(stdout, user);
}
```
- if user is set to "%s%s%s%s%s%s" it will print an amount of strings, determined by a NULL Pointer starting from the buffer address on the stack. So this can leak Stack memory really easily.

https://axcheron.github.io/exploit-101-format-strings/

• printf(“%n”, &x) will change the value of the variable x
• the parameter value on the stack is interpreted as a pointer to an integer value, and the place pointed by the pointer is overwritten

|   |   |   |
|---|---|---|
|%n|Writes the number of characters into a pointer|Reference|


# Prevention/defenses
 [[Unsafe and safe C-Functions]]
 Avoid risky programming constructs:
• Use fgets instead of gets
• Use strn* APIs instead of str* APIs
• Use snprintf instead of sprintf and vsprintf

• Always check for corner cases:
	• Negative values (implicit type conversion)
	• Large values
	• Long strings

n the case of mixing int and unsigned int, the int operand is automatically converted to an unsigned int before the operation is performed

The C usual arithmetic conversions convert the two operands to a common type: `unsigned int`

If you do a naïve cast from signed to unsigned (that is, don’t check for negative first and just treat the bit pattern as a positive number), all negative numbers will be greater than all positive numbers


## Countermeasures Stack overflows
[[Buffer overflow- keep in mind]]
• Type safe languages (Java, Meta Language).
• Non-executable stack (NOEXEC)
• Randomization (Address space layout randomization)(base addresses of heap, stack, code segment;variable layout; pad stack frames(on function call) and malloc() calls; position of global Offset table)
• Detection deviation of program behavior
• Canaries
• Shadow stack(maintain second stack copy and compare return addresses)
• Run time checking: StackGuard, Libsafe, SafeC, (Purify).


The **Global Offset Table**, or **GOT**, is a section of a [computer program](https://en.wikipedia.org/wiki/Computer_program "Computer program")'s (executables and shared libraries) memory used to enable computer program code compiled as an [ELF](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format "Executable and Linkable Format") file to [run](https://en.wikipedia.org/wiki/Execution_(computing) "Execution (computing)") correctly, [independent](https://en.wikipedia.org/wiki/Position-independent_code "Position-independent code") of the memory address where the [program's code](https://en.wikipedia.org/wiki/Machine_code "Machine code") or data is [loaded](https://en.wikipedia.org/wiki/Loader_(computing) "Loader (computing)") at runtime