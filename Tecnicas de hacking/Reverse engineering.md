![[Pasted image 20240103000359.png]]


- Dynamic analysis: We run the application (ALWAYS ON A VM) and observe its behavior with different inputs.

- Static analysis: We attempt to gather as much information as possible from the application's source code to understand how it works.


### Preguntas de la classe
- Saber en qué dirección de memoria comienza la pila.
- Cuál es el límite hasta el que puede crecer la pila (marco de pila).
- Cuál es la dirección actual de la pila en la que termina la información útil.

1. **Stack Memory Direction:**
    
    - In x86 architecture, the stack typically grows downward in memory. The stack starts at a higher memory address and moves towards lower memory addresses.
2. **Stack Size Limit:**
    
    - The stack size limit is usually determined by the operating system and can be adjusted. In Windows, for example, you can set the stack size during program compilation or change it using system calls. In Linux, the `ulimit` command can be used to view or set the stack size limit.
3. **Current Stack Pointer:**
    
    - The stack pointer (SP) register holds the memory address of the top of the stack. As new items are pushed onto the stack, the stack pointer decreases.
    - The base pointer (BP) register is often used to reference local variables and parameters within a function, providing a frame of reference within the stack.

- SS (Stack Segment): Indicates the starting address of the stack.
- ESP (Extended Stack Pointer): Indicates the address of the element at the top of the stack.
- EBP (Extended Base Pointer): Indicates the base address of the stack frame.




# Buffer overflow
#### NOP-Slide
In many examples and Proof of Concepts (PoCs), you will come across the concept of a NOP sled:
- When an attacker can only predict the starting address of their shellcode approximately, they often fill the memory with NOP (no-operation) instructions.
- This way, if we manage to jump to an address close to the beginning of the shellcode, we land in a block of NOPs. These NOPs are executed, and then the execution jumps to our actual shellcode.
-  This is a well-known technique, so its detection can be relatively easy.


#### Countermeasures
- Data Execution Prevention (DEP): Prevents an application from running in a memory region where it shouldn't (non-executable).
- Address Space Layout Randomization (ASLR): A technique that aims to prevent knowing the memory addresses that could be exploited for attacks.
- Canaries: A randomly generated value in each execution that aims to detect stack overflow.


#### Occurance
-  environments like mobile devices, IoT devices, embedded systems, etc.
- impacts appliances, robots, connected cars, and any other device incorporating software. The added problem is that many of these devices are connected to the internet without proper protections
- less software development


### Format-String vulnerabilities 
A format string vulnerability occurs when user input is passed as a format argument to functions that support it.
-  Functions like printf, scanf, or similar ones are susceptible.
-  The format argument has various specifications that could allow an attacker to leak information (if they control the printf format argument, which is our focus).
- Since printf is a function that takes a variable number of arguments, it will continue to extract data from the stack according to the specified format.
- For example, if we can make the format argument become "%x%x%x%x", printf will display four values from the stack in hexadecimal, potentially leaking sensitive information.
- printf can also leak an arbitrary "argument" with the following syntax: "%n$x" (where n is the decimal index of the desired argument).
- Although these vulnerabilities are powerful, they are rare to encounter nowadays because all modern compilers issue warnings when printf is called without using the format argument.

https://gist.github.com/anvbis/64907e4f90974c4bdd930baeb705dedf
https://docs.pwntools.com/en/stable/