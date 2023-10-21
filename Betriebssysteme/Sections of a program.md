## Which variables and data is stored in which section of the program?

- initialized global variables, static variables --> data 
```
char s[] = “hello world”; //.data
int debug=1; //.data

int main(){
	static int initVar=3; //.data
}

```

- data section is divided in read-only and read-write are, thus ```const char*string= "hello world"``` can be guaranteed


- zero initialized global and static variables -> bss 
-->Data in this segment is initialized by the kernel to arithmetic 0 before the program starts executing uninitialized data starts at the end of the data segment and contains all global variables and static variables that are initialized to zero or do not have explicit initialization in source code.
``` 
static int i;
int main(){
	static int i; //.bss
}

```

- constant data types -> code and/or data. 
	Consider string literals for a situation when a constant itself would be stored in the data segment, and references to it would be embedded in the code

Consider the code:

```c
const int i = 0;
static const int k = 99;

int function(void)
{
    const int j = 37;
    totherfunc(&j);
    totherfunc(&i);
  //totherfunc(&k);
    return(j+3);
}
```

Generally, `i` can be stored in the text segment (it's a read-only variable with a fixed value). If it is not in the text segment, it will be stored beside the global variables. Given that it is initialized to zero, it might be in the 'bss' section (where zeroed variables are usually allocated) or in the 'data' section (where initialized variables are usually allocated).

If the compiler is convinced the `k` is unused (which it could be since it is local to a single file), it might not appear in the object code at all. If the call to `totherfunc()` that references `k` was not commented out, then `k` would have to be allocated an address somewhere - it would likely be in the same segment as `i`.



- local variables(declared and defined in functions) ---> stack 
 --> Exception: variables declared and defined in `main` function ---heap also stack (the teacher was trying to trick you)

- pointers(ex: `char *arr`, `int *arr`) --> heap data or stack, depending on the context. C lets you declare a global or a `static` pointer, in which case the pointer itself would end up in the data segment.

- dynamically allocated space(using `malloc`, `calloc`, `realloc`) -------> heap

- function code, specific instructions-> .text (code segment)



https://www.quora.com/Where-are-functions-stored-in-memory-C

https://www.geeksforgeeks.org/memory-layout-of-c-program/
