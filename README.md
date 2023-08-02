## Nodo y API BFA para Docker

### Docker
Para poder levantar los contenedores es necesario contar con [Docker instalado](https://docs.docker.com/engine/install/).

### Descripción
El presente repositorio levanta dos contenedores Docker:
- [nodo transaccional](https://gitlab.bfa.ar/blockchain/nucleo) (producción)
- [api (tsa2)](https://gitlab.bfa.ar/blockchain/tsa2)

El nodo crea una cuenta y esa cuenta es la que levanta la API.

### Implementación
Para poder levantar todo con docker-compose primero es necesario crear las imágenes:

**NODO**
````
docker build -t nodobfa nodo/
````

**API**
````
docker build -t apibfa api/
````

**Por último:**
````
docker-compose up -d
````

### Importante
Al levantar los contenedores el nodo empezará a sincronizar. La API quedará expuesta en el puerto 3000.

**Comandos útiles:**
````
docker exec nodobfa bfalog.sh
docker exec nodobfa localstate.pl
````
O cualquier otro comando documentado del [nodo](https://gitlab.bfa.ar/blockchain/nucleo)
