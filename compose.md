# Docker-compose
## Paso 1
Hacemos este archivo de docker compose para nuestros servicios
[docker-compose](/Archivosyaml/docker-compose.yml)

## Paso 2


###### Obtener la versión de docker-compose.

> docker-compose --version

### Crear los contenedores (servicios) que están descritos en el docker-compose.yml.

> docker-compose up

### Crear en modo detach los contenedores (servicios) que están descritos en el docker-compose.yml. Eso significa que no muestran mensajes de log en el terminal y que se  nos vuelve a mostrar un prompt.

> docker-compose up -d

### Detiene los contenedores que previamente se han lanzado con docker-compose up.

> docker-compose stop

### Inicia los contenedores descritos en el docker-compose.yml que estén parados.

> docker-compose run

### Pausa los contenedores que previamente se han lanzado con docker-compose up.

> docker-compose pause

### Reanuda los contenedores que previamente se han pausado.

> docker-compose unpause

### Reinicia los contenedores. Orden ideal para reiniciar servicios con nuevas configuraciones.

> docker-compose restart

### Para los contenedores, los borra  y también borra las redes que se han creado con docker-compose up (en caso de haberse creado).

> docker-compose down

### Para los contenedores y borra contenedores, redes y volúmenes

> docker-compose down -v

### Muestra los logs del servicio llamado servicio1 que estaba descrito en el docker-compose.yml.

> docker-compose logs servicio1

### Ejecuta una orden, en este caso /bin/bash en un contenedor llamado servicio1 que estaba descrito en el docker-compose.yml

> docker-compose exec servicio1 /bin/bash
