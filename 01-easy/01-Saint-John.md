## Descripción del problema

**Nivel:** Easy  
**Tipo:** Fix  
**Acceso Root:** true  
**Tiempo estimado:** 10 minutos  
**Archivo afectado:** `/var/log/bad.log`

> ⚠️ Un programa de testing está escribiendo continuamente en `/var/log/bad.log`, llenando el disco.  
> El objetivo es **encontrar el proceso responsable y terminarlo**, sin borrar el archivo de log.

### Opción 1: `lsof` (List Open Files)

> `lsof` es una herramienta que muestra información sobre archivos abiertos y los procesos que los utilizan.

1. Ejecuta el siguiente comando para encontrar el proceso que está escribiendo en el archivo de log:
   ```bash
   lsof /var/log/bad.log
   ```
2. Busca el PID (ID de proceso) en la salida del comando.
3. Termina el proceso utilizando el siguiente comando, reemplazando `<PID>` con el ID de proceso encontrado:
   ```bash
   kill <PID>
   ```

### Opción 2: `fuser`

> `fuser` es una herramienta que identifica procesos que están utilizando un archivo o socket.

1. Ejecuta el siguiente comando para encontrar el proceso que está utilizando el archivo de log:
   ```bash
   fuser /var/log/bad.log
   ```
2. Ejecuta el siguiente comando para encontrar y terminar el proceso que está utilizando el archivo de log:
   ```bash
   fuser -k /var/log/bad.log
   ```

### Opción 3: `ps` y `grep`

> `ps` muestra información sobre los procesos en ejecución, y `grep` se utiliza para filtrar la salida.

> La diferencia entre ps y ps aux es que `ps aux` muestra todos los procesos del sistema, mientras que `ps` sin opciones muestra solo los procesos del usuario actual.

1. Ejecuta el siguiente comando para encontrar el proceso que está escribiendo en el archivo de log:

   ```bash
   ps aux | grep bad.log
   ```

2. Busca el PID (ID de proceso) en la salida del comando.
3. Termina el proceso utilizando el siguiente comando, reemplazando `<PID>` con el ID de proceso encontrado:
   ```bash
   kill <PID>
   ```  

### Opción 4: `pgrep`

> `pgrep` es una herramienta que busca procesos en ejecución basándose en criterios específicos.

1. Ejecuta el siguiente comando para encontrar el proceso que está escribiendo en el archivo de log:
   ```bash
   pgrep -f bad.log
   ```

2. Termina el proceso utilizando el siguiente comando, reemplazando `<PID>` con el ID de proceso encontrado:
   ```bash
   kill <PID>
   ```

### Diferencias entre kills

> Existen diferentes señales que se pueden enviar a un proceso para terminarlo. Las más comunes son:

- `SIGTERM` (15): Termina el proceso de manera ordenada, permitiendo que realice limpieza.
- `SIGKILL` (9): Termina el proceso de manera inmediata.
- `SIGINT` (2): Interrumpe el proceso, similar a presionar Ctrl+C en la terminal.
- `SIGHUP` (1): Indica que la terminal ha cerrado, a menudo utilizado para reiniciar procesos.
- `SIGSTOP` (19): Detiene el proceso, pero no lo termina.
- `SIGCONT` (18): Reanuda un proceso detenido.