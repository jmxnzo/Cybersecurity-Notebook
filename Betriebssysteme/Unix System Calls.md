system calls will change the current process running in user-mode to kernel-mode, until the system call is executed and thus returns back to the user-mode execution

### Process Control
- getpid(2) returns PID of the running process
-  getppid(2) returns PID of the parent process (PPID)
-  getuid(2) returns the user ID of the running process (UID)
-  fork(2) creates new child process
-  exit(3), terminates the running process
_exit(2)
-  wait(2) waits for the completion of a child process
-  execve(2) loads and starts a program in the context of the
running process


## Fork system call pid_t fork(void)
the child process inherits:
- address space (code, data, bss, heap, stack)
-  user ID
- standard I/O channels
- process group, signal table (more about this later)
- open files, current working directory (more on this much later).
what is not copied:
-  process ID (PID), parent process ID (PPID)
- pending signals, accounting data, ...
-> one process calls fork, but two processes return...
-> we can only differentiate between the two processes by looking at the pid/ppid
```C
.. /* includes */
int main () {
int pid;
printf(“Parent process: PID %d PPID %d\n”, getpid(), getppid());
pid = fork(); /* process is duplicated!
Both continue to run at this point. */
if (pid > 0) /* parent process */
	printf(“In the parent process, child PID %d\n”, pid);
else if (pid == 0) /* child process */
	printf(“In the child process, PID %d PPID %d\n”, getpid(), getppid());
else
	printf(“Error occurred.\n”);
}

```
Als **Zombie-Prozess** wird bei unixartigen Betriebssystemen der Prozesstabelleneintrag eines beendeten Prozesses bezeichnet. Ein beendeter Prozess wird aus der Prozesstabelle entfernt, sobald sein Elternprozess dessen Exit-Status abfragt. Bis dahin verbleibt er dort als Zombie, der keine weiteren Ressourcen außer dem Tabelleneintrag, der Prozess ID und Einträgen in Nutzungs-Statistiken mehr belegt.

```C 
/* ... includes, main() { ... */
char cmd[100], arg[100];
while (1) {
	printf ("Command?\n");
	scanf ("%99s %99s", cmd, arg);
	pid = fork(); /* Process is duplicated, two processes continue
to run at this point. */
if (pid > 0) {
	int status;
if (wait(&status) == pid && WIFEXITED(status))
	printf ("Exit Status: %d\n", WEXITSTATUS(status));
}
else if (pid == 0) {
	execlp(cmd, cmd, arg, NULL);
	printf ("exec has failed\n");
}

}```
1) wait() bis zur Terminierung des Prozesses
2) Überprüfen der Bereitstellung des exit status mit WIFEXITED
3) Erhalten bzw. Ausgeben des Status mit WEXITSTATUS(status)
If any process has more than one child processes, then after calling wait(), parent process has to be in wait state if no child terminates.   
If only one child process is terminated, then return a wait() returns process ID of the terminated child process.   
If more than one child processes are terminated than wait() reap any _**arbitrarily child**_ and return a process ID of that child process.   
When wait() returns they also define **exit status** (which tells our, a process why terminated) via pointer, If status are not **NULL**.


Die Funktion wait() wartet, bis sich ein Kindprozess beendet, und gibt dessen PID als Rückgabewert zurück. Bei Fehler wird -1 zurückgegeben. Die Funktion waitpid() hingegen wartet auf einen bestimmten Kindprozess mit der in pid als erstes Argument angegebenen Prozess-ID. Sofern beim Argument status nicht der NULL-Zeiger angegeben wurde, wird hier die Statusinformation zu dem beendeten Prozess gespeichert. Um diesen Status auszuwerten, sind in der Headerdatei <sys/wait.h> folgende Makros definiert:
![[waitpid()1.png]]



![[waitpid()2.png]]

The _options_ argument can be set to either 0 or WNOHANG.

![[waitpid()3.png]]


**What is the difference between `exit(0)` and `exit(1)` in C language?**

`exit(0)` indicates successful program termination & it is fully portable, While  
`exit(1)` (usually) indicates unsucessful termination. However, it's usage is non-portable.

Note that the C standard defines `EXIT_SUCCESS` and `EXIT_FAILURE` to return termination status from a C program.

`0` and `EXIT_SUCCESS` are the values specified by the standard to indicate successful termination, however, only `EXIT_FAILURE` is the standard value for returning unsucessful termination. `1` is used for the same in many implementations though.