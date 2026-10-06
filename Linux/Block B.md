# Bloque B: Gestión de Archivos y Visualización Parcial.

### 6) Dentro de su directorio HOME, cree mediante el comando cat y redireccionamiento un archivo de texto llamado identidad.txt que contenga únicamente su Nombre, Apellido y Legajo. Cierre elflujo usando la combinación de teclas adecuada.

``` Python
cd $HOME
cat > identidad.txt      //Crea archivo y te permite escribir sobre el
Nombre: Alejandro
Apellido: Arias
Legajo: 30640
[Ctrl + D]              //Para finalizar la escritura.

$ cat identidad.txt

Result:
Nombre: Alejandro
Apellido: Arias
Legajo: 30640

Note:
-mkdir se utiliza para crear directorios, mientras que cat trabaja con el contenido de archivos.
-cat archivo.txt muestra su contenido. Al usar cat > archivo.txt, cat recibe datos desde el teclado y > redirige esa información hacia el archivo; si no existe, se crea.
-Ctrl+D envía EOF (End Of File), indicando que terminó la entrada de datos; no es lo que “guarda” el archivo.
```

### 7) Copie el archivo /etc/passwd del sistema a su directorio Laboratorio01/seguro de dos maneras independientes:
#### -Método 1: Utilice únicamente rutas absolutas para el origen y el destino.

``` Python
cp /etc/passwd /home/alejandro/Laboratorio01/seguro

$ ls Laboratorio01/seguro

Result: passwd

Note: cp (copy) copia archivos siguiendo la estructura cp ORIGEN DESTINO.
-En este ejercicio se copia el archivo /etc/passwd al directorio seguro.
-Una ruta absoluta comienza desde la raíz /,
```

#### -Método 2: Ubíquese primero en su $HOME y copie usando rutas relativas.

``` Python
cp ../../etc/passwd Laboratorio01/seguro
ls Laboratorio01/seguro

Result: passwd

Note: cp (copy) copia archivos siguiendo la estructura cp ORIGEN DESTINO.
-En este ejercicio se copia el archivo /etc/passwd al directorio seguro.
Una ruta relativa se interpreta desde el directorio actual. .. representa el directorio padre y permite referirse a ubicaciones superiores sin tener que moverse con cd.
```

### 8) Muestre por pantalla de forma paginada el contenido del archivo passwd copiado dentro de su carpeta seguro. ¿Cuál es la tecla para salir de la visualización antes de llegar al final?
```Python
$ more Laboratorio01/seguro/passwd

Result:
Se muestra el contenido del archivo passwd de forma paginada.

Note: more permite visualizar el contenido de un archivo de forma paginada, a diferencia de cat, que muestra todo el contenido de una vez. Si el archivo ocupa más de una pantalla, Espacio avanza una pantalla, Enter avanza una línea y q (quit) permite salir antes de llegar al final. En este caso, passwd entra completo en la terminal, por lo que visualmente more y cat producen prácticamente el mismo resultado.
```

### 9) Extraiga únicamente las primeras 5 líneas del archivo passwd que copió en el paso anterior. Luego, extraiga las últimas 3 líneas. ¿Qué comando usó en cada caso?
#### Primeras 5 líneas:
``` Python
head -n 5 passwd

Result: Se muestran las primeras 5 líneas del archivo passwd.

Note: head permite visualizar el comienzo de un archivo y tail su final. Por defecto ambos muestran 10 líneas. La opción -n permite indicar una cantidad específica: head -n 5 muestra las primeras 5 líneas.
```

#### Últimas 3 líneas

``` Python
tail -n 3 passwd

Result: Se muestran las últimas 3 líneas del archivo passwd.

Note: Tail -n 3 las últimas 3. Estos comandos permiten consultar una parte del archivo sin modificar su contenido
```


### 10) Intente eliminar el directorio temporal que contiene el subdirectorio basura utilizando el comando rmdir. ¿Qué mensaje de error devuelve el sistema y a qué se debe? Explique cómo solucionarlo para realizar el borrado de forma interactiva (pidiendo confirmación para cada archivo/directorio)

#### Intento con rmdir:
``` Python
rmdir temporal

Result: rmdir: failed to remove 'temporal': Directory not empty

Note: rmdir (remove directory) se utiliza para eliminar directorios vacíos. Si el directorio contiene archivos o subdirectorios, no puede eliminarlo y devuelve el error "Directory not empty". En este caso, temporal contiene el subdirectorio basura.
```

#### Eliminación iterativa:
``` Python
rm -ri temporal

Result:
rm: descend into directory 'temporal'? y
rm: remove directory 'temporal/basura'? y
rm: remove directory 'temporal'? y

Note:
rm (remove) se utiliza para eliminar archivos y, con determinadas opciones, también directorios.
-r (recursive): permite eliminar un directorio junto con todo su contenido. El comando recorre la estructura desde adentro hacia afuera: primero elimina lo que contiene el directorio y luego el propio directorio.
-i (interactive): activa el modo interactivo. Antes de realizar cada eliminación, rm solicita una confirmación. Se responde "y" (yes) para aceptar.
Al combinar ambas opciones, rm -ri elimina directorios y su contenido de forma recursiva, pero solicitando confirmación en cada paso. En este caso primero entró en temporal, luego eliminó temporal/basura y finalmente temporal.
```
