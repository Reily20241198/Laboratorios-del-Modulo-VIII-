# Laboratorios-del-Modulo-VIII-
Practica #3: IDespliegue de contenedor de Wordpress utilizando Docker-Compose
=======================================================
   PRÁCTICA #3: WORDPRESS USANDO DOCKER COMPOSE (2pts)
=======================================================

1️⃣ INSTALAR DOCKER-COMPOSE
----------------------------
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
# Descarga el binario de docker-compose correspondiente al sistema.

sudo chmod +x /usr/local/bin/docker-compose
# Da permisos de ejecución al archivo.

docker-compose --version
# Verifica que docker-compose se haya instalado correctamente.


2️⃣ CREAR ARCHIVO docker-compose.yml
-------------------------------------
Contenido del archivo:

version: '3.1'

services:
  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppassword
      MYSQL_ROOT_PASSWORD: rootpassword
    volumes:
      - db_data:/var/lib/mysql

  wordpress:
    image: wordpress:latest
    ports:
      - "8080:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppassword
      WORDPRESS_DB_NAME: wordpress
    depends_on:
      - db

volumes:
  db_data:

# Este archivo define dos servicios:
# - db (MySQL) con sus variables de entorno.
# - wordpress (la aplicación principal).
# Usa volúmenes para persistencia y mapea el puerto 8080 al navegador.


3️⃣ DESPLEGAR WORDPRESS
------------------------
sudo docker-compose up -d
# Inicia todos los servicios definidos en el docker-compose.yml en segundo plano.


4️⃣ CONFIGURAR WORDPRESS EN NAVEGADOR
--------------------------------------
Accede a: http://127.0.0.1:8080

- Elige idioma
- Asigna nombre al sitio (puede dejarse vacío, pero se recomienda completarlo)
- Crear usuario administrador y contraseña
- Finalizar instalación

✅ WordPress estará listo para su uso y completamente funcional.
