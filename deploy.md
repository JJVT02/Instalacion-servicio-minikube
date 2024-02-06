# Deployments
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