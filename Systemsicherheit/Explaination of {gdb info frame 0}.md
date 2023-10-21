```gef➤  info frame 1
Stack frame at 0xffffd660:
 eip = 0x5655631a in main; saved eip = 0xf7df1ed5
 caller of frame at 0xffffd620
 Arglist at 0xffffd61c, args: 
 Locals at 0xffffd61c, Previous frame's sp is 0xffffd660
 Saved registers:
  ebx at 0xffffd644, ebp at 0xffffd648, eip at 0xffffd65c
```



```
(gdb) info frame
Stack level 0, frame at 0xb75f7390:
 eip = 0x804877f in base::func() (testing.cpp:16); saved eip 0x804869a
 called by frame at 0xb75f73b0
 source language c++.
 Arglist at 0xb75f7388, args: this=0x0
 Locals at 0xb75f7388, Previous frame's sp is 0xb75f7390
 Saved registers:
  ebp at 0xb75f7388, eip at 0xb75f738c
```

**stack level 0**

- Frame number in backtrace. 0 is the current executing frame, which **grows downwards**, in consistence with the stack.

**frame at 0xb75f7390**

- Starting memory address of this stack frame.

**eip = 0x804877f in base::func() (testing.cpp:16); saved eip 0x804869a**

- eip is the register for the next instruction to execute (also called program counter). So at this moment, the next instruction to execute is at "0x804877f", which is line 16 of `testing.cpp`.
    
- saved eip "0x804869a" is the so called "return address", i.e., the instruction to resume in the caller stack frame after returning from this callee stack. It is pushed onto the stack upon the "CALL" instruction (save it for return).
    

**called by frame at 0xb75f73b0**

- The address of the caller stack frame.

**source language c++**

- Which language is in use.

**Arglist at 0xb75f7388, args: this=0x0**

- The starting address of arguments.

**Locals at 0xb75f7388**,

- Address of local variables.

**Previous frame's sp is 0xb75f7390**

- This is where the previous frame's stack pointer points to (the caller frame), at the moment of calling. It is also the starting memory address of the called stack frame.

**Saved registers**

- These are the two addresses on the callee stack, for two saved registers.

**ebp at 0xb75f7388**

- That is the address where the "ebp" register of the caller's stack frame is saved (please note, it is the register, not the caller's stack address), i.e., corresponding to "PUSH %ebp". "ebp" is the register usually considered as the starting address of the locals of this stack frame, which use "offset" to address. In other words, the operations of local variables all use this "ebp", so you will see something like `mov -0x4(%ebp), %eax`, etc.

**eip at 0xb75f738c**

- As mentioned before, but here it is the address of the stack (which contains the value "0x804877f").