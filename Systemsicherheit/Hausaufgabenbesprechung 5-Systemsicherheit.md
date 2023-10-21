
Anzeige von dump einer Binärdatei:
objdump -d intro -M intel | grep "Funktion"


## Aufgabe 4 doa
lokale Variablen werden nacheinander auf den Stack geladen
-> Adressen wachsen demnach von hohen nach niedrigen Adressen

strcpy schreibt in den Buffer von niedrigen nach hohen Adresssen,
->overflowt somit auf den bereits beschriebenen Stackbereich

in Klausur kann man davon ausgehen, das die lokalen Variablen wie im Code definiert auf den Stack geladen werden, keine Stackrandomization etc.


! immer beachten ASCII String als Big endiness in Little endiness umzuwandeln, wenn man den buffer overflowt
-> dadurch das strcpy von unten niedrigen nach hohen Adressen kopiert
-> für die push and pop Operationen sind 


strncpy anstatt strcpy verwenden als Gegenmaßnahme,
generell sicheren C-Funktionen gegen buffer overflows


Endianness?
• Not important when writing the string directly into memory
• Not important for bytewise access of the string: mov byte ptr [esp], 'A'
- Not important for injecting shellcode, bc normal instructions are also stored in little endianness
• Important when accessing several bytes: push 'ABCD' vs push 'DCBA'

-> only addresses need to be written in other Endianness


-> Addresses and other overflows can never include zero bytes, because the following bytes won't be written to the buffer

NOP Sliding:
41...41 -> 20 bytes padding to fill the buffer 
41424344 -> (Arbitrary) value popped into EBP
0xffffd5e4 -> b"\xe4\xd5\xff\xff" return address, somewhere in the nop slide
90...90 -> 500  NOPs-> NOP slide in front of our shellcode
31...80 -> Shellcode to be executed

Execution grows with the addresses-> in other direction then the stack


Stack canaries:
31...80 -> Shellcode to be executed
'\x41'x16


Data Execution Prevention=alle memory pages als Code und somit executable oder schreibbar und nicht executable zu markieren
-> Return oriented programming: e.g. return-to-libc



```python
[::-1]
#list[<start>:<stop>:<step>]
```
this will reverse the address/ change the endianness in python -> useful to create the payload