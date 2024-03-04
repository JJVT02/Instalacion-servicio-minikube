# Dockerfile

## Construcción de una imagen sin nombre ni versión estando el Dockerfile en el mismo directorio donde se ejecuta docker build:


```bash
docker build .
```
## Construcción de una imagen especificando nombre y versión estando el Dockerfile en el mismo directorio donde se ejecuta docker build (--tag/-t):

```bash
docker build -t usuario/nombre_imagen:1.0 .
```
## Construcción de una imagen especificando un repositorio en GitHub donde se encuentra el Dockerfile. Ese repositorio es el contexto de construcción:

```bash
docker build -t usuarioDockerHub/nombre_imagen:1.1 https://github.com/usuario/repo.git#rama_git
```
## Construcción de una imagen usando una variable de entorno estando el Dockerfile en el mismo directorio donde se ejecuta docker build (--build-arg):

```bash
docker build --build-arg user=usuario -t usuarioDockerHub/nombre_imagen:1.0 .
```
## Construcción de una imagen sin usar las capas cacheadas por haber realizado anteriormente imágenes con capas similares y estando el Dockerfile en el mismo directorio donde se ejecuta docker build (--no-cache):

```bash
docker build --no-cache -t usuarioDockerHub/nombre_imagen:1.0 .
```
## Construcción de una imagen especificando nombre, versión y especificando la ruta al fichero Dockerfile mediante el flag --file/-f:

```bash
docker build -t usuario/nombre_imagen:1.0 -f /home/usuario/DockerProject/Dockerfile
```