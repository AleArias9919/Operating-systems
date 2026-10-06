### 1)Compruebe la ruta exacta de su directorio de conexión. Guarde este resultado.

```Python
alejandro@NotebookdeAle:~$ pwd

Result: /home/alejandro

Note: pwd (Print Working Directory) muestra la ruta absoluta del directorio actual. En este caso, /home/alejandro es mi directorio HOME.
```

### 2) Posiciónese en el directorio / (raíz). Ejecute un comando que muestre todos los archivos ocultos presentes en él.

```Python
alejandro@NotebookdeAle:~$ cd /
alejandro@NotebookdeAle:/$ ls -a
.  ..  bin  boot  dev  etc  home  init  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  snap  srv  sys  tmp  usr  var

Note: cd / posiciona en el directorio raíz   ---    ls -a lista todo su contenido, incluyendo las entradas ocultas.
```

### 3) Desplácese al directorio /bin y verifique con el comando apropiado qué terminal tiene asignada su sesión actual.

```Python
alejandro@NotebookdeAle:/$ cd bin
alejandro@NotebookdeAle:/bin$ tty
/dev/pts/0

Note: cd bin desplaza al directorio /bin. tty muestra la terminal asignada a la sesión actual.
```

### 4) Intente regresar a su directorio HOME usando tres variantes de comando diferentes (absoluta, relativa y por variable de entorno). Escriba las órdenes ejecutadas.

```Python
# Ruta absoluta
$ cd /home/alejandro

# Ruta relativa (desde /bin)
$ cd ../home/alejandro

# Variable de entorno
$ cd $HOME

Result: /home/alejandro

Note: Las tres órdenes llegan al mismo directorio: /home/alejandro.
- Ruta absoluta: indica el recorrido completo desde la raíz /. No importa dónde esté parado.
- Ruta relativa: indica el recorrido desde mi ubicación actual. .. representa el directorio padre.
- $HOME: es una variable de entorno que contiene la ruta del directorio personal del usuario. En mi caso, /home/alejandro.
- ~: representa también mi directorio HOME, por eso el prompt termina en :~$ cuando llego allí.
```


### 5) Cree la siguiente estructura de directorios dentro de su $HOME:
#### -Un directorio llamado Laboratorio01.
#### -Dentro de Laboratorio01, cree dos directorios llamados seguro y temporal.
#### -Dentro de temporal, cree un subdirectorio llamado basura

```Python
$ mkdir Laboratorio01
$ cd Laboratorio01
$ mkdir seguro
$ mkdir temporal
$ cd temporal
$ mkdir basura
$ ls

Result: basura

Note: mkdir (make directory) crea directorios. Los directorios pueden estar anidados formando una estructura jerárquica. cd permite desplazarse entre ellos y ls muestra el contenido del directorio actual. Una ruta que empieza con / es absoluta y parte desde la raíz; una que no empieza con / es relativa y parte desde el directorio actual.

Note: Directorio = carpetas
```
