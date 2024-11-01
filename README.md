# Install-Pi-hole

Este proyecto te guiará para instalar Pi-hole utilizando Docker Compose. Pi-hole es un bloqueador de anuncios que funciona como un servidor DNS.

## Pasos para la Instalación

### 1. Crear un directorio para el archivo de Docker Compose

Primero, crea un directorio donde quieras guardar el archivo de configuración y entra en él:

```mkdir pihole && cd pihole```


### 2. Crear el archivo `docker-compose.yml`

Usa un editor de texto para crear un archivo llamado `docker-compose.yml` dentro del directorio. Puedes usar `nano`:

```nano docker-compose.yml```


Luego, pega el siguiente contenido en el archivo:

```
version: "3"

services: pihole: image: pihole/pihole
container_name: pihole environment: TZ: "America/Argentina/Buenos_Aires" # Ajusta la zona horaria WEBPASSWORD: "tu_contraseña" # Establece una contraseña para el panel volumes: - "./etc-pihole/:/etc/pihole/" - "./etc-dnsmasq.d/:/etc/dnsmasq.d/" dns: - 127.0.0.1 - 1.1.1.1 ports: - "53:53/tcp" - "53:53/udp" - "80:80" restart: unless-stopped

```

Asegúrate de ajustar `TZ` a tu zona horaria y reemplaza `"tu_contraseña"` con una contraseña segura para acceder al panel web de Pi-hole.

### 3. Crear los directorios de configuración

Ejecuta estos comandos para crear los directorios de volúmenes:

```
mkdir ./etc-pihole ./etc-dnsmasq.d
```



### 4. Iniciar el contenedor

Ahora puedes lanzar Pi-hole con Docker Compose:

```
docker-compose up -d
```


### 5. Ingresar al panel de administración

Accede al panel de administración a través de la siguiente URL:

```
http://192.168.0.100:8080/admin/login.php
```


## Conclusión

¡Ahora tienes Pi-hole corriendo en tu entorno Docker! Disfruta de una navegación más limpia sin anuncios.
