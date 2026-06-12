## Contexto

Montado de nuevo volumen de disco en un servidor 24.04.2 una vez presentado el nuevo disco desde el hipervisor en turno, el cual alojara los archivos de base de datos de MySQL
Asumiendo que el disco nuevo es /dev/sdb (verifica con lsblk), los pasos son los siguientes:

## 1. Identificar el nuevo disco
Primero, asegúrate de cuál es el identificador del disco nuevo:
```
lsblk
```
Verás un disco que no tiene particiones (probablemente sdb) y cuyo tamaño coincide con el que agregaste.
## 2. Formatear el disco
Vamos a crear un sistema de archivos directo en el disco. Usaremos ext4, que es el estándar de Ubuntu:
```
sudo mkfs.ext4 /dev/sdb
```
Si prefieres XFS por rendimiento en bases de datos grandes:
```
sudo mkfs.xfs /dev/sdb
```
## 3. Crear el punto de montaje y asignar ruta
Primero creamos la carpeta donde quieres que viva la data (de un MySQL en este contexto):
```
sudo mkdir -p /home/mysql
```
## 4. Montaje persistente (Configurar /etc/fstab)
Si lo montas a mano, al reiniciar el servidor desaparecerá. Para que sea permanente, necesitamos el UUID del disco:
1. Obtén el UUID:
```
sudo blkid /dev/sdb
```
2. Edita el archivo de montajes:
```
sudo nano /etc/fstab
```
3. Agrega esta línea al final del archivo:
```
UUID=tu-codigo-uuid-aqui  /home/mysql  xfs  defaults  0  2
```
4. Prueba el montaje sin reiniciar:
```
sudo mount -a
```
Si no da error, ejecuta df -h /home/mysql para confirmar que ya tienes los GB disponibles ahí.









