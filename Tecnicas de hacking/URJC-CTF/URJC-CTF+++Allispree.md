1. Taking a look at the provided source code, shows us that there is a possible command injection in the provided ping tool, which is directly run on the server system using exec() system call
![[Screenshot from 2023-12-30 19-57-56.png]]![[Screenshot from 2023-12-30 19-58-14.png]]
2. Now we can check the current working directory, injecting `localhost & pwd`
![[Screenshot from 2023-12-30 20-00-12.png]]

3. Continuing the exploit we use `localhost & ls` to get show the contents of our current directory and we directly find the flag.txt
![[Screenshot from 2023-12-30 20-00-51.png]]
4. Last step is to use `localhost & cat flag.txt` to succesfully obtain the flag
![[Screenshot from 2023-12-30 20-01-25.png]]
