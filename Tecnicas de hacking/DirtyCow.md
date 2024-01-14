- vulnerabilidad del Kernel
- parcheada en las versiones 4.8.3, 4.7.9, 4.4.26 y posteriores
- explotable nivel local
- permite elevar privilegios(actuar como root)
- Aprovecha la forma que Tene el Kernel de gesTonar un Tpo de
operación en la memoria del sistema (Copy-On-Write)
https://www.youtube.com/watch?v=kEsshExn7aE
### Explanation of exploit
**Copy-On-Write (COW):** 
- When multiple processes share the same memory region and one of them attempts to modify the data, a copy of the memory region is typically created to maintain data integrity for the other processes. This is known as Copy-On-Write.

**Dirty Bit Tracking:** 
- To determine whether a specific memory region is "dirty" (i.e., has been modified), the kernel uses a Dirty Bit. This bit is set when a process attempts to write to a memory region.

**madvise Don't Care Function:** 
- The Dirty COW exploit involves the use of the `madvise` system call with the `MADV_DONTNEED` flag. This function advises the kernel that the application has no interest in the specified page range, allowing the kernel to free up resources. However, it is this very function that is misused in the Dirty COW attack to introduce a race condition.

**Race Condition:** 
- The Dirty COW vulnerability relies on a race condition that occurs when the kernel checks whether a specific memory region is read-only and decides whether to create a copy. An attacker can exploit this race condition by initiating write access to the memory region while the kernel is performing the check.

![[Pasted image 20231230133857.png]]
**Exploit Mechanism:** 
The Dirty COW exploit occurs in multiple steps:
- The attacker creates a thread, which modifies the read-only memory region.
- The kernel locates the physical address and starts checking the Dirty Bit and by that creates the private copy in mapped memory, because of the COW mechanism.
- During the write system call, the attacker initiates a race condition. The attacker uses `madvise` with `MADV_DONTNEED` to signal to the kernel that it doesn't care about the specified page range.
- At this point, since the kernel assumes the memory region is read-only and has received the `MADV_DONTNEED` signal, the private copy in main memory is discarded.
- However, the attacker's write access takes place afterwards, but instead of writing on the private copy, it is performed on the read-only memory area.
- Thus, the kernel remains unaware that the memory region has been altered, and the attacker gains write access to a read-only area.

**Privilege Escalation:** 
The exploit allows a non-privileged user to gain write access to read-only files, potentially leading to the escalation of user privileges by manipulating critical system files.
