# Deployments
## Actividad 1

## Paso 1: Crear el archivo YAML con la descripción del recurso Deployment

1. Abre tu editor de texto preferido.

2. Crea un nuevo archivo y nómbralo, por ejemplo, deployment.yaml.

3. Copia y pega el siguiente contenido en el archivo:

```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-web-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-web-app
  template:
    metadata:
      labels:
        app: my-web-app
    spec:
      containers:
        - name: my-web-container
          image: iesgn/test_web:latest
          ports:
            - containerPort: 80
```

## Paso 2: Crear el Deployment
```bash
kubectl apply -f deployment.yaml
```

## Paso 3: Verificar los recursos creados
```bash
kubectl get deployment
kubectl get replicaset
kubectl get pods
```
## Paso 4: Obtener información detallada del Deployment
```bash
kubectl describe deployment my-web-deployment
```

## Paso 5: Configurar port-forwarding y acceder a la aplicación

```bash
kubectl port-forward deployment/my-web-deployment 8080:80
```

**Abre un navegador web y accede a http://localhost:8080 para ver la aplicación desplegada.**


## Paso 6: Acceder a los logs del despliegue
```bash
kubectl logs <nombre_del_pod>
```

**Sustituye <nombre_del_pod> por el nombre del pod que se muestra al ejecutar kubectl get pods.**

## Paso 7: Eliminar el Deployment
```bash
kubectl delete deployment my-web-deployment
```

Verifica que se hayan eliminado todos los recursos ejecutando nuevamente los comandos:

**kubectl get deployment** 

**kubectl get replicaset** 
 
**kubectl get pods**.


# Actividad 2

## Paso 1:Ejecuta el siguiente comando para crear el Deployment en Kubernetes:

```bash
kubectl apply -f deployment.yaml
```
Esto creará el Deployment con el nombre my-web-deployment.

## Verifica que el Deployment se haya creado correctamente ejecutando:
```bash
kubectl get deployments
```
Deberías ver el my-web-deployment en la lista.

## Verifica que los pods se hayan creado correctamente ejecutando:
```bash
kubectl get pods
```
Deberías ver los pods creados por el Deployment.

Si necesitas exponer la aplicación fuera del clúster de Kubernetes, puedes crear un servicio para ello. Por ejemplo, para exponer la aplicación a través de un servicio de tipo NodePort, puedes ejecutar:
```bash
kubectl expose deployment my-web-deployment --type=NodePort --port=80
```

Esto creará un servicio que asignará un puerto aleatorio en cada nodo del clúster de Kubernetes al puerto 80 del Deployment.

## Verifica que el servicio se haya creado correctamente ejecutando:
```bash
kubectl get services
```
Deberías ver el servicio recién creado y el puerto asignado.

Si estás utilizando un entorno local de Kubernetes como Minikube o Docker Desktop, puedes obtener la URL para acceder a la aplicación ejecutando:
```bash
minikube service my-web-deployment --url
```
Esto te proporcionará la URL a la que puedes acceder en tu navegador para ver la aplicación.

![](/img/act2.png)

## Actividad 3

## Paso 1: Crear los despliegues

```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: guestbook-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: guestbook
  template:
    metadata:
      labels:
        app: guestbook
    spec:
      containers:
        - name: guestbook-container
          image: iesgn/guestbook
          ports:
            - containerPort: 5000
```

```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-deployment
spec:
  replicas: 1  # Puedes ajustar el número de réplicas según tus necesidades
  selector:
    matchLabels:
      app: redis
  template:
    metadata:
      labels:
        app: redis
    spec:
      containers:
        - name: redis-container
          image: redis
          ports:
            - containerPort: 6379
```


```bash
kubectl apply -f guestbook-deployment.yaml
kubectl apply -f redis-deployment.yaml
```


## Paso 2 Comprobar los recursos creados:
```bash
kubectl get deployments
kubectl get replicasets
kubectl get pods
```

## Paso 3 Crear una redirección utilizando el port-forward:

Utiliza el port-forwarding para acceder a la aplicación GuestBook a través del puerto 5000. Ejecuta el siguiente comando:

```bash
kubectl port-forward deployment/guestbook-deployment 5000:5000
```

go, intenta acceder a la aplicación GuestBook desde tu navegador web utilizando la dirección http://localhost:500

![](/img/act3.png)