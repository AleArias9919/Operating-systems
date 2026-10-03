## Bloque D: Atributos, Permisos y Enlaces.

## 16) Ejecute un comando de listado largo sobre el archivo /etc/passwd. Interprete detalladamente cada uno de los campos que devuelve el sistema de izquierda a derecha.

```Python
ls -l /etc/passwd

Result:
-rw-r--r-- 1 root root 1386 Oct 2 00:56 /etc/passwd

Note:
-- La opción -l (long) de ls realiza un listado largo, mostrando información detallada del archivo.

-- Los campos se interpretan de izquierda a derecha:

-- -rw-r--r-- → tipo y permisos. El primer "-" indica que es un archivo regular. Los siguientes 9 caracteres se dividen en usuario, grupo y otros. r = lectura, w = escritura, x = ejecución y - = permiso no concedido.

-- 1 → cantidad de enlaces duros asociados al archivo.

-- root → usuario propietario. root es el superusuario de Linux, con privilegios especiales sobre el sistema.

-- root → grupo propietario del archivo.

-- 1386 → tamaño del archivo en bytes.

-- Oct 2 00:56 → fecha y hora de la última modificación.

-- /etc/passwd → nombre/ruta del archivo.
```

## 17) Cree un archivo llamado privado.txt en su directorio Laboratorio01. Utilice chmod en modo relativo (letras) para quitar todos los permisos de lectura y escritura para el grupo y otros, dejando el control total al propietario. Compruebe los permisos resultantes con ls -l.
#### Quitar permisos al grupo y a otros
```Python
chmod go-rw privado.txt

Result: -rw------- 1 alejandro alejandro 0 Oct 3 15:06 privado.txt

Note:
chmod (change mode) permite modificar los permisos de archivos y directorios.

En el modo simbólico:
u = user (propietario)
g = group (grupo)
o = others (otros)

Los operadores indican qué hacer:
+ agrega permisos
- quita permisos
= establece permisos específicos

En go-rw, "go" selecciona al grupo y a otros, "-" indica quitar y "rw" representa lectura y escritura. Por eso ambos quedan sin esos permisos.
```

#### Dar control total al propietario.

``` Python
chmod u+x privado.txt

Result:
-rwx------ 1 alejandro alejandro 0 Oct 3 15:06 privado.txt

Note:
Los permisos se representan con:
r = read (lectura)
w = write (escritura)
x = execute (ejecución)

u+x agrega al propietario el permiso de ejecución. Como ya tenía lectura y escritura, queda con rwx (control total).

El resultado final -rwx------ indica:
Propietario → rwx
Grupo → ---
Otros → ---
```

## 18) Modifique los permisos del archivo privado.txt utilizando chmod en modo absoluto (octal) de tal forma que el propietario tenga permisos de lectura y escritura (rw-), el grupo tenga únicamente lectura (r--), y otros no tengan ningún permiso (---). Escriba el comando correspondiente y la representación octal utilizada.

``` Python
chmod 640 privado.txt

Result:
-rw-r----- 1 alejandro alejandro 0 Oct 3 15:06 privado.txt

Note:
La notación octal permite representar los permisos mediante números:

r (read) = 4
w (write) = 2
x (execute) = 1

Los valores se suman para cada grupo de permisos y se escriben en el orden: propietario, grupo y otros.

En este caso:
6 = 4 + 2 → rw- → propietario puede leer y escribir.
4 = 4     → r-- → grupo puede solamente leer.
0         → --- → otros no tienen permisos.

Por lo tanto, 640 representa rw-r-----.

chmod puede utilizarse tanto con notación simbólica (u, g, o, +, -, =) como con notación octal.
```

## 19) Cree un directorio llamado compartido dentro de Laboratorio01. Asígnele permisos rwxr-x--- utilizando tanto el modo octal como el modo simbólico . Explique por qué el permiso de ejecución (x) es obligatorio en un directorio para que un miembro del grupo pueda ingresar a él.

#### Modo octal
``` Python
chmod 750 compartido

Result:
drwxr-x--- 2 alejandro alejandro 4096 Oct 3 16:09 compartido

Note:
En notación octal:
7 = 4 + 2 + 1 → rwx
5 = 4 + 1     → r-x
0             → ---

Por lo tanto, 750 establece:
Propietario → rwx
Grupo → r-x
Otros → ---
```

#### Modo simbólico
``` Python
chmod u=rwx,g=rx,o= compartido

Result:
drwxr-x--- 2 alejandro alejandro 4096 Oct 3 16:09 compartido

Note:
El operador = establece exactamente los permisos indicados.

u=rwx → propietario: lectura, escritura y ejecución.
g=rx  → grupo: lectura y ejecución.
o=    → otros: ningún permiso.

Ambas formas, octal y simbólica, producen los mismos permisos.
```

#### Permiso x en directorios

```Python
Note:
En un archivo, x representa permiso de ejecución. En un directorio, x permite atravesarlo: entrar mediante cd y acceder a los elementos que contiene.

Por eso, para poder ingresar a compartido, el usuario necesita permiso x sobre el directorio.

La "d" inicial de drwxr-x--- indica que compartido es un directorio.
```

## 20) Verifique el valor de su máscara de usuario actual ejecutando umask sin parámetros . ¿Cuál es su valor octal? Cambie la máscara temporalmente a 077 (limpiar todos los permisos para grupo y otros). Cree un directorio llamado super_seguro and un archivo llamado secreto.txt dentro de él. Verifique con qué permisos fueron creados ambos elementos. ¿Cómo influye la máscara en este proceso?

#### Consultar y modificar máscara.

```Python
umask

Result:
0022

umask 077

Result:
0077

Note:
umask determina qué permisos se eliminan por defecto al crear nuevos archivos y directorios.

Los permisos base son:
Archivos → 666 (rw-rw-rw-)
Directorios → 777 (rwxrwxrwx)

Con umask 077, no se quita ningún permiso al propietario (0), mientras que se eliminan todos los permisos del grupo (7) y de otros (7).
```

#### Crear elementos con umask 077
```Python
mkdir super_seguro
touch super_seguro/secreto.txt

Result:
super_seguro → drwx------ → 700
secreto.txt  → -rw------- → 600

Note:
La misma umask produce resultados distintos porque los permisos base son diferentes.

Directorio: 777 con umask 077 → 700 (rwx------)
Archivo:    666 con umask 077 → 600 (rw-------)

Los archivos normales no reciben permiso de ejecución (x) por defecto.
```

#### Restaurar máscara original.
```Python
umask 0022

Result:
0022

Note:
El cambio de umask era temporal para el ejercicio. Al finalizar se restaura el valor original 0022.
```

## 21) Restablezca su máscara a su valor original. Con los permisos de compartido en rwxr-x---, intente quitar el permiso de ejecución (x) para el propietario . Intente ingresar al directorio con cd compartido. ¿Qué mensaje obtiene? Restablezca el permiso de ejecución, luego quite el permiso de lectura (r) al propietario e intente listar el contenido del directorio (ls compartido). ¿Qué sucede? Explique detalladamente la diferencia de comportamiento .

#### Quitar permiso x:

```Python
chmod u-x compartido

Result:
cd compartido
bash: cd: compartido: Permission denied

Note:
En un directorio, el permiso x permite atravesarlo, es decir, entrar con cd y acceder a elementos de su interior.

Al quitar x al propietario con u-x, este conserva lectura y escritura, pero no puede ingresar al directorio. Al restaurarlo con chmod u+x compartido, vuelve a poder entrar.
```
#### Quitar permiso r:
```Python
chmod u-r compartido

Result:
ls compartido
ls: cannot open directory 'compartido': Permission denied

Note:
En un directorio, el permiso r permite leer/listar los nombres de los elementos que contiene.

Al quitar r pero conservar x, el propietario puede atravesar el directorio, pero no puede listar normalmente su contenido con ls.

Por lo tanto:
r → permite listar el contenido.
x → permite atravesar/entrar al directorio.
```

#### Restaurar los permisos:
```Python
chmod u+r compartido

Result:
El propietario vuelve a tener rwx.
```

## 22) En su directorio Laboratorio01, cree un enlace físico llamado enlace_duro que apunte al archivo identidad.txt que creó en el paso 6 [19, 118].

```Python
Command:
ln ../identidad.txt enlace_duro

Result:
-rw-r--r-- 2 alejandro alejandro 49 Oct 2 22:37 enlace_duro

Note:
- ln permite crear enlaces. Sin opciones, crea un enlace duro (hard link).
- Un enlace duro es un nuevo nombre que apunta a los mismos datos que el archivo original; no es una copia independiente.
- El número 2 en el listado largo indica que existen dos enlaces duros apuntando al mismo archivo: identidad.txt y enlace_duro.
```

## 23) En el mismo directorio, cree un enlace simbólico llamado enlace_blando apuntando al mismo archivo identidad.txt [19, 118].

```Python
Command:
ln -s ../identidad.txt enlace_blando

Result:
lrwxrwxrwx 1 alejandro alejandro 16 ... enlace_blando -> ../identidad.txt

Note:
La opción -s hace que ln cree un enlace simbólico. Un enlace simbólico es un archivo especial que guarda una ruta hacia otro archivo.

La letra l al comienzo indica que es un enlace simbólico y -> muestra hacia qué ruta apunta.
```

## 24) Ejecute ls -l y compare ambos enlaces creados junto con el archivo original:
#### -Compare los números de inodo de los tres archivos (use ls-i para visualizarlos directamente). ¿Qué observa? [19,118]

```Python
Command:
ls -l ../identidad.txt enlace_duro enlace_blando

Result:
-rw-r--r-- 2 alejandro alejandro 49 ... ../identidad.txt
lrwxrwxrwx 1 alejandro alejandro 16 ... enlace_blando -> ../identidad.txt
-rw-r--r-- 2 alejandro alejandro 49 ... enlace_duro

Note:
El enlace duro tiene el mismo tamaño que identidad.txt (49 bytes) porque ambos nombres hacen referencia al mismo archivo.

El enlace simbólico ocupa 16 bytes porque es un archivo diferente que almacena la ruta "../identidad.txt". La letra l indica que es un enlace simbólico y -> muestra hacia dónde apunta.3
```



#### -Compare los tamaños de los archivos mostrados en bytes. ¿Por qué el enlace simbólico tiene un tamaño tan reducido en comparación al archivo original? [19, 118]

```Python
Command:
ls -i ../identidad.txt enlace_duro enlace_blando

Result:
41922 ../identidad.txt
41926 enlace_blando
41922 enlace_duro

Note:
El inodo identifica internamente un archivo en el sistema de archivos.

identidad.txt y enlace_duro comparten el inodo 41922, confirmando que son dos nombres para el mismo archivo.

enlace_blando tiene su propio inodo (41926), ya que es un archivo independiente que contiene una referencia al original.
```

## 25) Elimine o renombre el archivo original identidad.txt. ¿Qué sucede al intentar leer el contenido del enlace físico? ¿Y al intentar leer el enlace simbólico? Explique detalladamente el comportamiento técnico de ambos.

#### Renombrar el archivo original:

```Python
Command:
mv ../identidad.txt ../identidad_nueva.txt

Note:
mv permite mover o renombrar archivos. Al cambiar el nombre del archivo original, podemos comprobar cómo reaccionan los dos tipos de enlaces.
```

#### Probar el enlace duro:
```Python
Command:
cat enlace_duro

Result:
Nombre: Alejandro
Apellido: Arias
Legajo: 30640

Note:
El enlace duro sigue funcionando porque no depende del nombre ni de la ruta original. Comparte el mismo inodo y continúa apuntando a los mismos datos.
```

#### Probar el enlace simbólico:
```Python
Command:
cat enlace_blando

Result:
cat: enlace_blando: No such file or directory

Note:
El enlace simbólico guarda una ruta hacia el archivo original. Como identidad.txt fue renombrado, esa ruta dejó de existir y el enlace quedó roto.

En resumen:
Enlace duro → referencia directamente al mismo archivo/inodo.
Enlace simbólico → referencia una ruta y puede romperse si el destino se mueve, renombra o elimina.
```
