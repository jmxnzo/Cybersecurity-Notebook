■ First Fit (sorting: by memory address)
■ linear search, first matching hole is used
■ Rotating First Fit / Next Fit (sorting: by memory address)
■ like First Fit, but start at the last assigned hole
■ avoids many small holes at the beginning of the list (like First Fit)
■ Best Fit (sorting: by hole size – smallest hole first)
■ linear search, smallest matching hole is searched
■ Worst Fit (sorting: by hole size – largest hole first)
■ largest matching hole is searched
■ common problem:
■ when holes are too small ) memory fragmentation


- [x] Abstractions and Data Structures
- [x] Processes and Threads
- [ ] Synchronisation
- [ ] Deadlocks
- [x] Memory Management
	- [ ] Buddy System und andere Verfahren für Klausur angucken
- [ ] Virtual memory
- [ ] File systems
- [ ] Input/Output
- [ ] Scheduling
- [ ] Inter-process communication

- [ ] take a look at different exec() methods
- [ ] How to write a Makefile, maybe just write it on the cheat sheet
- [ ] Adr

**Exit Success:** **Exit Success** is indicated by **exit(0)** statement which means successful termination of the program, i.e. program has been executed without any error or interrupt.

**Exit Failure:** **Exit Failure** is indicated by **exit(1)** which means the abnormal termination of the program, i.e. some error or interrupt has occurred. We can use different integer other than 1 to indicate different types of errors.

