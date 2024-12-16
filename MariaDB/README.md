
# MariaDB Docker Setup

Este repositorio contiene la configuración para ejecutar un contenedor Docker con MariaDB. Está diseñado para facilitar el desarrollo y pruebas con una base de datos MariaDB utilizando `docker-compose`.

## Requisitos previos
- Docker instalado en tu sistema. [Descargar Docker](https://www.docker.com/products/docker-desktop/)
- Docker Compose instalado. [Instalar Docker Compose](https://docs.docker.com/compose/install/)

## Configuración del contenedor

El archivo `docker-compose.yml` configura un contenedor MariaDB con las siguientes credenciales por defecto:

- **Usuario de la base de datos:** `mariadbuser`
- **Contraseña del usuario:** `mariadbpass`
- **Base de datos:** `demo_db`
- **Contraseña de root:** `rootpassword`
- **Puerto:** `3306`

Puedes personalizar estas variables editando el archivo `docker-compose.yml`.

## Cómo usar

### 1. Clonar el repositorio
Clona este repositorio en tu máquina local:
```bash
git clone <URL del repositorio>
cd <nombre del repositorio>
```

### 2. Iniciar el contenedor
Ejecuta el siguiente comando para levantar el contenedor:
```bash
docker-compose up -d
```

Esto descargará la imagen de MariaDB si no la tienes y levantará el contenedor en segundo plano.

### 3. Verificar el contenedor
Confirma que el contenedor está corriendo:
```bash
docker ps
```

Deberías ver un contenedor con el nombre `mariadb-container`.

### 4. Acceso a la base de datos
Puedes acceder a MariaDB de las siguientes maneras:

#### Desde el cliente MySQL
```bash
mysql -h 127.0.0.1 -P 3306 -u mariadbuser -p
```
Introduce la contraseña `mariadbpass` cuando se te solicite.

#### Desde una herramienta gráfica (DBeaver, PhpMyAdmin, etc.)
- **Host:** `localhost`
- **Port:** `3306`
- **Username:** `mariadbuser`
- **Password:** `mariadbpass`

## Detener el contenedor
Para detener el contenedor, ejecuta:
```bash
docker-compose down
```

Esto detendrá y eliminará el contenedor, pero los datos permanecerán en el volumen `mariadb_data`.

## Reiniciar con un entorno limpio
Si deseas eliminar completamente los datos almacenados:
```bash
docker-compose down -v
```

Esto elimina tanto el contenedor como los volúmenes asociados.

## Personalización

Puedes modificar los valores predeterminados de MariaDB editando el archivo `docker-compose.yml`. Las variables relevantes son:

```yaml
environment:
  MYSQL_ROOT_PASSWORD: rootpassword  # Contraseña del usuario root
  MYSQL_DATABASE: demo_db           # Nombre de la base de datos
  MYSQL_USER: mariadbuser           # Usuario de la base de datos
  MYSQL_PASSWORD: mariadbpass       # Contraseña del usuario
```

## Problemas comunes

### Error: "Can't connect to MySQL server"
- Verifica que el contenedor está corriendo con `docker ps`.
- Asegúrate de que estás usando las credenciales correctas.
- Comprueba si otro servicio está ocupando el puerto `3306` y, de ser necesario, cámbialo en `docker-compose.yml`:
  ```yaml
  ports:
    - "3307:3306"
  ```

### El volumen de datos persiste tras reiniciar el contenedor
- Los datos se almacenan en el volumen `mariadb_data`. Para eliminarlo, usa:
  ```bash
  docker volume rm mariadb_data
  ```

## Recursos adicionales

- [Documentación oficial de MariaDB](https://mariadb.com/kb/en/)
- [Documentación de Docker](https://docs.docker.com/)
- [Docker Hub - MariaDB](https://hub.docker.com/_/mariadb)


