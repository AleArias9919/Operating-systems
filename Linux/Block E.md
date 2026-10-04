<img width="1345" height="644" alt="image" src="https://github.com/user-attachments/assets/123a0df4-cac3-4d68-80d3-c362e2f185e2" />## Bloque E: Redireccionamientos y Tuberías.

### 26) Cree un archivo de texto llamado cronologia.txt que contenga la fecha y hora actuales mediante el comando date y redirección . A continuación, ejecute un comando que liste los procesos activos en ese momento (ps) y anexe esos datos al final de cronologia.txt sin alterar la fecha previamente guardada. Verifique el contenido final del archivo.

```Python
Command:
date > cronologia.txt
ps >> cronologia.txt
cat cronologia.txt

Result:
Sat Oct 3 23:12:58 UTC 2026
    PID TTY      TIME CMD
    440 pts/0    ...  bash
   4384 pts/0    ...  ps

Note:
date muestra la fecha y hora actual, mientras que ps (process status) muestra los procesos asociados a la terminal.

> redirige la salida de un comando hacia un archivo, reemplazando su contenido.
>> también redirige la salida, pero la agrega al final sin borrar lo que ya existía.

Así, primero se guardó la fecha con > y luego se agregó la información de los procesos con >>.
```

### 27) Intente listar con ls un archivo inexistente en su directorio de conexión (por ejemplo, ls archivo_fantasma). Compruebe el error devuelto. Luego, repita el comando pero redirigiendo de forma exclusiva la salida de errores estándar (stderr) a un archivo llamado errores.log de manera que en la pantalla de la terminal no se visualice ningún mensaje de error .

```Python
Command:
ls archivo_fantasma
ls archivo_fantasma 2> errores.log
cat errores.log

Result:
ls: cannot access 'archivo_fantasma': No such file or directory

Note:
Los comandos tienen una salida normal y una salida de error separadas.

> redirige la salida normal.
2> redirige específicamente la salida de error (stderr).

Al ejecutar ls sobre un archivo inexistente, el error normalmente aparece en pantalla. Con 2> errores.log, ese error se guarda en el archivo errores.log.
```

### 28) Utilice la herramienta tee para listar por pantalla el contenido de su directorio personal y, al mismo tiempo, guardar una copia exacta de esa salida en un archivo llamado registro_personal.txt.

```
Command:
ls $HOME | tee personal_record.txt

Result:
Laboratorio01
identidad_nueva.txt

Note:
El símbolo | (pipe o tubería) toma la salida del comando de la izquierda y la utiliza como entrada del comando de la derecha.

tee recibe esa información y hace dos cosas al mismo tiempo: la muestra en pantalla y la guarda en un archivo.

Así, el listado de $HOME se mostró en la terminal y también quedó almacenado en personal_record.txt.
```

### 29) Conecte de manera secuencial mediante una tubería (pipeline) los comandos who y wc -l para calcular y mostrar por pantalla cuántos usuarios tienen una sesión activa actualmente en el sistema. Explique paso a paso el viaje de la información a través de esta tubería .

```
Command:
who | wc -l

Result:
0

Note:
who muestra las sesiones de usuarios registradas en el sistema.
wc (word count) permite realizar conteos y la opción -l cuenta líneas.

La tubería | toma la salida de who y la utiliza como entrada de wc -l. Por lo tanto, se cuenta una línea por cada sesión mostrada por who.

En este entorno WSL, who no mostró ninguna sesión registrada, por eso el resultado fue 0.
```

### 30) Muestre por pantalla las primeras 15 líneas del archivo de configuración del sistema /etc/passwd pero ordénelas alfabéticamente a través de una tubería. Detalle los comandos de la tubería utilizados .

```
Command:
head -n 15 /etc/passwd | sort

Result:
Las primeras 15 líneas de /etc/passwd se mostraron ordenadas alfabéticamente.

Note:
head -n 15 obtiene únicamente las primeras 15 líneas de /etc/passwd.

La tubería | pasa esas 15 líneas como entrada al comando sort.

sort ordena las líneas alfabéticamente. El orden de los comandos importa: primero se seleccionan las 15 líneas y después se ordenan.
```
