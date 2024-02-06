## PODS

# Paso 1: Crear el archivo YAML con la descripción del Pod

```bash
# archivo_pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: mi-primer-pod
  labels:
    app: servidor-web
spec:
  containers:
  - name: contenedor-web
    image: iesgn/test_web:latest
```
![](/img/archivo.png)

Paso 2: Crear el Pod
```bash
kubectl apply -f archivo_pod.yaml
```
![](/img/1.png)

Paso 3: Comprobar que el Pod está creado y corriendo
```bash
kubectl get pods
```
![](/img/getpod.png)

Paso 4: Obtener información detallada del Pod

```bash
kubectl describe pod mi-primer-pod
```
![](/img/describe.png)

Paso 5: Acceder de forma interactiva al Pod y verificar archivos

```bash
kubectl exec -it mi-primer-pod -- /bin/bash
ls /usr/local/apache2/htdocs/
exit
```
![](/img/exec.png)

Paso 6: Crear una redirección con kubectl port-forward
```bash
kubectl port-forward mi-primer-pod 8888:80
```
![](/img/80.png)

Paso 7: Mostrar los logs del Pod

```bash
kubectl logs mi-primer-pod
```

![](/img/logs.png)

Paso 8: Eliminar el Pod (OPCIONAL)

```bash
kubectl delete pod mi-primer-pod
```
![](/img/delete.png)