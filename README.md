
# Servidor Docker con SSH y FTP

Este repositorio contiene la configuración necesaria para crear y ejecutar un servidor Docker con SSH y FTP.

## **Requisitos previos**

- Docker instalado en tu sistema.
- Acceso a la línea de comandos.

## **Pasos para clonar, construir y arrancar el servidor**

### 1. Clonar el repositorio
Clona este repositorio en tu máquina local:
```bash
git clone <URL_DEL_REPOSITORIO>
cd <NOMBRE_DEL_REPOSITORIO>
```

### 2. Construir la imagen Docker
Ejecuta el siguiente comando para construir la imagen del servidor:
```bash
docker build -t ssh-ftp-server .
```

Esto creará una imagen llamada `ssh-ftp-server` a partir del `Dockerfile`.

### 3. Ejecutar el contenedor
Arranca un contenedor basado en la imagen recién creada, mapeando los puertos necesarios:
```bash
docker run -d -p 22:22 -p 21:21 --name ssh-ftp-container ssh-ftp-server
```

### 4. Verificar que el contenedor está en ejecución
Asegúrate de que el contenedor se esté ejecutando:
```bash
docker ps
```

Deberías ver una línea similar a esta:
```
CONTAINER ID   IMAGE            COMMAND                  ...  PORTS
xxxxxxxxxxxx   ssh-ftp-server   "/bin/sh -c 'service…"   ...  0.0.0.0:22->22/tcp, 0.0.0.0:21->21/tcp
```

## **Probar el servidor**

### Probar el servidor SSH
1. Usa un cliente SSH (como la terminal en macOS):
   ```bash
   ssh root@localhost
   ```
2. Ingresa la contraseña: `password123`.

Si la conexión es exitosa, verás una terminal dentro del contenedor.

---

### Probar el servidor FTP
1. Usa un cliente FTP, como `FileZilla` o la línea de comandos:
   - **Host:** `localhost`
   - **Usuario:** `ftpuser`
   - **Contraseña:** `ftp123`
2. Conéctate al servidor y verifica que puedes navegar por el sistema de archivos.

---

## **Detener y eliminar el servidor**

### Detener el contenedor
Si necesitas detener el servidor, ejecuta:
```bash
docker stop ssh-ftp-container
```

### Eliminar el contenedor
Si deseas eliminar el contenedor, ejecuta:
```bash
docker rm ssh-ftp-container
```

### Eliminar la imagen Docker
Para eliminar la imagen del servidor, ejecuta:
```bash
docker rmi ssh-ftp-server
```

---

## **Notas adicionales**

- Asegúrate de cambiar las contraseñas por valores seguros si vas a usar este servidor en entornos de producción.
- Si necesitas modificar alguna configuración, edita el archivo `Dockerfile` antes de construir la imagen.

¡Disfruta del servidor SSH y FTP en Docker!
