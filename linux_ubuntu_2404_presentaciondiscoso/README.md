## Contexto

Montado de nuevo volumen de disco en un servidor 24.04.2 una vez presentado el nuevo disco desde el hipervisor en turno
Asumiendo que el disco nuevo es /dev/sdb (verifica con lsblk), los pasos son los siguientes:

## 1. Identificar el nuevo disco
Primero, asegúrate de cuál es el identificador del disco nuevo:
```
lsblk
```
