push ebp: decrements esp(by 4) and then copies source operand ebp to the top of the stack

pop esi: copy top of stack to esi and add 4 to esp

call 2342: Call function at address 2341, push address of next instruction to stack (return address saved in frame)

ret: Return from subroutine, use the instruction pushed
previously onto the stack (pop it from stack)

