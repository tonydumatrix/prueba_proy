# Deployment de Pruebas Proyecto Final SOA

## MTIE - 501

## Instrucciones a seguir:

## Nos conectamos al contenedor de mongodb para configurar lo faltante

``` 
docker exec -it MRSI-MongoDB bash
mongo -u root -p
```

## Inicializamos replicaset en mongodb y verificamos status, el cluster se llama rs0 como lo hicimos en docker-compose
```
rs.initiate();
rs.status();
```

## Generamos una nueva BD llamada dbdata y creamos usuario dbo-operator y los roles de dicho usuario
```
use dbdata
    
db.createUser({
  user: 'dbo-operator',
  pwd: 'operadoradmin',
  roles: [
    { role: 'readWrite', db: 'dbdata' },
    { role: 'read', db: 'local' },
    { role: "dbAdmin", db: "dbdata" },
    { role: 'root', db: 'admin' }
  ]
});

db.getUsers();

exit
exit
```

## Abrimos Robo 3T para conectarnos a la base de datos, creamos la BD dbdata e insertamos las colecciones