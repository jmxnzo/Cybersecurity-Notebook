
# Return-to-libc
- passes by the nx bit countermeasure, which should indicate which parts of the stack are executable or not
## LibC
- has over thousends function
- printf, scanf,  etc.


## How does it work?
- the stack is manipulated in the same as a normal BO
- but the overflown return address now points to a wanted function of libc library, which is always marked as executable in the code segment of the process


## interesting functions in libc for the attack

#### system()
- system("/bin/bash"); would create a bash shell
-> 
1. we need to specify the F1 adress as the  function in the libc 
2. we need to pass a pointer, including the required argument/parameter(return adress+4)-> character pointer to an address in the stack, holding the /bin/bash string



## How to get the adress of libc function
![[Pasted image 20230715143857.png]]

![[Pasted image 20230715144407.png]]




![[Pasted image 20230715145421.png]]
ii) Wäre es problematisch falls die Funktion f mehr als einen Parameter erwarten würde? Gilt diese Einschränkung auch für die Funktion g? Begründe deine Antwort.
->Der erste Parameter der Funktion f ist die Return-Address von Funktion g. Wenn ein weiterer Parameter für f benötigt wird, wird die Adresse, an der der erste Parameter von g erwartet wird, überschrieben, somit erhält die Funktion g diesen Parameter, aber nicht Funktion f. Wenn Funktion g weitere Parameter benötigt muss hierzu nor das previous memory überschrieben werden was kein Problem für den Angriff darstellt.

iii) Auf welches Problem stoßen wir, wenn wir eine dritte Funktion nach f und g aufrufen möchten? Begründe deine Antwort.
->Da in der Return-Adresse von Funktion g der erste Parameter der Funktion f steht kann hier kein weiterer Call gestartet werden.


