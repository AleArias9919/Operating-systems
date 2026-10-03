# Moviéndose al directorio /bin o /etc (según se especifique), genere las expresiones compactas empleando comodines para listar únicamente: 

## 11) Todos los archivos en /bin que comiencen exactamente con las letras d o f. 
#### Nombres que comienzan con d:
``` Python
ls /bin/d*

Result: Se muestran los elementos de /bin cuyos nombres comienzan con d.

Note: Los comodines (wildcards) permiten seleccionar nombres que coincidan con un patrón. El comodín * representa cualquier cantidad de caracteres, incluso ninguno. Por eso, d* significa: nombres que comienzan con "d" y después pueden contener cualquier cantidad de caracteres.
```

#### Nombres que comienzan con f:
``` Python
ls /bin/f*

Result: Se muestran los elementos de /bin cuyos nombres comienzan con f.

Note: El patrón f* aplica la misma lógica: la "f" es un carácter fijo que debe aparecer al comienzo y * representa todo lo que pueda aparecer después. Los comodines son interpretados por el shell para encontrar los nombres que coinciden con el patrón antes de ejecutar el comando.
```

## 12) Todos los archivos en /bin cuyo nombre tenga exactamente cuatro caracteres. 

``` Python
ls /bin/????

Result: Se muestran los elementos de /bin cuyos nombres tienen exactamente 4 caracteres.

Note: El comodín ? representa exactamente un carácter cualquiera. A diferencia de *, que puede representar cualquier cantidad de caracteres, cada ? ocupa una única posición. Por eso, el patrón ???? exige que el nombre tenga exactamente 4 caracteres. Los comodines son interpretados por el shell antes de ejecutar el comando.
```


## 13) Todos los archivos en /etc que comiencen con las letras i y terminen exactamente con la letra b. 
``` Python
ls /etc/i*b

Result: ls: cannot access '/etc/i*b': No such file or directory

Note:
Los comodines pueden combinarse con caracteres fijos para formar patrones. En i*b, la "i" obliga a que el nombre comience con i, "*" representa cualquier cantidad de caracteres intermedios (incluso ninguno) y la "b" obliga a que termine con b.

En este sistema no existe ningún elemento de /etc que coincida con el patrón, por eso ls devuelve "No such file or directory". Esto no significa que el patrón sea incorrecto: el resultado depende de los archivos y directorios existentes en cada sistema.

Además, cuando ls recibe como resultado un directorio, normalmente muestra su contenido. La opción -d permite listar el nombre del directorio en sí, sin mostrar lo que contiene.
```
#### Ejemplo que si funciona
``` Python
ls /etc/c*y

Result:
/etc/chrony
/etc/cron.daily
/etc/cron.hourly
/etc/cron.monthly
/etc/cron.weekly
/etc/cron.yearly

Note: En este caso el patrón sí encuentra varias coincidencias. Como los resultados son directorios, ls muestra también el contenido de cada uno. Para mostrar únicamente los nombres de los directorios coincidentes puede utilizarse la opción -d:

```


## 14) Todos los archivos en /bin cuyo nombre comience por t y finalice exactamente en la letra r. 

``` Python
ls /bin/t*r

Result: /bin/tar  /bin/tr

Note:
-El patrón t*r selecciona elementos cuyo nombre comienza con "t" y termina con "r", permitiendo cualquier cantidad de caracteres entre ambos mediante *.
-El patrón por sí solo no es un comando. Debe utilizarse como argumento de un comando, por ejemplo ls. Si se escribe /bin/t*r directamente, el shell expande el patrón e intenta ejecutar las coincidencias como comandos.
```


## 15) Todos los archivos en su directorio de trabajo cuyo nombre NO comience por las letras a ni b (indique la máscara de exclusión utilizada).

### Sin la opción -d
```Python
ls [!ab]*

Result: passwd

Note:
La máscara [!ab]* selecciona nombres cuyo primer carácter no sea "a" ni "b":
- [!ab] → cualquier carácter excepto "a" o "b".
- * → cualquier cantidad de caracteres después.
- En este caso la coincidencia real es el directorio seguro. Como ls recibe un directorio, por defecto muestra su contenido; por eso aparece passwd en lugar de seguro.
```

### Con la opción -d
```Python
ls -d [!ab]*

Result:
seguro

Note: La opción -d hace que ls muestre el nombre del directorio que coincide con el patrón, en lugar de mostrar su contenido. Por eso ahora aparece seguro, que es la coincidencia real de [!ab]*.
```
