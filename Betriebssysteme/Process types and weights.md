![[Pasted image 20230719125953.png]]
■ kernel-level threading (1:1, one-to-one)
- light-weight processes: multiple control flows in a single address space
-  each user-level thread maps to one kernel-level thread → pthreads
■ user-level threading (m:1, many-to-one)
- feather-weight processes: multiple user-level control flows in a single
address space
- many user-level threads map to one kernel-level thread
■ hybrid threading (m:n, many-to-many)
- feather-weight process: multiple user-level control flows using multiple
kernel-level threads in a single address space
- many user-level threads map to many kernel-level threads



Can kernel threads be children of user-threads?
Kernel threads are threads running **permanently** in kernel mode.

issue a `ps -efl` command. You'll recognize these kernel threads to the fact their names stand between square brackets. And, paying attention to the parent process ID, you'll notice that most of them are sons of PID 2 ([kthreadd]) others being sons of PID 1 (init[3])

So, basically, the answer to your question is : no!

This however does not prevent whatever thread to issue system calls that will make them switch temporarily into kernel mode for the time of the execution of the call. But that does not make them _kernel threads_ it's simply threads running, for some time, in kernel mode.

Therefore, while you won't find user processes parents of kernel threads, you can have user processes parents of threads, sometimes executing, in kernel mode