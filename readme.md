
install postgres database
```shell
helm install database -f postgres/values.yaml oci://registry-1.docker.io/bitnamicharts/postgresql  --create-namespace -n development
```
forward to local port 5432
```shell
kubectl port-forward --namespace development svc/database-postgresql 5432:5432
```
uninstall postgres database
```shell
helm delete database -n development
```

Delete PVC's associated with database
```shell
kubectl delete pvc data-database-postgresql-0  -n development
```
create database, user and  password for application need install job
```shell
helm install user-db ./user-db -n development
```

deploy user-service
```shell
helm install user-service ./user-service -n development
```

run postman collections
```shell
newman run otus-2.postman_collection.json
```

uninstall user-service
```shell
helm uninstall user-service -n development
```

delete job
```shell
helm uninstall user-db -n development
```

