### Comprobación del formato del log

Antes de ejecutar ningún comando he visualizado las últimas líneas del fichero para comprobar el formato del log:

```bash
tail -n 5 access.log
```

### Contar cuántas peticiones realiza cada IP

```bash
awk '{print $1}' access.log | sort | uniq -c | sort -nr | head -1
```

| Parte del comando | Descripción |
|-------------------|-------------|
| `awk '{print $1}' access.log` | Extrae la primera columna del log (correspondiente a la IP). |
| `sort` | Ordena alfabéticamente las IPs para agrupar iguales. |
| `uniq -c` | Cuenta cuántas veces aparece cada IP consecutiva. |
| `sort -nr` | Ordena los resultados de forma numérica y de mayor a menor para ver las IP con más peticiones primero. |
| `head -1` | Ordena los resultados de forma numérica y de mayor a menor para ver las IP con más peticiones primero. |

### Escribir en el archivo highestip.txt el resultado

```bash
echo (IP) > highestip.txt
```
