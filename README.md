> docker build -t andyjesus2/debian .\proyect_one\
// EJECTURAR Y INTERACTUAR docker
> docker run -it 6f6545164e69
// Descargar ubuntu
> docker pull ubuntu

# Docker images
- Es un template para crear un entorno
- Este contiene todos los elementos necesitado para tu app librerias evn, config, iles softwate
- Este puede tener una version o snapshots basado en un tiempo
- ESte es inmutable, pero este puede ser clonado o compartido
- Esas imagees son creados usando Dockerfile
- Es la imagenes se puede decir q son como instaladores que crean disintios procesos llamados contendores
- Cada imagen se le puede pasar parametros depende de su creador
- Existen imagenes oficiales
- Se puede crear imagenes personalizadas
## Listar contener

`docker ps`

## Ver los LOGS de un Contendor

`docker logs -f myNameContainer`

## Instalar una imagen pull

`docker pull mongo`

## instalar una imagen con una tag especifica

`docker pull mongo:3.6.5-jessie`

## Ejecutar una imagen con parametros

- `-d` sirve para ejecutar la imagen en sugndo plano

`docker run -d -p 80:80 apache`

# Dockerfile
## Construir una imagen desde un DockerFile

`docker build -t apache .`

## .dockerignore
sirve para ignorar carpetas 

## Example de docker file

```Dockerfile
# FROM: la imagen que va a tomar
FROM centos
# LABEl: es para agregar metadescripcion a  tu imagen
LABEL version=1.0
LABEL description=This is an image
# RUN: ejectua comandos antes que la imagen se monte
# WORKDIR: Significa donde estas trabajando actualemnte, te mueve de directorio
# COPY beryllium html
WORKDIR /var/wwww
# RUN: sirve para ejecutar comandos
RUN yum install httpd -y
# COPY : Copia un  archivo de tu maquina local a la iamgen
# COPY tuRuta RutaDestinoDImagen
# Add: Sirve para  Url donde puedes colocar tu url y este la agregara descargando el archivo
COPY beryllium /var/www/html
# CMD: es el comando que mantiene a la imagen corriendo
# ENV: son variables que puedes pasarle al docker file
# EXPOSE: expone el puerto
EXPOSE 8080
ENV contenido valorContenido
# Sirve para mantener la persistencia de datos con el ordenador
VOLUME /var/www/html
# USER: es para decir que usuario realiza la tarea por defecto es root
USER root
# CMD: es para ejecutar una tarea que se mantendra a la escucha y esta mantendra ejecutando a la imagen
CMD apache
```
## Eliminar una imagen con su volumenes incluidos

`docker rm -fv thirsth_goodall`

# Docker Container
- It es una instancia de una imagen
- Tu puedes buscar una docker hub container repostire

```Dockerfile
FROM ngix:latest
WORKDIR /usr/share/nginx/html
COPY . .
```

`docker build -t [usernameFromDockerHub]/[nameImage]:[tag] [directory]`

para ejecutar un comando desde la imagen en el contenedor ya se en ejecusion

`docker exec -it [idContenedior] bash`
`docker exect -u root -it bash`

Esto genera una imagen

`docker-compose build`

Este levanta los servicios

`docker-compose up`

Linkear los docker que depende de unos
Docker crea un tunerl seguro entre lso contenedores que no requieren exponer ninugn puerto externamente del contenedor

`docker run -d -p 5000:5000 --link [nombre del contenedor] dockerapp:0.1`

Para ver los logs
¿ Como funciona los enlances entre los contenedores?
`
docker exec -it [iddocker] bash
more /etc/hosts
`
## Comando utiles de docker-compose
```bash
docker-compose up -d
docker-compose ps
docker-compose logs [name-container]
```

# Buenas practicas para el docker file
- Efimeros 
- Multi linea
- no instalar paquetes innecesarios
- labels

# RUN vs CMD
No confunda RUN con CMD. RUN en realidad ejecuta un comando y confirma el resultado; CMD no ejecuta nada en el momento de la compilación de la imagen, pero especifica el comando previsto para la imagen.

## Dangling images
- <none> <none>
cuando nos aparece esta etiquetas lo que seucede es q las imagenes son de solo lectura y lo que hace docker es crear una imagen y la otra imagen le coloca <none> donde el nombre y el tag son iguales 
Es una imagen sin referencia, cuando se genera una nueva imagen y no se especifica una tag
## Listar las images danling

`docker images -f dangling=true`

## Docker multi stage build

# Contenedores
- Son una instancia de ejecuacion de una imagen
- Son temporales
- Capa de rw 
- Podemos crear varios partiendo de una misma imagen
## Renombar el contenedor

`docker rename oldName newName`

## Listar y mapear los puertos puertos

- docker run -d -p [Puesto nuestra maquina]:[Puerto del contenedor] jenkins

`docker run --name my-dbl -p 3306:3306 -e MYSQL_ROOT_PASSWORD=admin -d mysql`

## Listar volume

`docker volume ls`

`docker ps -a`

## Inicar / Reniciar / Dentener Contendor

```
docker stop [id | Nombre ]
docker start [id | Nombre ]
docker restart [id | Nombre ]
```

## Ingresar modo rrot
`-ti` significa interactivo

`docker exec -ti -u root drupal bash`

## Variables de entorno

Son las variables que se pasan al iniciar un contenedor del docker File

`docker run --name my-dbl -p 3306:3306 -e MYSQL_ROOT_PASSWORD=admin -d mysql`

## Ver stats de un contendor

`docker stats [nameContainer | idContainer ]`

## Limitar recursos conteneodr puede consumir

`docker run -d -m "500mb | 5gb" --name myNameContainer nameImage`

## Limitar cpu

`docker run -d --cpuset-cpus 0-1 --name myNameContainer nameImage`

## Para copiar archivos  desde afuera hacia el docker

`docker cp index.html [nameCOntainer]:/tmp`

## Para copiar archivos desde el docker hacia la computadora 

`docker cp [nameContainer]:/var/log/miarchivodocker.txt .`

## Docker contendor que se autodestruye

`--rm delete the container`

`docker run --rm --ti --name centos centos`

## Mostrar netwokr de docker

`docker network`

## Inspeccionar una network

`docker network inspect [name network]`

## Conectar contenedores en la misma red

`docker run -d --network docker-test-my-network --name cont1 -ti centos`
`docker run -d --network docker-test-my-network --name cont2 -ti centos`

## Conectar contenedores en distintas redes

`docker network connect  docker-test-network containerName`

## Como desconectar los contenedores de distintas redes

`docker network disconnect  docker-test-network containerName`

## Eliminar una red

`docker network rm myNetworkcustom`

## Asignar una IP a un contenedor

`docker network create --subnet 172.128.10.0/4 --gatewarey 172.128.10.1 -d bridge my-testnetw`


`docker run --network my-net -d --name nginxl --ip 172.10.50 -ti gninxl`

## LA red de Host

`docker run --network host -d --name tst2 --ti centos`

## Ver imagenes

`docker images | grep centos`

## Eliminar Imagenes

`docker rmi centos:prueba1`

## Sobreescribir el CMD de una imagen sin un DockerFile

`docker un -d -p 8080:8080 centos python -m SimpleHTTPServer 8080`

# Volumenes
- Sirve para mantener data Persistente en nuestra maquina local.
- Los volumenes permiten almacenar data persistente del contendor
Existen 3 tipo de volumenes
- Host archivo especificados en nuestra maquinba
- Anonymus volumenes especificado aletoriamente por docker
- Named Volumens volumenes adminsitrados por docker

## Eliminar una imagen con su volumenes incluidos

`docker rm -fv thirsth_goodall`

## Porq es importante los volumenes?
Para mantener la persistencia de los datos que sean importnates en nuestro equipoo 

`docker run --name some-mysql -v /miDirectorioLocal/:/directorioContenedor -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag`

`docker run --name some-mysql -v /miDirectorio/:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag`
## Volumenes de HOST

`docker run -d --name db -p 3306:3306 -e "MYSQL_ROOT_PASSWORD=123456789" -v mydirectory/directory/:/var/lib/mysql/ `

## Volumnenes anonimos 
- tienen nombres aletorias hash
- se crea en un archivo  aletorio del lugar
- cuando se elimina el Container se borra el volumen anonimo


## Volumenes Nombrados
- se nombre en los Docker files con VOLUME
- utiliza la misma logica q los VOLUME anonimos



## Docker Compose
- Es una herramientas q nos ayuda a crear aplicaciones multicontendor
- Podemos Definiar
    - Contenedores
    - Imangesn
    - Volumunenes
    - Redes
    - ...
## Example VOLUMENES nombrados

```
docker volume create my-vol
docker volume ls
docker run -d --name db -p 3306:3306 -e "MYSQL_ROOT_PASSWORD=123456789" -v my-vol:/var/lib/mysql/
```
NOTA: al eliminar el contenedor no se elimina el volumen al ser este creado

`docker rm -fv mysql`

## Example persistiendo Data en MongoDB

```
docker run -d -p 27017:27017 -v mydirectory/directory:?data/db -d mongo
docker exec -ti myNameContainer bash
```
## Listar Volumenes creados

`docker volume ls -f dangling=true`

`docker volume ls -f dangling=true -q`

`docker volume rm idVolumen`

## Dangling Volumen
`docker v`
## Comparte Volumenes entre uno o mas contendores
## Docker Compose
Es una herramientas que nos ayuda a crear herramientars multicontendores, donde podemos definir toda la configuraciones necesarias de estas
## Generar Container desde DockerCompose

`docker-compose up -d`

## Las propiedaes del DockerCompose
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
`docker-compose up -d`
## Para deeter el servicio docker-compose
`docker down`
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
Tambien podemos definirlo enun archivo Llamandolo como  
`common.env`
```
MYSQL_ROOT_PASSWORD=12345678
hola=hola12
```
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

`docker-compose build`

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

## example wordpress mysql
```yml
version: '3'

services:
	db:
		container_name: wp-mysql
		image: mysql:5.7
		volumens:
			- $PWD/data:/var/lib/mysql
		enviroment:
			MYSQL_ROOT_PASSWORD: 123456789
			MYSQL_DATABASE: wordpress
			MYSQL_USER: wordpress
			MYSQL_PASSWORD: wordpress
		ports:
			-	"3306:3306"
		networks:
			-	my_net

	wp:
		container_name: wp-web
		volumens:
			-	"$PWD/html:/var/www/html"
		dependes_on:
			-	db
		image: wordpress:lastes
		porst:
			-	"80:80"
		enviroment:
			WORDPRESS_DB_HOST: db:3306
			WORDPRESS_DB_USER: wordpress
			WORDPRESS_DB_PASSWORD: wordpress
		networks:
			-	my_net
network:
	my_net:
```
## Buenas practicas
### ¿ Porque y para que los dotfiles?