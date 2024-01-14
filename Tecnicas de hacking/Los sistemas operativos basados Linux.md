## Linux Kernel
- El Kernel es la parte más importante de un Sistema Operativo:
	- Gestiona la memoria del sistema.
	- Gestiona las llamadas al sistema.
	- Gestiona los procesos.
	- Gestiona la comunicación software-hardware.
	-  +28M de líneas de códig
- se puede interactuar a traves de la Shell con el Kernel (bash, zsh, sh, ash)

## Procesos y ficheros
![[Pasted image 20231230115251.png]]
- Proceso: es un programa en ejecución identificado por un identificador de proceso único, llamado PID.
- Fichero: es una colección de datos, con una ubicación en el sistema de archivos llamada ruta
	- Los directorios son un tipo especial de fichero.
![[Pasted image 20231230115523.png]]

## Variables
- Variables de entorno globales: 
	- permanecen durante toda la sesión del usuario, desde su inicio de sesión. Se nombran en mayúsculas.
	- ```export MIVARIABLE=‘variable global’```
- Variables de entorno locales: 
	- son locales a cada instancia de cada Shell, es decir, permanecen mientras la Shell esté abierta. Se nombran en minúsculas.
	- `mivariable=‘variable local’`
- Ejemplos:
	- $PATH: muestra las rutas en los que la Shell buscará los comandosa ejecutar.
	- $HOME: muestra la ruta absoluta del directorio home del usuario actual.
	- $USER: muestra el usuario logado.
	- $HOST: muestra el nombre de la máquina.
	- $ARCH: muestra la arquitectura del procesador de la máquina.
	- $OSTYPE: muestra el Sistema Operativo que se está utilizando.
	- $PRINTER: muestra la impresora por defecto para enviar trabajos de impresión.


[[Técnicas Básicas de Explotación en Linux]]