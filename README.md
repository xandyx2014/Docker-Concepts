> docker build -t andyjesus2/debian .\proyect_one\
// EJECTURAR Y INTERACTUAR docker
> docker run -it 6f6545164e69
// Descargar ubuntu
> docker pull ubuntu

## Docker images
- Es un templatae para crear un entorno
- Este contiene todos los elementos necesitado para tu app librerias evn, config, iles softwate
- Este puede tener una version o snapshots basado en un tiempo
- ESte es inmutable, pero este puede ser clonado o compartido
- Esas imagees son creados usando Dockerfile
- Es la imagenes se puede decir q son como instaladores que crean disintios procesos llamados contendores
## Docker Container
- It es una instancia de una imagen
- Tu puedes buscar una docker hub container repostire

```Dockerfile
FROM ngix:latest
WORKDIR /usr/share/nginx/html
COPY . .
```

> docker build -t [usernameFromDockerHub]/[nameImage]:[tag] [directory]
// para ejecutar un comando en el contenedor ya se en ejecusion
> docker exec -it [idContenedior] bash
> docker exect -u root -it bash
Esto genera una imagen
> docker-compose build
Este levanta los servicios
>docker-compose up
Linkear los docker que depende de unos
- Docker crea un tunerl seguro entre lso contenedores que no requieren exponer ninugn puerto externamente del conenedor
> docker run -d -p 5000:5000 --link [nombre del contenedor] dockerapp:0.1
Para ver los logs
¿ Como funciona los enlances entre los contenedores?
> docker exec -it [iddocker] bash
> more /etc/hosts
## Comando utiles de docker-compose
> docker-compose up -d
> docker-compose ps
> docker-compose logs [name-container]

# Buenas practicas
- Efimeros 
- Multi linea
- no instalar paquetes innecesarios
- labels

# RUN vs CMD
No confunda RUN con CMD. RUN en realidad ejecuta un comando y confirma el resultado; CMD no ejecuta nada en el momento de la compilación de la imagen, pero especifica el comando previsto para la imagen.

# Dangling images
- <none> <none>
cuando nos aparece esta etiquetas lo que seucede es q las imagenes son de solo lectura y lo que hace docker es crear una imagen y la otra imagen le coloca <none> donde el nombre y el tag son iguales 
# Docker multi stage build

# Contenedores
- Son una instancia de ejecuacion de una imagen
- Son temporales
- Capa de rw
- Podemos crear varios partiendo de una misma imagen
# Listar puertos
- docker run -d -p [Puesto nuestra maquina]:[Puerto del contenedor] jenkins
> docker run --name my-dbl -p 3306:3306 -e MYSQL_ROOT_PASSWORD=admin -d mysql
## Listar volume
> docker volume ls
## Ingresar modo rrot
> docker exec -ti -u root drupal bash
## Ver stats de un contendor
> docker stats [nameContainer | idContainer ]
## Limitar recursos conteneodr puede consumir
> docker run -d -m "500mb | 5gb" --name myNameContainer nameImage
## Limitar cpu
> docker run -d --cpuset-cpus 0-1 --name myNameContainer nameImage
## Para copiar archivos  desde afuera al docker
> docker cp index.html [nameCOntainer]:/tmp
## Para copiar archivos desde el docker hacia la computadora 
> docker cp [nameCOntainer]:/var/log/miarchivodocker.txt .
## Docker contendor que se autodestruye
> docker run --rm --ti --name centos centos
## Mostrar netwokr de docker
> docker network
## Inspeccionar una network
> docker network inspect [name network]
## Conectar contenedores en la misma red
> docker run -d --network docker-test-my-network --name cont1 -ti centos
> docker run -d --network docker-test-my-network --name cont2 -ti centos
## Conectar contenedores en distintas redes
> docker network connect  docker-test-network containerName
## Como desconectar los contenedores de distintas redes
> docker network disconnect  docker-test-network containerName
## Eliminar una red
> docker network rm myNetworkcustom
## Asignar una IP a un contenedor
> docker network create --subnet 172.128.10.0/4 --gatewarey 172.128.10.1 -d bridge my-testnetw

> docker run --network my-net -d --name nginxl --ip 172.10.50 -ti gninxl
## LA red de Host
> docker run --network host -d --name tst2 --ti centos
# Volumenes
- Los volumenes permiten almacenar data persistente del contendor
Existen 3 tipo de volumenes
- Host archivo especificados en nuestra maquinba
- Anonymus volumenes especificado aletoriamente por docker
- Named Volumens volumenes adminsitrados por docker
## Porq es importante los volumenes?
Para mantener la persistencia de los datos que sean importnates en nuestro equipoo
> docker run --name some-mysql -v /miDirectorioLocal/:/directorioContenedor -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag

> docker run --name some-mysql -v /miDirectorio/:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag
## DOcker anonimos 
- tienen nombres aletorias hash
- se crea en un arhivo alteroia del lugar
- cuando se elimina el Container se borra el volumen anonimo
## Volumenes Nombrados
- se nombre en los docekr files con VOLUME
- utiliza la misma logica q los VOLUME anonimos

# Docker Compose
- Es una herramientas q nos ayuda a crear aplicaciones multicontendor
- Podemos Definiar
    - Contenedores
    - Imangesn
    - Volumunenes
    - Redes
    - ...
## Las propiedaes son
- version: 
- services:
- volumnes:
- networks:
```yml
version: '3'
services:
  web:
    container_name: nginx1
    ports:
      - "8080:80"
    image: nginx
```
## Para levantar el servicio de docker-compose.yml
> docker-compose up -d
## Para deeter el servicio docker-compose
> docker down
## Variales de entorno
```yml
version: '3'
services:
    db:
        image: mysql:5.7
        container_name: mysql
        ports:
            - "3306:3306"
        enviroment:
            - "MYSQL_ROOT_PASSWORD=1234566"
```
Tambien podemos definirlo enun archivo llamano common.env
```yml
version: '3'
services:
    db:
        image: mysql:5.7
        container_name: mysql
        ports:
            - "3306:3306"
        env_file: common.env
```
## Volumenes en docker compose
### Volumenees nombrados
```yml
version: '3'
services:
  web:
    container_name: nginx1
    ports:
      - "8080:80"
    volumens:
      - "vol2:/usr/share/ngix/html"
    image: nginx
volumen:
    vol2:
```
### Volumenees host
```yml
version: '3'
services:
  web:
    container_name: nginx1
    ports:
      - '8080:80'
    volumes:
      - 'E:\proyects_docker\tutorial\project-4:/usr/share/nginx/html'
    image: nginx
```
## Redes en docker compose
```yml
version: '3'
services:
  web:
    container_name: nginx1
    ports:
      - "8080:80"
    image: nginx
		networks:
			- net-test
	web:
    container_name: nginx2
    ports:
      - "8080:81"
    image: nginx
		networks:
			- net-test
networks:
	net-test:
```
## Construye imagenes con docker-compose.yml
> docker-compose build
```yml
version: '3'
services:
  web:
    container_name: nginx1
		build:
			context: .
    ports:
      - '8080:80'
    volumes:
      - 'E:\proyects_docker\tutorial\project-4:/usr/share/nginx/html'
    image: nginx
```
## Sobreescribiar el CMD de un contenedor con COmpose
```yml
version: '3'
services:
  web:
    container_name: nginx1
		command: python -m SimpleHttpServer 8080
		build:
			context: .
    ports:
      - '8080:80'
    volumes:
      - 'E:\proyects_docker\tutorial\project-4:/usr/share/nginx/html'
    image: nginx
```
## Limitar recursos de la memoria
```yml
version: "3.9"
services:
  redis:
    image: redis:alpine
    deploy:
      resources:
        limits:
          cpus: '0.50'
          memory: 50M
        reservations:
          cpus: '0.25'
          memory: 20M
```
## Politico de renicio de contendores

Flag	Description
- **no**	Do not automatically restart the container. (the default)
- **on-failure**	Restart the container if it exits due to an error, which manifests as a non-zero exit code.
- **always**	Always restart the container if it stops. If it is manually stopped, it is restarted only when Docker daemon restarts or the container itself is manually restarted. (See the second bullet listed in restart policy details)
- **unless-stopped**	Similar to always, except that when the container is stopped (manually or otherwise), it is not restarted even after Docker daemon restarts.
```yml
version: '3'
services:
	test:
		container_name: test
		image: restar-image
		build: .
		restart: unless-stopped
```