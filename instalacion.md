# Instalación 
Veamos cómo se instala en Ubuntu 20.04

## Para empezar deberemos actualizar el sistema:

```bash
sudo apt-get update -y
sudo apt-get upgrade -y
```


## Después deberemos instalar algunas dependencias de descarga de datos:

```bash
sudo apt-get install apt-transport-https wget curl
sudo apt install virtualbox virtualbox-ext-pack
```

*Nota: en la instalación dale a Aceptar y  acepta la licencia*

## A continuación descarga minikube, dale permisos e instálalo para que tengas acceso desde cualquier sitio:

```bash
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
chmod +x minikube-linux-amd64
sudo mv minikube-linux-amd64 /usr/local/bin/minikube
```

## Comprueba que está bien instalado ejecutando:

```bash
minikube version
```
## Instala kubectl, dale permisos y colócalo en el path:


```bash
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```

## Comprueba que va todo correcto

```bash
kubectl version -o json
```

## Arranqua minikube

```bash
minikube start
```

## si ves que falla por un tema de red:

```bash
docker swarm leave --force
docker network prune
```
## Si falla por un tema de permisos:
```bash
sudo usermod -aG docker $USER && newgrp docker
```
## Si falla por un tema de la máquina Virtual (VM):

Comprueba que tienes activadas en la BIOS las extensiones de virtualización
Comprueba que tienes acceso:
```bash
kubectl cluster-info
kubectl config view
```
# comandos principales de minikube

minikube ssh -> acceso a la máquina virtual

minikube stop-> parada del servidor

minicube delete -> borrado de la máquina virtual
Minikube dispone de addons:
```bash
minikube addons list
```
Por ejemplo del dashboard o url de acceso a la gestión:
```bash
minikube dashboard --url
```
