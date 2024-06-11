#### Análisis de datos proyecto sistema de ventas

### Levantar la base de datos

1) Crear el directorio de la base de datos 

```
bryanalonso@MacBook-Pro-de-bryan proyecto % mkdir storage_mysql
bryanalonso@MacBook-Pro-de-bryan proyecto % ls -l
total 408
-rw-r--r--  1 bryanalonso  staff      52 Jun  9 10:45 Readme.md
drwxr-xr-x  5 bryanalonso  staff     160 May 20 21:35 deploy_mysql
-rw-r--r--  1 bryanalonso  staff  203667 Jun  9 10:42 proyecto_sistema_ventas.ipynb
drwxr-xr-x  2 bryanalonso  staff      64 Jun  9 10:48 storage_mysql
bryanalonso@MacBook-Pro-de-bryan proyecto % pwd
/Users/bryanalonso/datapath/analisis-datos-python/proyecto
```

2) Modificar el deploy_mysql/mysql-storage.yaml, setear el path de la base de datos

```
bryanalonso@MacBook-Pro-de-bryan proyecto % kubectl apply -f deploy_mysql/mysql-storage.yaml
persistentvolume/mysql-pv-volume created
persistentvolumeclaim/mysql-pv-claim created
bryanalonso@MacBook-Pro-de-bryan proyecto % kubectl get pv
NAME              CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                    STORAGECLASS        REASON   AGE
mysql-pv-volume   20Gi       RWO            Retain           Bound    default/mysql-pv-claim   mysqlstorageclass            7s
bryanalonso@MacBook-Pro-de-bryan proyecto % kubectl get pvc
NAME             STATUS   VOLUME            CAPACITY   ACCESS MODES   STORAGECLASS        AGE
mysql-pv-claim   Bound    mysql-pv-volume   20Gi       RWO            mysqlstorageclass   10s
bryanalonso@MacBook-Pro-de-bryan proyecto %
```

3) Modificar el password de la base de datos en caso se requiera del archivo 
 deploy_mysql/mysql-secret.yaml

```
bryanalonso@MacBook-Pro-de-bryan proyecto % kubectl apply -f deploy_mysql/mysql-secret.yaml
secret/mysql-secret created
```

4) Ejecutar el deployment
```
bryanalonso@MacBook-Pro-de-bryan proyecto % kubectl apply -f deploy_mysql/mysql-deployment.yaml
deployment.apps/mysql created
service/mysql created
```
