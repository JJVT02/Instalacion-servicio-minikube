# ReplicaSet

## Crear un fichero yaml con la descripción del ReplicaSet:

```bash
yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: test-web
  template:
    metadata:
      labels:
        app: test-web
    spec:
      containers:
      - name: web-container
        image: iesgn/test_web:latest
```

## Crear el ReplicaSet:

Guardar el código anterior en un archivo llamado, por ejemplo, replicaset.yaml, luego ejecuta el siguiente comando en tu terminal para 
crear el ReplicaSet:

```bash
kubectl apply -f replicaset.yaml
```

## Comprobar que se ha creado el ReplicaSet y los 3 Pods:

```bash
kubectl get replicaset,pods
```
## Obtener información detallada del ReplicaSet creado:

```bash
kubectl describe replicaset my-replicaset
```
## Probar la tolerancia a fallos: Eliminar uno de los 3 Pods:

```bash
kubectl delete pod <nombre-del-pod>
```
## Comprobar que se ha creado un nuevo Pod:

```bash
kubectl get pods
```
## Comprobar la escalabilidad: Escalar el ReplicaSet a 6 Pods:

```bash
kubectl scale --replicas=6 replicaset my-replicaset
```
## Eliminar el ReplicaSet y comprobar que se han borrado todos los Pods:

```bash
kubectl delete replicaset my-replicaset
kubectl get pods
```