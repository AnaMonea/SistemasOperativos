# Primer Examen

## Software Libre

Es una filosofía comunitaria de desarrollo de programas que da la libertad de crear, distribuir, estudiar, modificar y vender o pagar software, sin estar violando alguna ley o patente. Pudiendo modificarlos en pos de mejorarlos y adaptarlos a sus necesidades. **Software libre no quiere decir “gratuito” se centra más en la libertad que en la gratuidad**

1- La distribución Ubuntu fue lanzada antes que Debian? Falso
2- La distribución Fedora, deriva de que otra distribución? Red hat 
3- Dennis Ritchie fue el creador de Unix y el lenguaje de programación C? Verdadero 
4- De la lista de las 500 supercomputadoras más poderosas del planeta, cuál es el sistema operativo dominante? Linux 
5- Bajo una licencia de Software Libre, podremos adaptar un software ya existente, con licencia de código abierto, distribuirlo y cobrar dinero por el? Verdadero. El software libre es una filosofía comunitaria de desarrollo de programas que da la libertad de crear, distribuir, estudiar, modificar y vender o pagar software, sin estar violando alguna ley o patente. Por lo tanto, bajo una licencia de software libre, se puede adaptar un software ya existente con licencia de código abierto, distribuirlo y cobrar dinero por él, siempre y cuando se cumpla con los términos de la licencia de software libre y no se esté violando ninguna ley o patente.



## Configurar Virtual Machine

-Convertirnos en el usuario administrador
```
sudo su
```
-Configurar el teclado
```
setxkbmap es
```
-Cambiar password de root (escribirla dos veces, cuando tipeamos no se visualizan los caracteres por razones de seguridad):
```
passwd
```
-Sistema en modo consola
```
systemctl set-default multi-user.target
```
-Reiniciar el sistema
```
reboot
```
-Configurar el DNS de nuestro equipo editando el archivo de configuración
```
vi /etc/resolv.conf
```
-Actualizar el sistema
```
yum update
```

### Red

-Nat: 
Tenemos a la vm en una red aislada y tiene salida a través de nuestra computadora física a la red

-Bridg<span style="color:#894d4d"><span style="color:#894d4d"><span style="color:#894d4d"><span style="color:#894d4d"><span style="color:#894d4d"><span style="color:#894d4d"><span style="color:#894d4d"><span style="color:#894d4d"><span style="color:#894d4d"><span style="color:#894d4d"><span style="color:#894d4d"></span></span></span></span></span></span></span></span></span></span></span>e o Adaptador Puente:
La vm aparece en nuestra red como si fuera una computadora más dentro de nuestra red

-Host Only o Sólo Anfitrión:
Es una red completa aislada de la nuestra, donde no tendremos comunicación con nuestra red ni salida a internet.


## Deshabilitar el Firewall de CentOS

1. Bajar los servcios de firewall: 
```
systemctl stop firewalld
```

2. Deshabilitamos el servicio de firewall para su inicio con el sistema:
```
systemctl disable firewalld
```

## Deshabilitar Selinux

Selinux es una capa extra de seguridad para sistemas operativos Red Hat y derivados, otorga un completo control sobre la red, archivos y servicios. Para nuestro laboratorio es más sencillo no usarlo, ya que su complejidad es alta

1. Comprobar el estado de selinux:
```
getenforce
```

Puede devolver 3 valores: 
a- enforced: estará activo y restringiendo operaciones no permitidas. 
b- permissive: no bloqueara acciones no permitidas, pero dará avisos de seguridad. 
c- disabled: no bloqueara ningún tipo de acción y no dará aviso

2. Configurar el modo de operación de selinux, para ello editamos el archivo:
```
vi /etc/selinux/config
```

Deberia verse asi:
```
# This file controls the state of SELinux on the system. 
# SELINUX= can take one of these three values: 
# enforcing - SELinux security policy is enforced. 
# permissive - SELinux prints warnings instead of enforcing. 
# disabled - No SELinux policy is loaded. SELINUX=disabled 
# SELINUXTYPE= can take one of three values: 
# targeted - Targeted processes are protected, 
# minimum - Modification of targeted policy. Only selected processes are protected. 
# mls - Multi Level Security protection. 
#SELINUXTYPE=targeted
```

3. Reiniciar el sistema
```
reboot
```

### Opciones de localizacion del sistema (lenaguaje, distribucion del teclado)

-Cambiar distribución de teclado a español latinoamericano
```
localectl set-keymap latam
```

-Salir de la sesión de usuario actual
```
exit
```
<!---Podemos utilizar también Ctrl + d--->

-Limpiar la pantalla
```
clear
```
<!---Podemos utilizar también Ctrl + l--->

## Sistema de archivos

El sistema de archivos de Linux está basado en un árbol de directorios invertido, donde arriba de todo estará el directorio raíz (root), representado por una “/”, y de ella irán desprendiendo los directorios que conforman la estructura.

### Directorios importantes

En la jerarquía de directorios estándar (FHS por su sigla en inglés) existen directorios que cumplen funciones específicas. Por ejemplo:

-Directorio raíz o /
Este directorio es el más alto en la jerarquía, contendrá toda la estructura

-Directorio /etc
Contendrá las configuraciones del sistema operativo como de las aplicaciones (no en todos los casos)

-Directorio /home
Contiene los directorios de trabajo de los usuarios de sistema, un directorio por cada usuario.

-Directorio /root
Es el directorio de trabajo por defecto del usuario administrador del sistema (root)

-Directorio /tmp
Sirve para contener archivos temporales que pueden ser borrados en cualquier momento. <mark style="background: #FF5582A6;">Advertencia</mark>: No se deberá alojar en él información que sea necesaria para la operación de ninguna aplicación que se ejecute en el sistema. Muchas distribuciones vacían este directorio en el momento del apagado o reinicio del sistema.

-Directorio /bin
Están los programas esenciales del sistema operativo

-Directorio /sbin
Contiene los programas esenciales que solamente pueden ser ejecutados por el usuario administrador del sistema (root)

-Directorio /lib y /lib64
Contiene librerías que son necesarias para el funcionamiento de los programas que se ejecuten el sistema

-Directorio /usr
Contiene una colección de aplicaciones no esenciales y los archivos necesarios para las mismas

-Directorio /opt
Contiene software adicional. Generalmente las necesidades de estos programas estarán en este directorio y no en algún otro directorio del sistema.

-Directorio /var
Contiene archivos y directorios que varían con el tiempo. Ej: archivos de registros de aplicaciones y del sistema operativo (logs), que irán reportando el funcionamiento de éstos en el tiempo.

-Directorio /dev
Contiene archivos que representan los dispositivos físicos del sistema, como unidades de disco, tarjetas de red, etc.

-Directorio /proc, /sys
Son directorios volátiles que contienen información que se carga durante el inicio del sistema. Representan archivos con valores de configuración de parámetros de kernel, usados por el sistema operativo

-Directorio /boot
Contiene los archivos necesarios para el inicio del sistema operativo, cuando se enciende la computadora, esta irá al disco y buscará estos archivos para comenzar la ejecución del sistema

### Sobre los filesystems

-Directorio
Es aquel que contendrá archivos o incluso otros directorios. O bien, es un archivo especial en Linux con la capacidad de contener otros archivos.

-Filesystems
Es la asignación de un recurso de disco a un directorio. En linux no podremos escribir directamente en una unidad de disco, para poder realizar esto necesitamos que ese disco esté asignado a un directorio, esta acción se la llama como montaje, montar un disco en un directorio es generar un filesystem. Cuando escribimos información en ese filesystem, lo hacemos en esa unidad particular de disco, no afectando a las demás.

## Gestión de archivos y directorios.

Nos permite listar, crear, borrar, copiar, renombrar o mover los mismos. Para cada una de estas tareas existen diferentes tipos de herramientas que nos provee el sistema operativo Linux.

### Listar

Sirve para ver el contenido dentro de un directorio, aunque también podemos listar un archivo en particular. Para esto contamos con el comando ls:
```
•ls – lista el contenido de un directorio 
  • uso: ls [flags]<path>
  • Flags: 
  • -l: lista detallada, muestra permisos, dueño, peso y fecha de modificación. 
  • -t: ordena los archivos por fecha de modificación. 
  • -r: invierte el orden del listado. 
  • -R: recursivo, lista el contenido de subdirectorios. 
  • -a: muestra archivos ocultos. (aquellos que comienzan con un “.”)
```

### Copiar

Sirve para generar un archivo o directorio idéntico en base a un archivo o directorio ya existente, ya sea para modificarlo o para conservar un resguardo del original por cualquier tipo de necesidad. Para esto contamos con el comando cp:
```
•cp – copia de archivos y directorios 
  • uso: cp [flags] <origen> <destino>
  • Flags: 
  • -r : recursivo, se usa para directorios y su contenido 
  • -f: forzar la acción • -p: mantener los permisos originales 
  • -i: interactivo, consulta por cada archivo
```

### Mover

Al mover un archivo o directorio estamos cambiándolo de ubicación, dejando de existir el archivo o directorio original. También se usa para renombrar un archivo o directorio.
```
•mv – mover archivos y directorios 
  • uso: mv [flags] <origen> <destino>
  • Flags: 
  • -f : forzar la acción 
  • -i: interactivo, consulta por cada archivo. 
  • -v: verboso, muestra un resumen de la operación
```

### Crear directorios

Podemos crear un nuevo directorio con el comando mkdir:
```
•mkdir – crea directorios 
  • uso: mkdir [flags]<path>
  • Flags: 
  • -p: genera la ruta previa si no existe
```

### Remover

Podemos eliminar de forma permanente archivos o directorios con el uso del comando rm:
```
•rm – remueve archivos y directorios 
  • uso: rm [flags] <archivo/path>
  • Flags: 
  • -r : recursivo, se usa para directorios y su contenido 
  • -f: forzar la acción 
  • -i: interactivo, consulta por cada archivo/directorio
```

### Cambiar de directorio

Podemos movernos entre directorios y recorrer la estructura de los mismos con el uso del comando cd.
```
• cd – moverse en el árbol de directorios 
  • uso: cd
```
```
•pwd - indica en qué directorio me encuentro actualmente
```

## Paths absolutos y relativos.

Un path (ruta en inglés) es el recorrido que realizamos a la hora de movernos de directorios. Podemos diferenciar ese path en dos tipos:

-Absoluto: Es el camino completo a ese directorio (o archivo) comenzando desde el directorio raíz (/), por ejemplo: /var/log/messages, es la ruta completa del archivo “messages” (archivo de log principal del sistema).

-Relativo: En cambio un path relativo comienza sin él “/”, es la ruta para llegar a un archivo o directorio pero desde donde uno está parado en ese momento, por ejemplo, nos encontramos parados en el directorio /var, la ruta relativa para llegar al archivo “messages” seria: log/messages.

#### Ejercicios

1) generar en el directorio de trabajo del usuario root un directorio llamado PRUEBA. 
2) Crear los directorios dir1, dir2 y dir3 en el directorio PRUEBA. 
3) Dentro de dir1 crear el directorio dir11. 
4) Dentro del directorio dir3 crear el directorio dir31. 
5) Dentro del directorio dir31, crear los directorios dir311 y dir312. 
6) Copiar el archivo /etc/motd a un archivo llamado mensaje dentro directorio /root/PRUEBA. 
7) Copiar "mensaje" dentro de los directorios dir1, dir2 y dir3 (recuerde la estructura generada en los puntos 2,3,4 y 5). 
8) Comprobar el ejercicio anterior, usando solamente un comando. 
9) Copiar el contenido del directorio /etc/rc.d dentro del directorio dir31 (recuerde la estructura generada en los puntos 2,3,4 y 5). 
10) Copiar en el directorio dir311 los archivos de /bin que comiencen con la letra “a”. 
11) Mover el directorio dir31 y sus subdirectorios debajo de dir2. 
12) Borrar los archivos y directorios de dir1, incluido el propio directorio.

#### Ejercicios

1) Crear un directorio “A” que contengan otros 3 directorios dentro (B,C y D). 
2) dentro de “B” generar dos directorios (E,F). 
3) Dentro de “D” generar el directorio “G”. 
4) Copiar el contenido del directorio “B” dentro de “G”. 
5) Ir hasta el directorio “G” y comprobar con el comando “ls” el punto anterior. 
6) Remover el directorio “B”, usando paths absolutos. 
7) comprobar el contenido del directorio “A”. 
8) Armar el directorio “B” tal cual estaba antes de ser borrado


## Comodines y expresiones regulares

Son patrones de agrupación. Sirven para trabajar con archivos o directorios según diferentes criterios de aglomeración. Permiten ahorrar tiempo en operaciones repetitivas y muy vulnerables a fallas humanas

-?
Representan un solo carácter. Ej: “clase1”, “clase2”, “clase3” puede ser representado con “clase?”.

-*
Muy amplia representación que pueden tomar, pueden ser nada o N cantidad de caracteres. Ej: “clase1”, “clase2”, “clase3”, “class1”, “class2”, “clase”, “club”. Puede ser representado con “cl*”

-\[-]
Representa un rango de caracteres o números. Ej: clase1”, “clase2”, “clase3” puede ser representado por “clase\[1-3]”. No todos los comandos lo pueden usar.

-\[!] 
Es el mismo caso anterior, pero negado, ósea que representa todo lo que está fuera del rango. No todos los comandos los puede usar.

-{}
Representa un conjunto de expresiones regulares separadas por comas. Ej: “clase1”, “clase2”, “club1”, “club2” es representado por cl{a*,u*}. De esta forma, comandos como mkdir o touch pueden usar rangos numéricos: 
```bash
mkdir dir{1..5}
```

-\
Es una secuencia de escape, el carácter siguiente lo tomara como texto sin interpretar. Ej: Para generar un directorio cuyo nombre contenga un espacio, podríamos ejecutar: 
```bash
mkdir laboratorio\ 1
```
Sin usar "\\" generaría dos directorios. 

-^
Principio de línea. Ej: Si tengo los archivos clase1, clase2, club1, club2, podría listarlos a todos con: 
```bash
ls ^cl
```

## Búsqueda de archivos

Comprende una colección de herramientas que nos permiten encontrar archivos o directorios según patrones que vayamos definiendo. Tiene gran utilidad para la gestión de grandes volúmenes de información.

### Locate

Es una herramienta de búsqueda de archivos y directorios que viene preinstalada en algunas distribuciones de Linux. Buscar archivos rápidamente debido al uso de una base de datos local, donde contiene una lista de todos los directorios y su path absoluto, lo negativo es que esa base de datos no se encuentra actualizada en tiempo real, sino que es asíncrona.
```
• Locate – búsqueda de archivos. 
  • uso: locate [flags] <archivo>
  • Locate hace uso de una base de datos local que se actualiza periódicamente, pero      también podemos forzarlo con el comando updatedb 
  • Flags: 
  • -d: ruta de búsqueda
```
<mark style="background: #CACFD9A6;">Ejemplo</mark>: Búsqueda de un archivo llamado “sistemas1”
```
locate sistemas1
```
<!---Arrojará como devolución al comando, la ruta completa del archivo.--->

### Find

Se puede realizar búsquedas en tiempo real de archivos y directorios basadas en gran cantidad de características de los mismos, como su nombre, tipo de archivo, fecha de creación, etc. Hay una propiedad de este comando que nos permite realizar acciones sobre los resultados de las búsquedas que realizamos

```bash
• Find – búsqueda de archivos. 
• uso: find<path> [flags] <argumentos>
• Flags: 
• -name: nombre del archivo. 
• -iname: nombre del archivo sin tener en cuenta mayúsculas y minúsculas. 
• -mtime: tiempo de modificación (días) 
• -mmin: tiempo de modificación (minutos)
• -newer : archivo modificado más recientemente con respecto a <file>
• -exec: realizar comandos sobre las búsquedas. Ej: find / -name -exec ls -l {}\;
```
<mark style="background: #CACFD9A6;">Ejemplo</mark>: Buscar archivos alojados en el directorio “/root” llamados “sistemas1”
```
find /root -name sistemas1 /root/sistemas1
```
<mark style="background: #CACFD9A6;">Ejemplo</mark>: Buscar archivos alojados en el directorio “/root” llamados “sistemas1”, sin discriminar entre mayúsculas y minúsculas
```
find /root -iname sistemas1
```
<mark style="background: #CACFD9A6;">Ejemplo</mark>: Buscar directorios llamados “sistemas1” dentro del directorio “/root”, sin discriminar entre mayúsculas y minúsculas
```
find /root -type d -iname sistemas1 /root/SISTEMAS1
```
<mark style="background: #CACFD9A6;">Ejemplo</mark>: Buscar todos los archivos llamados “sistemas1” dentro del directorio “/root”, sin discriminar entre mayúsculas y minúsculas, para luego borrarlos
```
find /root -type f -iname sistemas1 -exec rm -f {} \; 
```

## Redirección y tuberías

### Data Stream

#### Standard Input o STDIN

Es la entrada estándar de datos. Se realiza por medio del teclado al escribir. Ej. Un comando es representado por un “0”

#### Standard Ouput o STDOUT

Es la salida estándar de datos. Se visualiza por medio de la pantalla. Ej. El resultado de un comando es representado por un “1”

#### Standard Error o STDERR

Es la salida estándar de mensajes de error en la ejecución de un comando. Es presentado por un “2”

### Redirección

Es el desvío del tránsito estándar de la información

<mark style="background: #CACFD9A6;">Ejemplo</mark>: Para redireccionar la salida estándar hacia un archivo, se utiliza ”>”
```
ls -l > listado.txt
```
Para leer el contenido del archivo "listado.txt"
```
cat listado.txt
```
<mark style="background: #CACFD9A6;">Ejemplo</mark>: Si ejecutamos un comando y nos arroja un error, podemos redirigir ese mensaje a un archivo. 
```
ls -l nofile 2> error.txt
```
<!---En pantalla no se vera el mensaje de error, pero sabemos que el archivo "nofile" no existe--->
Para leer el contenido del archivo "error.txt"
```
cat error.txt
```
<!---El mensaje de error que nos habría aparecido en pantalla, lo veremos en el interior del archivo--->

### Tubería

Sirve para combinar la salida de un comando y usarlo de entrada para otro comando, es útil para trabajar con información en tiempo real y dinámica. Es representado por una “|”

<mark style="background: #CACFD9A6;">Ejemplo</mark>: Tenemos un directorio que cuenta con los archivos: "archivo1", "archivo2", "archivo3", "archivo4", "archivo5".
Para saber la cantidad de archivos que tengo, puedo usar el comando wc (Word Count) para contar, con la opción “-l” cuento las líneas
```
ls | wc -l
```
<!---Usando la salida del comando “ls”, servirá como entrada para el comando “wc”. Este cuenta la cantidad de líneas, por lo cual tengo 5 archivos que es igual a 5 líneas--->

#### Ejercicios 

1) Generar 10 directorios, clase1-5 y club1-5 usando comodines {}. 
2) Generar 20 archivos, laboratorio0-9, comision0-9 usando comodines {}. Nota: para crear archivos vacíos se puede usar el comando touch. 
3) copiar todos los archivos laboratorioX dentro del directorio clase1 usando comodines. 
4) copiar los archivos comisionX, de la siguiente forma: los dos primeros en el directorio club1, los dos siguientes a club2, así hasta copiar todos los archivos comisionX. Usando comodines. 
5) listar todos los directorios clubX y claseX de forma recursiva. Usando comodines. 
6) Buscar todos los archivos que comiencen con las letras “ar” dentro del directorio /usr (y subdirectorios dentro de /usr). 
7) Crear un directorio llamado “ejercicio” dentro del directorio /tmp y copiar todos los archivos encontrados en en el punto 1, usando el comando find. 
8) Usar el comando find para encontrar los archivos más viejos a 90 días, dentro del directorio /etc. 
9) Usar el comando find para encontrar todos los archivos más nuevos a 90 días, dentro del directorio /etc 
10) Buscar los archivos más viejos a 100 días en todo el árbol de directorios, redirigir los resultados de las búsquedas a un archivo llamado resultado.txt

## Visualización de textos

### Cat

Se usa para concatenar el contenido de dos o más archivos en un único archivo. También se puede utilizar como argumento un solo archivo y muestra su contenido en pantalla.
```
cat cat.txt
```
<!---Muestra el contenido de un archivo de texto en pantalla--->

### Less

Sirve para visualizar texto plano en una interfaz dedicada que soporta componentes como es la búsqueda y la navegación de texto de un archivo determinado. Esta herramienta cuenta con diferentes teclas. Como para la navegación, con el uso de las teclas ←↑↓→, o moverse entre páginas del archivo, con (space). Para salir del visualizador less, se usa la tecla “q”
<mark style="background: #ABF7F7A6;">Estructura</mark>;
```
less <archivo>
```
<mark style="background: #CACFD9A6;">Ejemplo</mark>:
```
less less.txt
```
<!---Se usa para visualizar el contenido de un archivo de texto en pantalla less.txt (END)--->

### More

Al igual que el comando less, se usa para ver en pantalla el contenido de un archivo de texto, podemos desplazarnos en el mismo o incluso hacer búsquedas de palabras claves.
<mark style="background: #D2B3FFA6;">Estructura</mark>;
```
more <archivo>
```
<mark style="background: #CACFD9A6;">Ejemplo</mark>:
```
more more.txt
```
<!---Se usa para visualizar el contenido de un archivo de texto en pantalla--->

### Editor vi

Es un editor de textos y uno de los más utilizados, viene preinstalado en la mayoría de las distribuciones Linux. Es una poderosa y  versátil herramienta, su curva de aprendizaje es un poco lenta, pero una vez adoptado su uso es sumamente útil. Posee dos modos de operación, el modo “comandos” y el modo edición con la tecla "i".

### Modo comandos de vi

Está por defecto una vez que lo ejecutamos, en este modo podemos usar teclas o combinación de las mismas para realizar diferentes tipos de acciones. También podemos extender el uso escribiendo expresiones propias de vi.

#### Teclas de acción del editor de textos vi <!---Los mas usados--->

| Tecla | Accion |
|----------|----------|
| h | Moverse un carácter hacia la izquierda | 
| j | Moverse una línea hacia abajo | 
| k | Moverse una línea hacia arriba | 
| l | Moverse un carácter a la derecha | 
| w | Moverse una palabra a la derecha | 
| b | Moverse una palabra a la izquierda | 
| e | Moverse al final de la palabra actual |
| Enter | Moverse una línea hacia abajo | 
| Back Space | Moverse un carácter a la izquierda | 
| gg | Moverse al principio del archivo | 
| G | Moverse al final del archivo | 
| i | Insertar caracteres a la izquierda del cursor | 
| a | Insertar caracteres a la derecha del cursor | 
| A | Insertar caracteres al final de la línea | 
| l | Insertar caracteres al principio de la línea | 
| o | Insertar una línea por debajo el cursor | 
| O | Insertar una línea por encima del cursor | 
| cw | Cambiar una palabra a la derecha del cursor | 
| c | Cambiar una línea |
| r | Cambiar un caracter por otro | 
| u | Deshacer el comando anterior | 
| U | Deshacer todos los cambios de una línea actual | 
| x | Eliminar el carácter del cursor | 
| X | Eliminar el carácter a la izquierda del cursor | 
| dw | Eliminar la palabra a la derecha del cursor | 
| dd | Eliminar la línea donde está el cursor | 
| 2dd | Eliminar dos líneas desde el cursor | 
| D | Eliminar la parte de la línea a la derecha del cursor | 
| Dg | Eliminar hasta el final de línea | 
| dG | Eliminar hasta el final del archivo | 
| yy | Copiar línea | 
| 2yy | Copiar dos líneas desde el cursor | 
| p | Pegar la línea copiada por debajo del cursor | 
| /string | Buscar una cadena de texto | 
| :%s/buscar/reemplazar/g | Reemplazar texto en base a patrones | 
| :q | Salir sin guardar | 
| :q! | Salir sin guardar forzando la acción | 
| :wq | Salir y guardar | 
| :wq! | Salir y guardar forzando la acción | 
| :x! | Guardar y salir forzando la acción | 
| ZZ | Salir y guardar | 


## Búsqueda de patrones

Configuraciones y comportamientos del sistema operativo Linux se pueden controlar en base a ficheros de texto, también podemos obtener información de los ficheros de registros (logs). Para encontrar una información concreta en base a patrones existe la herramienta llamada grep.
  El comando grep viene del sistema operativo Unix. Su funcionamiento es tomar como entrada una expresión regular (patrón) y buscarla en el archivo que indiquemos.
```bash
• grep – búsqueda de patrones. 
  • uso: grep [flags] <patrón> <archivo>
  • Flags: 
  • -i: no hace distinción entre mayúsculas y minúsculas. 
  • -v: excluye de la búsqueda el patrón que sigue. 
  • -r: recursivo, busca en directorios y subdirectorios. 
  • -e: uso de múltiples patrones. 
  • -f: file, puedo usar un archivo como entrada de los patrones.
```
<mark style="background: #CACFD9A6;">Ejemplo</mark>: Tengo un archivo con la siguiente información.
```
laboratorio 
LABOratorio 
laboRATORIO 
esto es un laboratorio 
ESTO es UN LABORATORIO 
laboral 
LABORAL
```
Para encontrar las líneas que contengan la palabra “laboratorio”
```bash
grep laboratorio texto.txt
```
Si no queremos diferenciar entre mayúsculas y minúsculas
```bash
grep -i laboratorio texto.txt
```
Se puede extender grep con el uso de expresiones regulares. 
Si queremos encontrar las líneas que comienzan con la palabra “laboratorio” sin diferenciar entre mayúsculas y minúsculas
```bash
grep -i ^laboratorio texto.txt
```

#### Ejercicios 

1) Generar un archivo llamado “texto” dentro del directorio /tmp con el siguiente contenido: 
```
texto 
TEXTO 
esto es un texto 
EsTo Es Un TeXto 
ESTO ES UN TEXTO 
laboratorio 
LABOratorio 
LABORATORIO 
```
3) Usar el comando grep para encontrar las líneas que contengan la palabra “texto” solamente con minúsculas. 
4) Usar el comando grep para encontrar las líneas que contengan la palabra “texto” solamente con MAYÚSCULAS. 
5) Encontrar las líneas que contengan solamente la palabra “LABOratorio”.


## Comandos

### Cpio 
Para crear un único archivo en base a otros archivos
```
cpio archivo1 archvo2 archivo3 > archivo_final
```

### Bzip
Es un librería de compresión, una evolución de gzip. Tiene mayor nivel de compresión en archivos de texto plano
```
bzip2 -9
```

### Zxip
Es librería de compresión, evolución de gzip. Tiene mayor nivel de compresión en archivos de texto plano.
```
xzip -9
```

### Cat
Es una herramienta para concatenar archivos. si solo indico un archivo, enseñara su contenido en pantalla
<mark style="background: #ABF7F7A6;">Estructura</mark>;
```
cat <archivo>
```
<mark style="background: #CACFD9A6;">Ejemplo</mark>:
```
cat archivo1 archivo2 archivo3 > archivo_final
```

### Zcat
Misma funcionalidad de cat, pero puede leer archivos comprimidos con gzip

### Bzcat
Misma funcionalidad de cat, pero puede leer archivos comprimidos con bzip

### Xzcat
Misma funcionalidad de cat, pero puede leer archivos comprimidos con xzip

## Comodines y expresiones regulares

• Son patrones de búsqueda. 
• Se usan para simplificar búsquedas. 
• Son muy útiles a la hora de realizar acciones repetitivas o masivas. 
• Muchos comandos pueden interactuar con comodines. 
• Las expresiones regulares son mas complejas de utilizar

### Comodines mas usados

• ?
Representan un solo carácter. 
Ej. “clase1”, “clase2”, “clase3” puede ser representado con “clase?”

• *
Amplia representación que pueden tomar, pueden ser nada o n cantidad de caracteres. 
Ej. “clase1”, “clase2”, “clase3”, “class1”, “class2”, “clase”, “club”. Puede ser representado con “cl*”

• \[]
Representa un rango, de caracteres o números. 
Ej. "clase1”, “clase2”, “clase3” puede ser representado por “clase\[1-3]”. 
<!---No todos los comandos lo pueden usar--->

### Comodines mas usados

• \[!]
Es el mismo caso anterior \[], pero negado. Representa todo lo que esta afuera del rango. 
<!---No todos los comandos los puede usar--->. 
En el ejemplo anterior se puede representar por clase\[!1-3] (mostrara clase4 y clase5).
<mark style="background: #FFF3A3A6;">Nota</mark>: Según el tipo de Shell habrá que agregar “\!.”

• {}
Representa un conjunto de expresiones regulares separadas por comas. 
Ej. “clase1”, “clase2”, “club1”, “club2” es representado por c{la*,lu*}
También lo puede usar el comando mkdir para generar multitud de directorios
```
mkdir clase{1,2,3,4,5}
```

• \
Es una secuencia de escape, el carácter siguiente lo tomara como texto sin interpretar. 
Ej. Si se quiere generar un directorio cuyo nombre contenga un espacio,
```
mkdir laboratorio\ 1
```
<!---Sin usar “\” generaría dos directorios--->

## Compresión de archivos

• La compresión de archivos es muy utilizada para la gestión de los mismos. 
• Podemos ahorrar espacio de archivos no accedidos frecuentemente. 
• Facilitan el traspaso de los mismos. 
• Es una forma rudimentario de resguardo.

```
tar – empaquetar archivos 
• uso: tar [flags] <archivo.tar> <archivos>
• Flags: 
• -c: crear tar • -v: modo verbose 
• -f: forzar la acción 
• -x: desempaquetar 
• -z: comprime o descomprime el tar usando la librería gzip.
```

```
• gzip – comprimir archivos. 
• uso: gzip [flags] <archivo>
• Flags: 
• -9: el mejor porcentaje de compresion 
• -d: descomprimir un archivo ya comprimido 
• -f: forzar la acción
```

#### Ejercicios 

1) Utilizar los archivos y directorios realizados en el anterior ejercicio. 
2) Compactar los directorios clubX en un solo archivo club.tar 
3) remover los directorios clubX usando comodines. 
4) Comprimir todos los archivos laboratorio dentro del directorio clase1 usando gzip. 
5) Descompactar los directorios clubX

## Búsquedas de archivos. 

• Gran utilidad para buscar archivos según patrones. 
• Puede ayudar a determinar problemas que sucedan en el sistema 
• Diversas herramientas son utilizadas para ello.

```
• Locate – búsqueda de archivos. 
  • uso: locate [flags] <archivo>  
  • Locate hace uso de una base de datos local que se actualiza periódicamente, pero      también podemos forzarlo con el comando updatedb 
  • Flags: 
     • -d: ruta de búsqueda
```

```
• Find – búsqueda de archivos. 
  • uso: find <path> [flags] <argumentos>
  • Find es una potente herramienta, puede hacer búsquedas sobre diversos aspectos de       los archivos y no solamente el nombre, puede realizare acciones sobre las               búsquedas. 
  • Flags: 
    • -name: nombre del archivo. 
    • -iname: nombre del archivo sin tener en cuenta mayúsculas y minúsculas. 
    • -mtime: tiempo de modificación (días) 
    • -mmin: tiempo de modificación (minutos)
    • -newer : archivo modificado mas recientemente con respecto a <file>
    • -exec: realizar comandos sobre las búsquedas. Ej: find / -name -exec ls –l {}
```

```
• grep – búsqueda de patrones
  • uso: grep [flags] <patrón> <archivo>
    • Es un comando muy valioso a la hora de filtrar salidas de comandos o contenidos         de archivos.
  • Flags: 
    • -i: no hace distinción entre mayúsculas y minúsculas
    • -v: excluye de la búsqueda la patrón que sigue
    • -r: recursivo, busca en directorios y subdirectorios
    • -e: uso de múltiples patrones
    • -f: file, puedo usar un archivo como entrada de los patrones
```

```
• egrep – búsqueda de patrones. 
  • uso: egrep [flags] <patrón> <archivo>
     • Es una variante de grep (en desuso) es lo mismo que usar grep –E, ósea con              expresiones regulares extendidas
```

```
• fgrep – búsqueda de patrones. 
  • uso: fgrep [flags] <patrón> <archivo>
    • Es una variante de grep (en desuso) es lo mismo que usar grep –F, ósea sin              expresiones regulares, lo que lo hace mas rápido en traer las búsquedas.
```

## Comandos

### Wc (Word Count)

Sirve para contar palabras, caracteres, líneas, etc. de un documento. Su estructura es; 
**wc \<opciones> archivo**

<mark style="background: #CACFD9A6;">Ejemplo</mark>:
```
wc -l archivo
```

### Date

Para gestionar la fecha/hora del sistema. Su estructura es;
**date \<opciones>**

<mark style="background: #CACFD9A6;">Ejemplo</mark>:
```
date
```
<!---Muestra la hora y fecha actual--->

## Primer Examen

### Gestión de archivos

1) generar la siguiente estructura de directorios usando solamente 1 comando:
![[Pasted image 20230708201131.png]]
```
mkdir -p examen/{tema1/alumno{1..3}/ejercicio{1..2},tema2/alumno{4..6}/ejercicio{1..2}}
```

2) trabajando con la anterior estructura de directorios, generadas en el punto 1, usar solamente un comando para renombrar los directorios "alumnosX" a "alumnosX0", resultando la siguiente estructura:
![[Pasted image 20230708201305.png]]
```
find examen/* -depth -name "alumno*" -type d -execdir mv {} {}0 \
```

3) Trabajando con la misma estructura resultante del punto 2, generar 3 archivos llamados: archivo1, archivo2 y archivo3 dentro de cada directorio "ejercicio1"
```
find -name "ejercicio1" -exec touch {}/archivo{1..3} \;
```

4) como redirecciono un mensaje de standar error al archivo /tmp/standar_error.log?
```
"mensaje de error" 2> /tmp/standar_error.log
```

5) Usar el siguiente comando para generar un archivo de 1M: "fallocate -l 1M /tmp/archivo". Trabajando sobre ese archivo, usar las tres herramientas de compresión (gzip, bzip2 y xz) con el mayor nivel de compresión, para comprimir dicho archivo. Con cual herramienta de compresión se obtuvo el mejor resultado? haga la demostración.
```bash
Al realizar: 
gzip -9 /tmp/archivo 
bzip2 -9 /tmp/archivo 
xz -9 /tmp/archivo 
Con bzip2 obtuve un mejor resultado. 
Comprobandolo con: 
ls -ls archivo*
```

6) Generar un empaquetado llamado log.tar con el contenido del directorio /var/log. Escriba el comando.
```bash
tar -cf log.tar /var/log
```

7) Teniendo 3 archivos llamados: a1,a2 y a3, como sumo el contenido de los 3 en un archivo llamado a4?
```bash
cat a1 a2 a3 > a4
```

8) Como podría contar la cantidad archivos de un directorio? 
```bash
Por ejemplo: 
find /root -type f | wc -l 
o 
ls -a | wc -l
```

### Variables de entorno

9) Usando los conceptos vistos en la clase, cual seria una forma rapida de cambiar la shell que esta usando un usuario?
```bash
export SHELL="/bin/bash"
```

### Edición de textos

10) Teniendo un archivo de texto con el siguiente contenido, Como cambio las palabras "el examen" por "la evaluación" usando el editor de textos vi? nota: usar vi en modo comandos.
![[Pasted image 20230708201810.png]]
```
Luego de utilizar vi en el archivo y presionar i, se debe utilizar el comando: 
:s%/el examen/la evaluacion/g
```

# Segundo Examen

##



## Desarrollo

### Que es un proceso?

Es una serie de instrucciones que se ejecutan debido a un programa. Puede ser ejecutado por un usuario o por el mismo sistema operativo, en el segundo caso, ese proceso puede ser resultado de otro proceso. Cada proceso es sometido a un análisis de su prioridad, eso ayuda a dar orden a la cadena de ejecución que tiene el procesador

### PID

Cada proceso posee un código de identificación único en el sistema operativo, esto es conocido como PID (process ID), a medida que se van iniciando los procesos, se les asigna un número de PID, podemos interactuar con ellos mediante este código único. 

Cuando se inicia Linux, el primer proceso que es ejecutado es el mismo kernel, por lo tanto tiene asignado el PID “1”, y es el último proceso al ser detenido cuando el sistema se apaga. En anteriores versiones de Linux, el PID 1 se le asignaba al INIT, el sistema de gestión de procesos y servicios, en versiones recientes, es asignado a systemd

### Padres e hijos

Cuando un proceso inicia otro proceso, este se convierte en un proceso padre, un proceso padre puede tener más de un proceso hijo. Si por alguna razón un proceso padre es detenido abruptamente, dejará a los procesos hijos “huérfanos” y pasarán a depender del PID 1. Si un proceso padre es detenido de forma correcta, sus procesos hijos también lo harán.

### Procesos zombies

Es un proceso finalizado que ya no se ejecuta pero que sigue reconociéndose en la tabla de procesos (en otras palabras, tiene un número PID). Ya no se asigna espacio del sistema a dicho proceso. Los procesos zombie han sido cerrados o han salido y siguen existiendo en la tabla de procesos hasta que muere el proceso padre o se apaga el sistema y se reinicia. Los procesos zombie se visualizan como cuando se listan por el mandato ps

### Monitorización de procesos

Existen varias herramientas que nos permiten interactuar con los procesos, vamos a listar algunas de las más utilizadas.

#### Comando ps

Con el comando ps podemos obtener gran cantidad de información sobre los procesos, como nombre, PID, usuario dueño del proceso, memoria consumida, estado, etc.

| Comando | Acción | 
|----------|----------|
| ps -e | lista todos los procesos activos en el sistema | 
| ps -a | lista los procesos de todos los usuarios | 
| ps -u | muestra aspectos de procesos como uso de cpu, memoria | 
| ps -x | muestra procesos no controlados por alguna terminal | 
| ps -f | formato “forest” (bosque) muestra familias de procesos | 
| ps -l | formato largo | 
| ps -m | muestra información de la memoria | 

Las opciones mostradas anteriormente pueden ser combinadas
<mark style="background: #CACFD9A6;">Ejemplo</mark>:
```
[root@centos1 ~]# ps -ef 
UID PID PPID C STIME TTY TIME CMD 
root 1 0 0 15:54 ? 00:00:01 /usr/lib/systemd/systemd --switched-root --system --deserialize 22
```

<mark style="background: #ABF7F7A6;">Explicación</mark>;
* **UID**: es el usuario que es dueño del proceso. 
* **PID**: es el process ID. 
* **PPID**: es el PID del proceso padre. 
* **C**: uso de procesador. 
* **STIME**: start time, horario donde se ejecutó el proceso. 
* **TTY**: en que terminal se está ejecutando (si se ejecutó en alguna). 
* **TIME**: tiempo de ejecución. 
* **CMD**: comando que ejecuta ese proceso.

#### comando top

Enseña información sobre los procesos en ejecución en tiempo real. Con él podemos observar diversos aspectos del funcionamiento general del sistema operativo, como consumo total de CPU y memoria, haciendo enfoque en los procesos.

```bash
Tasks: 117 total, 1 running, 116 sleeping, 0 stopped, 0 zombie
%Cpu(s): 0.0 us, 6.2 sy, 0.0 ni, 93.8 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st
KiB Mem : 3880368 total, 3431812 free, 239320 used, 209236 buff/cache
KiB Swap: 9437180 total, 9437180 free, 0 used. 3413656 avail Mem 

PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND 
1 root 20 0 128292 6932 4196 S 0.0 0.2 0:01.26 systemd 
2 root 20 0 0 0 0 S 0.0 0.0 0:00.00 kthreadd 
4 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 kworker/0:0H 
5 root 20 0 0 0 0 S 0.0 0.0 0:00.02 kworker/u2:0 
6 root 20 0 0 0 0 S 0.0 0.0 0:00.09 ksoftirqd/0 
7 root rt 0 0 0 0 S 0.0 0.0 0:00.00 migration/0 
8 root 20 0 0 0 0 S 0.0 0.0 0:00.00 rcu_bh 
9 root 20 0 0 0 0 S 0.0 0.0 0:00.92 rcu_sched 
10 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 lru-add-drain 
11 root rt 0 0 0 0 S 0.0 0.0 0:00.08 watchdog/0 
13 root 20 0 0 0 0 S 0.0 0.0 0:00.00 kdevtmpfs 
14 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 netns 
15 root 20 0 0 0 0 S 0.0 0.0 0:00.00 khungtaskd 
16 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 writeback 
17 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 kintegrityd 
18 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 bioset 
19 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 bioset 
20 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 bioset 
21 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 kblockd 
22 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 md 
23 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 edac-poller 
24 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 watchdogd 
30 root 20 0 0 0 0 S 0.0 0.0 0:00.00 kswapd0 
31 root 25 5 0 0 0 S 0.0 0.0 0:00.00 ksmd 
32 root 39 19 0 0 0 S 0.0 0.0 0:00.05 khugepaged 
33 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 crypto 
41 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 kthrotld 
43 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 kmpath_rdacd 
44 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 kaluad 
45 root 0 -20 0 0 0 S 0.0 0.0 0:00.00 kpsmoused
```

Podemos observar dos grandes regiones, la primera con un resumen del estado general del sistema, como CPU, memoria, swap, cantidad de procesos activos, detenidos o zombies. En la segunda región tendremos un listado en tiempo real de los procesos, con gran cantidad de información, como por ejemplo PID, usuario dueño, prioridad, consumo de memoria y CPU y comando que generó ese proceso. 

## Prioridades

Para ser atendidos los procesos, se establece un sistema de prioridades a los mismos, según esa prioridad serán ejecutados en la cola de procesamiento que se envía al procesador. Esta prioridad es establecida numéricamente, con una escala que va desde -20 (negativo) hacia el 20 (positivo). Mientras más bajo sea el número, mayor prioridad tendrá.

### Comando Nice

Sirve para ejecutar un proceso con un determinado valor de prioridad. Si este no se aclara, lo hará con una prioridad neutra: 0

| Comando | Acción |
|----------|----------| 
| nice \<prioridad> \<comando> | ejecuta un comando con una prioridad dada |

<mark style="background: #CACFD9A6;">Ejemplo</mark>: 
Ejecutamos el comando cat con una prioridad neutra de 0 
```
nice cat
```

### Comando Renice

Sirve para cambiar la prioridad de ejecución de un proceso dado.

| Comando | Acción |
|----------|----------| 
| renice \<prioridad> \<PID> | cambia la prioridad del proceso indicado |

<mark style="background: #CACFD9A6;">Ejemplo</mark>: 
Cambiamos la prioridad del comando cat a -20 (mayor prioridad)
```bash
[root@centos1 ~] ps -ef | grep cat
root 4762 1657 0 21:29 pts/0 00:00:00 cat 
root 4799 1657 0 21:30 pts/0 00:00:00 grep --color=auto cat 
[root@centos1 ~] renice -20 -p 4762
4762 (process ID) old priority 0, new priority -20
```

### Ejercicios 

1. contar cuántos procesos corren actualmente en el sistema. 
2. listar todos los procesos del usuario root. 
3. crear un proceso y buscar su PID. 
4. cambiar la prioridad del proceso a la prioridad mas alta. 
5. cambiar la prioridad del proceso a la prioridad mas baja

## Gestores de paquetes

### Yum

• Es el administrador de paquetes incluido en Red Hat y sus derivados. 
• Con él podemos instalar, actualizar o remover paquetes. 
• Posee una base de datos local, recreada a partir de la información que sincronizan desde los repositorios. 
• esta base es actualizada cada vez que llamamos al comando yum.

| Comando  | Función  |
|---|---|
| yum install \<paquete>  | instala el paquete indicado  |
| yum install update <paquete  | actualiza el paquete indicado a la ultima versión  |
| yum remove \<update>  | desinstala el paquete indicado  |
| yum update  | actualiza todos los paquetes instalados  |
| yum check-update  | chequea por actualizaciones disponibles  |
| yum search \<paquete>  | hace una búsqueda de disponibilidad de un paquete  |
| yum whatprovides \<librería>  | busca que paquete contiene una librería  |
| yum clean \<opciones>  | elimina la base local de yum  |
| yum repolist  | lista los repositorios disponibles en el sistema  |
| yum list  | lista los paquetes disponibles  |

#### Manejo de repositorios

• Yum utiliza una serie de archivos con listas de repositorios disponibles en el sistema. 
• Se alojan en /etc/yum.repos.d/ 
• Estos archivos deben terminar el nombre con un .repo

### Apt

• Administrador de paquetes usados en distribuciones Debian y sus derivados. 
• Podemos actualizar, instalar, remover paquetes. 
• Al igual que yum, utiliza repositorios centralizados de software

| Comando  | Acción  |
|---|---|
| apt update  | actualiza la información local desde los repositorios  |
| apt install \<paquete>  | instala un paquete  |
| apt remove \<paquete>  | remueve un paquete  |
| apt purge \<paquete>  | remueve un paquete y todas sus configuraciones  |
| apt upgrade  | actualiza todos los paquetes instalados  |
| apt dist-upgrade  | actualiza el sistema operativo a una nueva versión  |
| apt search \<paquete>  | busca la disponibilidad de un paquete en los repositorios  |

#### Manejo de repositorios

• Los repositorios de apt se administran vía archivos de configuración. 
• Alojados en el directorio /etc/apt /sources.list.d /

## Dependencias

• Son paquetes necesarios para la instalación del primer paquete. 
• Los gestores de paquetes se encargan de satisfacer dichas dependencias. 
• Si no se instala la dependencia, el paquete que depende de ella no se instalará.

## Ejercicios 

1. Instalar el paquete httpd (apache)
2. Listar los paquetes instalados y corroborar que esté instalado el paquete httpd 
3. Remover el paquete httpd. 
4. Buscar que paquete provee la librería libXi
5. Buscar que paquetes hay disponibles con el nombre samba. 
6. Obtener la información del paquete samba

## ¿Qué es un servicio?

Es el encargado de controlar el ciclo de vida de uno o más procesos, con la posibilidad de monitorear su comportamiento en todo momento que este se encuentre corriendo

## Gestión de servicios: SysInit

Linux es un sistema operativo que heredo muchas características de sus antecesores, como por ejemplo UNIX. Por años el control de los servicios fue gestionado por SysInit (Init System V). 
SysInit era el encargado de controlar el ciclo de vida de los servicios. Para ello contaba con una estructura de directorios alojados en el /etc:

<mark style="background: #D2B3FFA6;">/etc/init.d/</mark>
Se alojaban los scripts para inicio y detención de daemons (como se denominaban a los encargados de levantar un proceso).

<mark style="background: #D2B3FFA6;">/etc/rc.0,1,2,3,4,5,6,7</mark>
Son directorios que contenían el comportamiento de los servicios en los diferentes RunLevels

### Runlevels

Este sistema estaba compuesto por diferentes modos de operación del sistema operativo, cada uno de ellos atienden a una necesidad específica. Mencionaremos los más importantes

<mark style="background: #FFF3A3A6;">Runlevel 0</mark>: 
Este modo es como opera el sistema operativo cuando es apagado, generalmente detiene todos los servicios y por último al PID 1, el proceso Init. 4 

<mark style="background: #FFF3A3A6;">Runlevel 1</mark>: 
Modo monousuario sin acceso a red. Este modo de Linux se usa para cuestiones de mantenimiento cuando el sistema operativo no puede iniciar correctamente. Inicia una mínima cantidad de servicios indispensables para poder realizar las acciones necesarias de mantenimiento. 

<mark style="background: #FFF3A3A6;">Runlevel 3</mark>: 
Modo multiusuario con acceso a red pero sin sesiones gráficas. Este modo es el más comúnmente usado en Linux, tendremos todas las características habilitadas pero sin acceso a sesiones gráficas. 

<mark style="background: #FFF3A3A6;">Runlevel 5</mark>: 
Modo multiusuario con acceso a red y sesión gráfica. tendremos todas las características habilitadas y con la posibilidad de iniciar sesiones gráficas. 

<mark style="background: #FFF3A3A6;">Runlevel 6</mark>: 
Este modo de operación controla el comportamiento cuando el sistema es reiniciado, contiene la secuencia de parada de servicios y su posterior inicio. Una vez iniciado el sistema operará según en que Runlevel se inicie por defecto.

---
Para cambiar a cualquier modo de operación en todo momento, se usaba el comando Init, seguro al Runlevel elegido. Por ejemplo;

Reiniciar el sistema
```bash
init 6
```

Apagar el sistema
```bash
init 0
```

Cambiar el modo multiusuario grafico
```bash
init 5
```

---
Para elegir el modo de operación que se iniciará por defecto había que editar el archivo /etc/inittab, donde la línea que decide esto es:

```
# The default runlevel. 
id:3:initdefault:
```

## La evolución: systemd

Systemd se utiliza en las versiones recientes de Linux para reemplazar a SysInit. Nos permite controlar no solamente los servicios desde un mismo framework sino también otros aspectos del sistema operativo, al mismo tiempo que interactúa directamente con el kernel. 
Usando esta herramienta podemos gestionar servicios, sockets (red), timers (programación de tareas) y cambiar aspectos del sistema operativo, como modo de operaciones.

### Dejando atrás los RunLevels

Con la adopción de systemd, dejó de usarse la distribución de modos de operación en runlevels, para ello se usan targets. Los targets agrupan varias unidades (units) y componen un espacio de trabajo como lo hacía un Runlevel. Los targets más comunes pueden ser: 

<mark style="background: #ADCCFFA6;">default.target</mark>: 
Es el target por defecto que iniciara con el sistema 

<mark style="background: #ADCCFFA6;">emergency.target</mark>: 
Inicia los recursos indispensables para entrar al sistema y realizar tareas de mantenimiento cuando este no inicia de forma correcta. 

<mark style="background: #ADCCFFA6;">multi-user.target</mark>: 
Es el modo más común en Linux, levanta completamente el sistema operativo con acceso multiusuario sin sesión gráfica. 

<mark style="background: #ADCCFFA6;">graphical.target</mark>: 
Es el modo de operación multiusuario con sesiones gráficas. 

<mark style="background: #ADCCFFA6;">halt.target</mark>: 
Se encarga de apagar el sistema. 

<mark style="background: #ADCCFFA6;">rescue.target</mark>: 
Modo monousuario sin acceso a red. 

<mark style="background: #ADCCFFA6;">reboot.target</mark>: 
Reinicia el sistema. 

<mark style="background: #ADCCFFA6;">halt.target</mark>: 
Apaga el sistema. 

---
Podemos cambiar el modo de operación en el próximo inicio con:

```
[root@centos1 ~] systemctl set-default
```

### Controlando servicios con systemd

Systemd tiene la capacidad de gestionar los servicios en Linux. Cada uno de los servicios que estén presentes en el sistema deberán estar declarados en el directorio **/usr/lib/systemd/system**, un archivo por cada servicio. Dicho archivo tiene una estructura definida, citemos por ejemplo el archivo de servicio de apache (httpd en CentOS):

```bash
[root@centos1 ~]# cat /usr/lib/systemd/system/httpd.service 
[Unit] 
Description=The Apache HTTP Server 
After=network.target remote-fs.target nss-lookup.target 
Documentation=man:httpd(8) 
Documentation=man:apachectl(8) 
[Service] 
Type=notify 
EnvironmentFile=/etc/sysconfig/httpd 
ExecStart=/usr/sbin/httpd $OPTIONS -DFOREGROUND 
ExecReload=/usr/sbin/httpd $OPTIONS -k graceful 
ExecStop=/bin/kill -WINCH ${MAINPID} 
# We want systemd to give httpd some time to finish gracefully, but still want 
# it to kill httpd after TimeoutStopSec if something went wrong during the 
# graceful stop. Normally, Systemd sends SIGTERM signal right after the 
# ExecStop, which would kill httpd. We are sending useless SIGCONT here to give 
# httpd time to finish. 
KillSignal=SIGCONT 
PrivateTmp=true 

[Install] 
WantedBy=multi-user.target
```
---
Podemos destacar que se encuentran divididos en secciones, estas secciones son:

>\->**\[Unit]**: donde describe el servicio en sí, documentación, descripción, etc. 
>\->**\[Service]**: donde están las acciones para iniciar, detener el servicio. 
>>     **ExecStart**: comando necesario para iniciar el servicio. 
>>     **ExecStop**: comando para detener el servicio. 
>\->**\[Install]**: define en qué target podrá ser ejecutado el servicio.

