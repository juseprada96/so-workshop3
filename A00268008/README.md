### Taller 3
**Universidad ICESI**  
**Curso:** Sistemas Operativos  
**Nombre:** Juan Sebastián Prada.  
**Tema:** Llamadas al sistema (syscalls)  
**Correo:** juseprada96 at gmail.com


### Objetivos
* Conocer y explicar la función de las llamadas al sistema en un sistema operativo

### Prerrequisitos
* Virtualbox o WMWare
* Máquina virtual con sistema operativo CentOS7
* Aplicativo strace

### Descripción
El tercer taller del curso sistemas operativos trata sobre las llamadas al sistema y su importancia para el sistema operativo

### Actividades

1. Empleando el aplicativo **strace** obtenga 5 llamadas al sistema para uno o varios comandos de linux. Explique por qué los comandos seleccionados emplean las llamadas al sistema encontradas, para ello debe emplear los manuales de Linux en Internet o del sistema operativo (comando **man**). Debe incluir la explicación de los parámetros que reciben las llamadas al sistema encontradas. Consigne capturas de pantalla donde muestre las llamadas al sistema obtenidas (sugerencia: emplear -etrace para filtrar los resultados)

### Capturas de llamadas al sistema del comando rm 

![][1]

![][2]

### Llamadas al sistema

#### unlinkat(int dirfd, const char *pathname, int flags);
unlinkat(AT_FDCWD, "examplerm.txt",0)
El llamado unlinkat se encarga de eliminar un nombre del sistema de archivos.
En este comando se utiliza unlinkat para liberar el nombre del sistema de archivos y dejar libre el espacio para ser reutilizado.
El parametro dirfd indica la dirección del directorio, el patname el nombre del archivo y las flags son las banderas que puede usar el
comando, en este caso 0 indica que ninguna esta activa.

#### mmap(void *addr, size_t length, int prot, int flags,int fd, off_t offset)
mmap es un comando que se utiliza para mapear la dirección virtual del espacio del proceso que hace el llamado.
Parametros:
addr: Direcciones para crear el mapeo, si es Null, el kernel escoge la dirección
length: es el tamaño del espacio para crear el mapeo
prot: es la protección de memoria deseada para el mapeo
flags: indican si el mapa es privado o compartido y otras caracteristicas en el caso del rm se utilizan el private y el anonymus
el anonymus indica que el mapeo no esta respaldado por un archivo y su contenido se inicia en 0. y los parametros fd y offset son ignorados.

En este comando se usan los mmap para mapear los espacios de los procesos a usar.

####  int mprotect(void *addr, size_t len, int prot);
mprotect es un llamado para proteger un espacio de memoria
addr indica la dirección de memoria a proteger.
length: el tamañno a proteger.
prot: el tipo de protección que se va a otorgar.
en este comando se utiliza mprotect para proteger ciertos espacios de memoria como solo read.

####  int fstat(int fd, struct stat *buf);
El llamado fstat se utiliza para conocer el estado de un archivo el fd es file descriptor
y el struct stat indica la estructura del estado a ser retornado.
En este comando el llamado fstat se utiliza para concer el estado de los archivos.

#### brk(void *addr)
El llamdo brk se utiliza para cambiar la posición de break el programa que define el final del segmento de datos del proceso.
addr es la nueva posición de break.


2. Realice la compilación del código fuente adjunto y su ejecución empleando el aplicativo **strace**. Identifique las llamadas al sistema encargadas de enviar y recibir datos a través de la red. A partir de los manuales de Linux en Internet o del sistema operativo explique las llamadas al sistema encontradas y sus parámetros.


![][3]


![][4]


Comandos de escritura y lectura, read y write

read(int fd, void *buf, size_t count)

fd es el file descriptor
buf es el buffering de dónde leera los datos
count es la cantidad de datos que va a leer del buffering

write(int fd, const void *buf, size_t count)

fd es el file descriptor
buf es el buffering dónde escribira los datos
count es la cantidad que va a escribir




## Referencias

* http://man7.org/linux/man-pages/man2/syscalls.2.html  
* https://jvns.ca/blog/2014/09/18/you-can-be-a-kernel-hacker/


[1]:imagenes/Captura.PNG
[2]:imagenes/Captura2.PNG
[3]:imagenes/Captura3.PNG
[4]:imagenes/Captura4.PNG
