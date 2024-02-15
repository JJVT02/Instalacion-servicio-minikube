# NextCloud
## Despliegue y acceso a Nextcloud + MariaDB
### Tenemos que crear los archivos de configMap

```yaml
kubectl create cm bd-datos --from-literal=bd_user=user_nextcloud \
                           --from-literal=bd_dbname=nextcloud \
                           -o yaml --dry-run=client > bd_datos_configmap.yaml

kubectl create secret generic bd-passwords --from-literal=bd_password=password1234 \
                                           --from-literal=bd_rootpassword=root1234 \
                                           -o yaml --dry-run=client > bd_passwords_secret.yaml
```
*lo aplicamos con el siguiente comando*

```bash
kubectl apply -f bd_datos_configmap.yaml
kubectl apply -f bd_passwords_secret.yaml
```


## Despliegue de la base de datos

*Usa este fichero* [`mariadb-deployment.yaml`](/Archivosyaml/mariadb-deployment.yaml)

```bash
kubectl apply -f mariadb-deployment.yaml
```



*Luego despliega el servicio*La definición del Service que vamos a crear lo tenemos en el fichero: [`mariadb-srv.yaml`](/Archivosyaml/mariadb-srv.yaml)


```bash
kubectl apply -f mariadb-srv.yaml
```


## Despliega la aplicacion

Para desplegar la aplicación Wordpress vamos a usar el fichero [`nextcloud-deployment.yaml`](/Archivosyaml/nextcloud-deployment.yaml)

```bash
kubectl apply -f nextcloud-deployment.yaml
```


La definición del Service que vamos a crear la tenemos en el fichero: [`nextcloud-srv.yaml`](/Archivosyaml/nextcloud-srv.yaml)

```bash
kubectl apply -f nextcloud-srv.yaml
```

## Acceso a la aplicacion

Para acceder a la aplicación vamos a crear un recurso Ingress que tenemos definido en el fichero: [`nextcloud-ingress.yaml`](/Archivosyaml/nextcloud-ingress.yaml)

```bash
kubectl apply -f nextcloud-ingress.yaml
```

