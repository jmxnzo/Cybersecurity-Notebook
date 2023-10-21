int * a = malloc(...);
if(a == NULL){ perror("malloc failed");}
check man pages (man 3p malloc) if errno is used, then perror() else use fprinf()


wenn keine Parameter an eine Funktion übergeben werden, verwende void
loadNextString(void)


strdup Methode verwenden, anstatt malloc + strcpy


in case of writng static in front of a global variable in C --> 
`Static` is a keyword with many meanings, and in this particular case, it means **not global** (paraphrasing)

In C, the use of global variables should be avoided, as stated in your question. Instead, it is recommended to use module-level (file-level) variables, which have extended visibility and lifetime. To declare a module-level variable, you can use the `static` keyword. Here's an example:

```c
// File: module.c

static int moduleVariable; // module-level variable

void moduleFunction() {
    moduleVariable = 10;
    // other code
}
```

In this example, `moduleVariable` is a module-level variable, which means it can be accessed within the same file but not outside of it. The `static` keyword ensures that the variable has file scope.

Now, let's address the concern about global variables. Global variables are variables that are defined outside of all functions and are available to all functions. They are not limited to any specific scope and exist until the program ends. However, global variables should be used sparingly due to their potential negative impact on code maintainability and reusability.

To access a global variable defined in one file from another file, you need to declare it in both files using the `extern` keyword. This informs the compiler that the variable is defined in another file. Here's an example:

```c
// File: file1.c

int globalVariable; // global variable

void function1() {
    globalVariable = 10;
    // other code
}
```

```c
// File: file2.c

extern int globalVariable; // extern declaration

void function2() {
    int value = globalVariable;
    // other code
}
```

In this example, `globalVariable` is declared and defined in `file1.c`. In `file2.c`, we declare it using `extern` so that we can access its value.

To summarize:
- Module-level variables, declared with the `static` keyword, have extended visibility and lifetime within the same file.
- Global variables, declared outside of all functions, are accessible to all functions but should be used sparingly.
- To access a global variable defined in one file from another file, you need to declare it using `extern` in the second file.
- Avoid using global variables when possible to improve code maintainability and reusability.

Sources:
- [Source 0](https://faculty.cs.niu.edu/~freedman/241/241notes/241var2.htm)
- [Source 3](https://overiq.com/c-programming-101/local-global-and-static-variables-in-c/)

## Makefile- what to keep in mind?
```Makefile
CC = gcc
CFLAGS = -Wall -Werror -pedantic -std=c11
CFLAGS = $(CFLAGS) -D_XOPEN_SOURCE=700

prog: main.o fib.o
	$(CC) $(CFLAGS) -o prog main.o fib.o
fib.o: fib.c fib.h
	$(CC) $(CFLAGS) -c fib.c
main.o: main.c fib.h
	$(CC) $(CFLAGS) -c main.c
```

You can use Macros(CC -> compiler and CFLAGS->compile flags) for different needs



Pseudo-Targets
Dienen nicht der Erzeugung einer gleichnamigen Datei
so deklarierte Targets werden immer gebaut
Deklaration als Abhängigkeit des Spezial-Targets .PHONY nötig
Beispiel: Erzeugen einer ausführbaren Datei mit make all
```
.PHONY: all clean

all: 
	lilo
clean:
	rm -f lilo
lilo: lilo.o #...

```
Konventionen:
- all ist immer erstes Target im Makefile und baut die komplette Anwendung
- clean löscht alle durch make erzeugte Dateien
- Hinweis: bei Aufruf von rm den Parameter -f verwenden
⇒ kein Abbruch bei nicht existierenden Dateien

1. use .PHONY if not build target 
2. always include the belonging headerfile for example main.h 
	--> fib.o:
		$(CC) $(CFLAGS) -c fib.c fib.h
3. regard the difference between

For example, the **-c** option says not to run the linker.  Then the output consists of object files output by the assembler.

-o -> `output_file`: The name of the output file (executable) that will be generated.

state that it must be possible to include a header in a source file as the only header, and that code using the facilities provided by that header will then compile
Header file soll alle anderen Header includen, der zum Compilen der Header Methoden und Variablen etc. benötigt wird. Jedoch auch nicht darüberhinaus, andere Header die nur durch das Modul an sich benötigt werden.
- **self-contained** — all necessary types are defined by including relevant headers if need be.
- **idempotent** — compilations don't break even if it is included multiple times.
- **minimal** — it doesn't define anything that is not needed by code that uses the header to access the facilities defined by the header.