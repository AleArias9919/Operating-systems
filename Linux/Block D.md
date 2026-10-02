## Bloque D: Atributos, Permisos y Enlaces.

### 16) Ejecute un comando de listado largo sobre el archivo /etc/passwd. Interprete detalladamente cada uno de los campos que devuelve el sistema de izquierda a derecha.

```

```

### 17) Cree un archivo llamado privado.txt en su directorio Laboratorio01. Utilice chmod en modo relativo (letras) para quitar todos los permisos de lectura y escritura para el grupo y otros, dejando el control total al propietario. Compruebe los permisos resultantes con ls -l .

```

```

### 18) Modifique los permisos del archivo privado.txt utilizando chmod en modo absoluto (octal) de tal forma que el propietario tenga permisos de lectura y escritura (rw-), el grupo tenga únicamente lectura (r--), y otros no tengan ningún permiso (---). Escriba el comando correspondiente y la representación octal utilizada.

```

```

### 19) Cree un directorio llamado compartido dentro de Laboratorio01. Asígnele permisos rwxr-x--- utilizando tanto el modo octal como el modo simbólico . Explique por qué el permiso de ejecución (x) es obligatorio en un directorio para que un miembro del grupo pueda ingresar a él.

```

```

### 20) Verifique el valor de su máscara de usuario actual ejecutando umask sin parámetros . ¿Cuál es su valor octal? Cambie la máscara temporalmente a 077 (limpiar todos los permisos para grupo y otros) . Cree un directorio llamado super_seguro and un archivo llamado secreto.txt dentro de él. Verifique con qué permisos fueron creados ambos elementos. ¿Cómo influye la máscara en este proceso?

```

```

### 21) Restablezca su máscara a su valor original. Con los permisos de compartido en rwxr-x---, intente quitar el permiso de ejecución (x) para el propietario . Intente ingresar al directorio con cd compartido. ¿Qué mensaje obtiene? Restablezca el permiso de ejecución, luego quite el permiso de lectura (r) al propietario e intente listar el contenido del directorio (ls compartido). ¿Qué sucede? Explique detalladamente la diferencia de comportamiento .

```

```

### 22) En su directorio Laboratorio01, cree un enlace físico llamado enlace_duro que apunte al archivo identidad.txt que creó en el paso 6 [19, 118].

```

```

### 23) En el mismo directorio, cree un enlace simbólico llamado enlace_blando apuntando al mismo archivo identidad.txt [19, 118].

```

```

### 24) Ejecute ls -l y compare ambos enlaces creados junto con el archivo original:
#### -Compare los números de inodo de los tres archivos (use ls-i para visualizarlos directamente). ¿Qué observa? [19,118]
#### -Compare los tamaños de los archivos mostrados en bytes. ¿Por qué el enlace simbólico tiene un tamaño tan reducido en comparación al archivo original? [19, 118]

```

```

### 25) Elimine o renombre el archivo original identidad.txt. ¿Qué sucede al intentar leer el contenido del enlace físico? ¿Y al intentar leer el enlace simbólico? Explique detalladamente el comportamiento técnico de ambos.

```

```
