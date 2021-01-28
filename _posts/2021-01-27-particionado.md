---
title: "Linux: Montaje de Particiones"
toc: true
toc_sticky: true
permalink: /particionado/
---

**¿Cómo crear particiones en Linux?**

A continuación, vamos a explicar 3 formas diferentes de crear particiones en un sistema operativo de Unix.

- Fdisk (programa desde la consola).
- Parted (programa desde la consola).
- GParted (mediante interfaz gráfica).

## FDISK: Cómo crear particiones en Linux desde la consola

> *🎥 Creación de particiones con fdisk*](https://www.youtube.com/watch?v=r4EEYhfzGUk&ab_channel=JoseLuisCalvo)*

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/r4EEYhfzGUk" frameborder="0"> </iframe>

> *🎥 Crear, Formatear y Montar Particiones con Comandos en Ubuntu*

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/-KNAe_7wwQ8" frameborder="0"> </iframe>

> **Fuente**: [Galisteo Cantero](https://www.galisteocantero.com/fdisk-como-crear-particiones-en-linux/)

En esta ocasión vamos a ver el uso de **fdisk** para aprender a **crear particiones en Linux** desde la línea de comandos. Hay herramientas como gParted, que nos permiten gestionar nuestros discos duros de forma visual, pero cuando trabajamos con servidores no tenemos entorno gráfico, por lo que es bueno conocer la herramienta fdisk.

En primer lugar, debes tener en cuenta que en un disco solo puedes tener 4 particiones primarias y una extendida que contenga muchas lógicas. Bien, pues una vez conectado nuestro disco, debemos ver que lo haya reconocido correctamente, y aquí, vamos a usar por primera vez fdisk:

```
fdisk -l
```

El comando anterior, nos va a mostrar todo nuestro sistema de archivos y ahí debe estar nuestro disco. En mi caso, tengo un solo disco, con una partición, y unos 10GB de espacio libre donde iremos haciendo la demostración. El disco es de 20GB

![Cómo crear particiones con fdisk](https://www.galisteocantero.com/wp-content/uploads/2018/10/como-crear-particiones-con-fdisk.png)

Nos devolverá bastante información, así que busca bien tu disco. Una vez localizado, en mi caso /dev/sda debemos tener en cuenta una cosa. Podemos encontrar:

```
/dev/sda
/dev/sda0
/dev/sda1
/dev/sda2
```

El disco duro es /dev/sda y el resto, son cada una de las particiones que tenga dicho disco, así que con fdisk, debemos trabajar con el disco duro y no con sus particiones.

Recuerda, que si te equivocas con algún cambio, **siempre puedes salir sin guardar** con la opción q. Dicho esto, podemos comenzar el particionado de nuestro disco con:

```
fdisk /dev/sda
```

Nos mostrará la interfaz de fdisk

![Usando fdisk para particionar](https://www.galisteocantero.com/wp-content/uploads/2018/10/usando-fdisk-para-particionar.png)

Es muy importante usar la ayuda que el propio programa nos ofrece, fíjate que te indica que pulses m para obtener ayuda, y ésta es realmente buena

![Ayuda de fdisk](https://www.galisteocantero.com/wp-content/uploads/2018/10/ayuda-de-fdisk.png)

Como puedes ver, la ayuda es bastante completa e intuitiva, de forma que no tenemos que salir de fdisk para consultar man u otras fuentes de ayuda. En primer lugar vamos a mostrar la tabla de particiones del disco, para ello, como ves en la ayuda, debes pulsar p

![Ver tabla de particiones con fdisk](https://www.galisteocantero.com/wp-content/uploads/2018/10/ver-tabla-particiones-con-fdisk.png)

Podemos ver que mis disco duro es de 20GB y que solo tengo una partición de tipo 83 Linux de 10GB creada. Pero, ¿Qué es eso del tipo 83 Linux? Si recurrimos de nuevo a la ayuda, puedes ver los tipos de particiones con la opción l.

![Ver tipos de particiones con fdisk](https://www.galisteocantero.com/wp-content/uploads/2018/10/ver-tipos-particiones-fdisk.png)

Donde podemos ver una lista de ID’s y el tipo de partición. Ahora, ya estamos en condiciones de **crear una nueva partición**, para ello, usaremos la opción n donde en primer lugar nos preguntará qué tipo de partición queremos crear, primaria o extendida

![Crear una partición con fdisk](https://www.galisteocantero.com/wp-content/uploads/2018/10/crear-una-particion-con-fdisk.png)

Vamos a crear una partición de tipo primaria pulsando la p y nos preguntará el número de partición. Automáticamente le asigna un secuencial que yo personalmente no suelo modificar, así que lo dejamos por defecto pulsando enter. A continuación, nos preguntará desde donde queremos que comience. Por defecto, si no indicamos nada, comenzará o bien al principio si no hay ninguna, o inmediatamente después de la que ya exista como en este caso, pulsamos enter sin poner nada. Por último, nos preguntará en qué sector termina la partición. Obviamente es complicado calcular el tamaño de una partición mirando el sector donde debe terminar, por ello, podemos indicar el tamaño con la nomenclatura +2GB por ejemplo, el tamaño que queramos. En mi caso, la crearé de ese tamaño.

![Particionando el disco con fdisk](https://www.galisteocantero.com/wp-content/uploads/2018/10/particionando-el-disco-con-fdisk.png)

Si volvemos a usar la opción p para ver la tabla de particiones veremos nuestra nueva partición

![Partición creada con fdisk](https://www.galisteocantero.com/wp-content/uploads/2018/10/particion-creada-con-fdisk.png)

Como se muesra, la partición se ha creado de tipo 83 Linux, pero imagínate que la queremos de tipo Windows. Si acudimos a la ayuda veremos que con la opción t podemos cambiar el tipo de una partición. Vamos a **cambiar el tipo de la partición** anterior. Pulsamos t. Nos preguntará qué partición queremos cambiar, elegimos la 2, recuerda que este es el secuencial que se le asigna cuando la estamos creando y por último nos preguntará el tipo de partición que deseamos. Si no nos acordamos, nos indica que con l podemos ver los tipos, vemos que para FAT32 es el tipo b. Si volvemos a mostrar las particiones con p podremos ver el cambio realizado.

![Cambiar tipo de partición con fdisk](https://www.galisteocantero.com/wp-content/uploads/2018/10/cambiar-tipo-particion-fdisk.png)

Ahora vamos a **crear una partición de tipo extendida** con el resto de espacio que tenemos, en mi caso 6GB. El proceso es exactamente igual que para la partición primaria pero seleccionando la opción e

![Crear una partición extendida con fdisk](https://www.galisteocantero.com/wp-content/uploads/2018/10/crear-una-particion-extendida-fdisk.png)

Como ves, le asigno el secuencia 3, comenzó después de la partición 2, la he creado de 6GB (o casi) y es de tipo Extendida. Esta última, no contiene nada, es simplemente una partición donde puedo crear más particiones dentro. Bien, vamos a **crear una partición lógica** dentro de nuestra extendida:

![Crear partición lógica con fdisk](https://www.galisteocantero.com/wp-content/uploads/2018/10/crear-particion-logica-fdisk.png)

Cómo puedes ver, le ha asignado el id 5, y la he creado de 3GB de tipo linux, podemos cambiar el tipo exactamente igual que en el resto de particiones. Para finalizar vamos a crear una última partición lógica con el espacio restante para tener todo nuestro disco particionado.

![Cómo crear particiones lógicas con fdisk](https://www.galisteocantero.com/wp-content/uploads/2018/10/como-crear-particiones-logicas-con-fdisk.png)

Fíjate que he intentado darle varios valores para tomar todo el espacio disponible y me ha dado error, pero si te fijas, por defecto, toma el último sector del espacio libre, por lo que con solo pulsar enter, tomará todo el espacio libre.

Por último, también puedes borrar una partición. Para esto, usamos la opción p y lo único que nos preguntará es el id el a partición que deseamos eliminar.

Con esto ya tenemos todo nuestro disco particionado. Tenemos dos particiones primarias, una entendida, y dentro de ésta, dos particiones lógicas. Pero los cambios no están guardados aún, para ello, debemos usar la opción w

![Guardar particiones con fdisk](https://www.galisteocantero.com/wp-content/uploads/2018/10/guardar-particiones-fdisk.png)

Ahora sí se han aplicado todos los cambios a nuestro disco duro. Si sumas el tamaño de todas las particiones, es mayor a los 20GB que te dije que tenía mi disco duro. Esto es porque el tamaño de la partición extendida y de las lógicas que contiene, no se suman, es decir, si mi partición extendida tiene 6GB, las lógicas ocupan dicho espacio, por lo que las particiones lógicas no se suman.

Ten en cuenta que las particiones están creadas, pero no están formateadas por lo que es probable que tu sistema no las encuentre o las monte.

Puedes aprender más en nuestra [sección de Linux](https://www.galisteocantero.com/category/noticias-y-tutoriales/tutoriales-linux/).

## PARTED: Comandos

> Creado Por Juanjo y Ana 😹

Particionado de un disco en formato GPT a través del programa PARTED.

- `$ sudo su`
- `$ password`
- `$ fdisk –l`: Ver los discos que existen en el sistema.
- `$ parted /dev/sdd`: para entrar en el disco que quiero hacer las particiones
- `(parted)- mklabel gpt`

### Primera Partición

- (parted)- mkpart: poner nombre (Juanjo 1)
- Tipo de sistema de ficheros? ext4
- ¿Inicio? 1 ----ponemos donde empezara la 1ª partición
- ¿fin? 301

### Segunda Partición

- (parted)- mkpart: poner nombre (Juanjo 2)
- Tipo de sistema de ficheros? ext4
- ¿Inicio? 301 –Es el fin de la 1ª y comienzo de la 2ª
- ¿fin? 501

### Tercera Partición

- (parted)- mkpart: poner nombre (Juanjo 3)
- Tipo de sistema de ficheros? ext4
- ¿Inicio? 501 –Es el fin de la 2ª y el inicio del la 3ª
- ¿fin? 1101

### Cuarta Partición

- (parted)- mkpart: poner nombre (Juanjo 4)
- Tipo de sistema de ficheros? ext4
- ¿Inicio? 1101 - Fin de la 3ª y comienzo de la 4ª
- ¿fin? 100%: Se pone % para que sea todo el resto.

### Así con todas las particiones que queramos hacer

- `(parted)- quit`: para volver al modo root o `Cntrl+Z / Cntrl+C` para interrumpir el proceso.
- `$ root@juanjo-virtual-machine:/home/juanjo# fdisk –l`: para ver el listado de
discos con sus particiones.
- `root@juanjo-virtual-machine:/home/juanjo# lsblk –fm`: para ver el formato
de los discos con sus particiones.

### Relacionados Parted

¿Cómo administrar particiones con GNU Parted? 👇

- [Administrar particiones con GNU Parted](https://www.sololinux.es/administrar-particiones-con-gnu-parted/)

## Montar Particiones

Teniendo en cuenta de que ya hemos creado las particiones, debemos guardar el "nombre de las mismas" (/dex/xxx, /dev/sdbx) de cada una de las particiones primarias y lógicas creadas.

### Paso 1º: Damos formato a cada una de las particiones anteriores

`mkfs.ext4 /dev/xxx` o `mkfs.ext4 /dev/sbd1` o `mkfs.FormadoElegido /dev/NombrePartición`

### Paso 2º: Crear Carpetas

Debemos crear una carpeta en la ubicación para cada una de las particiones, dentro del lugar en el que las queramos montar. Existen dos posibilidades para hacer esto: 1. Movernos a la ruta en la queremos tener la carpeta, y crearla allí. 2. Crear la carpeta desde cualquier lugar en el que nos encontremos, marcando la ruta completa.

- Modo 1

`cd /mnt/`
`mkdir NombreCarpeta`

- Modo 2

`mkdir /mnt/NombreCarpeta`

### Parte 3º: Ejecutar el montaje

Utilizar el comando `mount -t` + formato dado a la partición `ext4` + ruta de la partición `/dev/sdbx` + ruta de montaje elegida `/mnt/NombreCarpeta`
El comando completo sería:

```mount -t ext4 /dev/sbdx /mnt/NombreCarpeta```

El comando debe de repetirse para cada partición y ruta.

### Parte 4º: Comprobar el montaje

Usando el comando `lsblk -f` o `df -h`

### Parte 5º: Desmontar una partición

Simplemente debes utilizar el comando `unmount /mnt/NombreCarpeta`

## Instalar GPARTED

- [🎥 Tutorial de como instalar Gparted mediante Comandos](https://www.youtube.com/watch?v=83RdL3Bncwo&ab_channel=JairoAriza)

- Menú de Mint > Gestor de Paquetes Synaptic > Buscar (buscar gparted) > Seleccionar los paquetes: gparted y gparted-common > Aplicar.
- Buscar el programa GPARTED en el Menú.

### Crear Particiones con GPARTED

- [🎥 Particionar con Gparted Basico](https://www.youtube.com/watch?v=qTlr-ebZd44&ab_channel=ZodzLinux)

## Tipos de Particiones de disco duro

> **Fuente**: [Región de Murcia](http://www.carm.es/edu/pub/04_2015/2_5_2_contenido.html#:~:text=Partici%C3%B3n%20extendida.,en%20un%20solo%20disco%20f%C3%ADsico.)

El **formato** o **sistema de archivo de una partición** (por ejemplo NTFS) no debe ser confundido con el **tipo de partición** (por ejemplo “partición primaria”), ya que en realidad no tienen directamente mucho que ver. A continuación se va a explicar cada término y sus características. [29]

![img](https://i.ibb.co/7Y0nQWj/imagen-1.jpg)

Independientemente del sistema de archivos de una partición (FAT, NTFS, ext3, ext4, etc.), si se habla de un disco duro que use **MBR, existen 3 tipos diferentes de particiones:** [32]

**Partición primaria:** Son las divisiones primarias del disco. En un disco duro, pueden existir de una a cuatro particiones primarias o hasta tres primarias y una extendida. Depende de una **tabla de particiones.** Un disco duro físico completamente formateado (por ejemplo, una unidad de disco duro externa USB nueva) consiste, en realidad, en una partición primaria que ocupa todo el espacio del disco y posee un sistema de archivos. Prácticamente, cualquier sistema operativo puede detectar este tipo de particiones primarias, y asignarles una unidad, siempre y cuando el sistema operativo reconozca su **formato (sistema de archivos).**

![img](https://i.ibb.co/ccs5RXt/imagen-2.jpg)

Disco duro con una única partición primaria.

![img](https://i.ibb.co/kQKDZKS/imagen-3.jpg)

Disco duro con cuatro particiones primarias.

La **partición primaria** puede ser reconocida como una partición de arranque y puede contener un sistema operativo que realice el arranque del equipo. Una de las particiones primarias se llama la **partición activa** y es la de **arranque**. El ordenador busca en esa **partición activa** el arranque del sistema. Cuando hay varios sistemas operativos instalados la partición activa tiene un pequeño programa llamado **gestor de arranque** que presenta un pequeño menú que permite elegir qué sistema operativo se arranca.

![img](https://i.ibb.co/PNGqwXR/imagen-4.jpg)

Gestor de arranque GRUB.

**Partición extendida:** También conocida como partición secundaria, es otro tipo de partición que actúa como una partición primaria; sirve para contener múltiples unidades lógicas en su interior. Fue ideada para romper la limitación de 4 particiones primarias en un solo disco físico. Solo puede existir una partición de este tipo por disco, y solo sirve para contener particiones lógicas. Por lo tanto, es el único tipo de partición que no soporta un sistema de archivos directamente.

![img](https://i.ibb.co/2Y34zQq/imagen-5.jpg)

Disco duro con tres particiones primarias y una extendida.

![img](https://i.ibb.co/4p2zyYF/imagen-6.jpg)

Disco duro con tres particiones primarias y cuatro extendidas.

**Partición lógica:** Ocupa una porción de la partición extendida o la totalidad de la misma, y se ha formateado con un tipo específico de sistema de archivos (FAT32, NTFS, ext3, ext4, etc.) y se le ha asignado una unidad, así el sistema operativo reconoce las particiones lógicas o su sistema de archivos. Se pueden tener un máximo de 23 particiones lógicas en una partición extendida. Aunque algunos sistemas operativos pueden ser más restrictivos, como Linux que impone un máximo de 15, incluyendo las 4 primarias, en discos SCSI y en discos IDE 8963.

### Relacionados

- [Tipologías de Discos Durso en Linux](/csi/discos-duros/)
- [Particionar Discos Duros en Linux](/csi/particionado/)