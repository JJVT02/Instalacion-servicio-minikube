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

Paso 2: Crear el Pod
```bash
kubectl apply -f archivo_pod.yaml
```
Paso 3: Comprobar que el Pod está creado y corriendo
```bash
kubectl get pods
```
Paso 4: Obtener información detallada del Pod
```bash
kubectl describe pod mi-primer-pod
```

Paso 5: Acceder de forma interactiva al Pod y verificar archivos
```bash
kubectl exec -it mi-primer-pod -- /bin/bash
ls /usr/local/apache2/htdocs/
exit
```

Paso 6: Crear una redirección con kubectl port-forward
```bash
kubectl port-forward mi-primer-pod 8888:80
```
Paso 7: Mostrar los logs del Pod
```bash
kubectl logs mi-primer-pod
```
Paso 8: Eliminar el Pod (OPCIONAL)
```bash
kubectl delete pod mi-primer-pod
```