## Configurando nuestra aplicación Temperaturas

## 1. Crea un recurso ConfigMap

```bash
kubectl create configmap servidor-temperaturas-config --from-literal=SERVIDOR_TEMPERATURAS=servidor-temperaturas:5000
```

## 2. Modifica el fichero de despliegue del frontend:
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: temperaturas-frontend
  labels:
    app: temperaturas
    tier: frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: temperaturas
      tier: frontend
  template:
    metadata:
      labels:
        app: temperaturas
        tier: frontend
    spec:
      containers:
      - name: contenedor-temperaturas
        image: iesgn/temperaturas_frontend
        ports:
          - name: http-server
            containerPort: 3000
```
```bash
kubectl apply -f frontend-deployment.yaml
```
## 3. Realiza el despliegue y crea el Service para acceder al frontend.
```yml
apiVersion: v1
kind: Service
metadata:
  name: temperaturas-frontend
  labels:
    app: temperaturas
    tier: frontend
spec:
  type: NodePort
  ports:
  - port: 3000
    targetPort: http-server
  selector:
    app: temperaturas
    tier: frontend
```

```bash
kubectl apply -f frontend-srv.yaml
```
## 4. Despliega el microservicio backend.

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: temperaturas-backend
  labels:
    app: temperaturas
    tier: backend
spec:
  replicas: 1
  selector:
    matchLabels:
      app: temperaturas
      tier: backend
  template:
    metadata:
      labels:
        app: temperaturas
        tier: backend
    spec:
      containers:
        - name: contendor-servidor-temperaturas
          image: iesgn/temperaturas_backend
          ports:
            - name: api-server
              containerPort: 5000
```
```yml
apiVersion: v1
kind: Service
metadata:
  name: temperaturas-backend
  labels:
    app: temperaturas
    tier: backend
spec:
  type: ClusterIP
  ports:
  - port: 5000
    targetPort: api-server
  selector:
    app: temperaturas
    tier: backend

```

```bash
kubectl apply -f backend-deployment.yaml
kubectl apply -f backend-srv.yaml
```

![temp](/img/temp1.png)

## 5.Acceso a la aplicación usando el Ingress Controller

```yml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: temperaturas
spec:
  rules:
  - host: www.temperaturas.org
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: temperaturas-frontend
            port:
              number: 3000
        
```

A continuación usamos el fichero ingress.yaml para crear el recurso Ingress, que definirá el nombre del host www.temperaturas.org que tendremos que introducir en la resolución estática tay como hemos visto anteriormente. Por lo tanto modificamos el fichero /etc/hosts de nuestro ordenador con la siguiente línea:
```
(tu direccion ip de minikube) www.temperaturas.org
```
```
kubectl apply -f ingress.yaml
```

![](/img/temp2.png)

