- 32bit system 
-> 4 GiB of byte-addressable memory(RAM) due to 2³2 possible addresses
- CISC instruction set

- Instruction layout: target operand is always on the left
- jz jumps if ZF(zero flag) is set in eflags register(equality of two previous compared operands)



-  Stack segment (local variables and procedure
activation records)
• Data segment [global uninitialized (.bss) and
initialized (.data) variables; dynamic variables (heap)]
• Code (text) segment (program instructions à read-only)


## Calling conventions
- parameter passing?
- When is the stack pointer modified during a function call?
- which registers need to be saved during a function call?

>[!definition] cdecl
• All parameters are pushed to stack
• Calling function cleans the stack after the function call returns
• C semantic
• Advantage: variable number of parameters (e.g., printf)
• ecx and edx are available for use in the function
• Return value available in eax

>[!definition] stdcall
>• All parameters are pushed to stack
• Callee is responsible to cleanup the stack
• ecx and edx are available for use in the function
• Return value available in eax
• Standard calling convention for Win32 API


>[!definition] fastcall
>• First two parameters in ecx and edx
• All other parameters on stack
• Return value available in eax
• Typically only used internally by OS

- always keep in mind, that the parameter order on the stack is reversed: first parameter of function will be the last parameter to be pushed to the stack
[[Intel x86- important functions]]

### Register preservation
- function might operate on register values after return -> First push all registers to stack, then pop them in reverse order! 