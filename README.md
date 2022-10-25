# Hola mundo

```bash
docker build -t andyjesus2/debian .\project_one\
# Ejecutar  Y INTERACTUAR docker
docker run -it 6f6545164e69
# Descargar ubuntu
docker pull ubuntu
```

# Docker images
- Es un template para crear un entorno
- Este contiene todos los elementos necesitado para tu app librerías evn, config, Files software
- Este puede tener una version o snapshots basado en un tiempo
- Este es inmutable, pero este puede ser clonado o compartido
- Esas imágenes son creados usando Dockerfile
- Es la imágenes se puede decir q son como instaladores que crean Distintos procesos llamados Contenedores
- Cada imagen se le puede pasar parámetros depende de su creador
- Existen imágenes oficiales
- Se puede crear imágenes personalizadas
# Contenedores vs VMS
- un contenedor es una instancia de la imagen
- el contenedor es solo un proceso del sistema
- la maquina virtual es todo un set completo del Sistema operativo

# IMAGES
## Listar contener

`docker ps`

## Ver los LOGS de un Contenedor

`docker logs -f myNameContainer`

## Instalar una imagen pull

`docker pull mongo`

## instalar una imagen con una tag especifica

`docker pull mongo:3.6.5-jessie`

## Ejecutar una imagen con parámetros

`-d` sirve para ejecutar la imagen en segundo plano

`docker run -d -p 80:80 apache`

# Images crear con DockerFile

## Construir una imagen desde un DockerFile

Sirve para crear una imagen tomando de base un DockerFile
`docker build -t [NameImage] .`
`docker build -t apache .`
## .dockerignore
sirve para ignorar carpetas 

# Example DockerFile

```Dockerfile
# FROM: la imagen que va a tomar
FROM centos
# LABEl: es para agregar metadescripcion a  tu imagen
LABEL version=1.0
LABEL description=This is an image
# RUN: ejecuta comandos antes que la imagen se monte
# WORKDIR: Significa donde estas trabajando actualmente, te mueve de directorio
# COPY beryllium html
WORKDIR /var/wwww
# RUN: sirve para ejecutar comandos
RUN yum install httpd -y
# COPY : Copia un  archivo de tu maquina local a la imagen
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
# CMD: es para ejecutar una tarea que se mantendrá a la escucha y esta mantendrá ejecutando a la imagen
CMD apache
```
## RUN vs CMD
No confunda RUN con CMD. RUN en realidad ejecuta un comando y confirma el resultado; CMD no ejecuta nada en el momento de la compilación de la imagen, pero especifica el comando previsto para la imagen.

## DockerFile buenas practicas

- Efímeros
- Un servicio por contenedor
- Build context utilizar dockerignore
- pocas capas
- utilizar labels

## Docker Container
- It es una instancia de una imagen
- Tu puedes buscar una docker hub container repositorio

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

Link los docker que depende de unos
Docker crea un túnel seguro entre lso contenedores que no requieren exponer ninugn puerto externamente del contenedor

`docker run -d -p 5000:5000 --link [nombre del contenedor] dockerapp:0.1`

Para ver los logs
¿ Como funciona los enlances entre los contenedores?
`
docker exec -it [iddocker] bash
more /etc/hosts
`
## Comando útiles de docker-compose
```bash
docker-compose up -d
docker-compose ps
docker-compose logs [name-container]
```
## Eliminar una imagen con su volúmenes incluidos

`docker rm -fv thirsth_goodall`


## Listar las images danling

`docker images -f dangling=true`


## Dangling images
- <none> <none>
cuando nos aparece esta etiquetas lo que sucede es q las imágenes son de solo lectura y lo que hace docker es crear una imagen y la otra imagen le coloca <none> donde el nombre y el tag son iguales 
Es una imagen sin referencia, cuando se genera una nueva imagen y no se especifica una tag


# Contenedores
- Son una instancia de Ejecución de una imagen
- Son temporales
- Capa de rw 
- Podemos crear varios partiendo de una misma imagen

## Ver Información del contenedor

Ver el contenedor que mas esta consumiendo

`docker top [idName | NameContainer]`

Ver Stats del contenedor

`docker stats [IdName | NameContainer]`
## Información y gestión del sistema de los contenedores

`docker system info`

Ver los docker y los Tamaño

`docker system df`

Eliminar todos los contendores network danling images danling build cache
`docker system prune`

## Mover archivos a los contendores 

`docker cp miArchivoLocal.txt [NameContainer]:/tmp`


## Ver características del contenedor

`docker inspect [IdName | NameContainer]` 

mandar el inspect a un fichero

`docker inspect [IdName | NameContainer] > container.txt`

## Ver logs del contendor

`docker logs --tail 10 [IdContainer | NameContainer]`

Ver de manera directa 
`docker logs -f 10  [IdContainer | NameContainer]`
## PARAR y ELIMINAR un contenedor al mismo tiempo

`docker kill [IdContainer | NameContainer]`

## Correr un Contenedor modo Background

```bachs
docker run -d nginx
```
## Listar contenedor
muestra los contendor que estan corriendo y los que no
`docker ps`

`docker ps -a`

## Renombrar el contenedor

`docker rename oldName newName`

## Listar y mapear los puertos puertos

`docker run -d -p [Puesto nuestra maquina]:[Puerto del contenedor] jenkins`

`docker run --name my-dbl -p 3306:3306 -e MYSQL_ROOT_PASSWORD=admin -d mysql`

## Listar volúmenes disponibles

`docker volume ls`

`docker ps -a`

## Iniciar / Reiniciar / Detener Contenedor

```
docker stop [id | Nombre ]
docker start [id | Nombre ]
docker restart [id | Nombre ]
```

## Ingresar modo ROT
`-ti` significa interactivo

`docker exec -ti -u root drupal bash`

## Variables de entorno

Son las variables que se pasan al iniciar un contenedor del docker File

`docker run --name my-dbl -p 3306:3306 -e MYSQL_ROOT_PASSWORD=admin -d mysql`

## Ver stats de un Contenedor

`docker stats [nameContainer | idContainer ]`

## Limitar recursos Contenedor puede consumir

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

## Ver Imágenes

`docker images | grep centos`

## Eliminar Imágenes

`docker rmi centos:prueba1`

## Sobrescribir el CMD de una imagen sin un DockerFile

`docker run -dti centos echo hello world`
`docker un -d -p 8080:8080 centos python -m SimpleHTTPServer 8080`

## Contenedor que se autodestruya

`docker run --rm -ti --name centos centos bash`
# REDES
Las redes de docker por defecto son bridge
existen 3 tipos de redes
- dridge
- host
- none
## Listar redes

`docker network ls`

## Comprobar puertos de las Contenedores/Imagenes

`docker port [nameContainer | IdContainer]`

## Crear redes

Los drivers  son (bridge, bridge)

`docker network create red1`

## Inspeccionar una red

`docker network inspect [NameRed]`


# Volúmenes
- Sirve para mantener data Persistente en nuestra maquina local.
- Los volúmenes permiten almacenar data persistente del contenedor

Existen 3 tipo de volúmenes
- [Bind Amount] archivo especificados en nuestra maquina
- [Anonymous volúmenes] especificado de forma aleatoria por docker
- [Named Volúmenes] volúmenes administrados por docker
## Bing Amount 
Los bing amount han existido desde los primeros días de Docker. Los bing amount tienen una funcionalidad limitada en comparación con los volúmenes. Cuando se utiliza un montaje de enlace, un archivo o directorio en la máquina anfitriona se monta en un contenedor. El archivo o directorio es referenciado por su ruta absoluta en la máquina anfitriona. Por el contrario, cuando se utiliza un volumen, se crea un nuevo directorio dentro del directorio de almacenamiento de Docker en la máquina anfitriona, y Docker gestiona el contenido de ese directorio.
No es necesario que el archivo o directorio ya exista en el host de Docker. Se crea bajo demanda si aún no existe. Los montajes Bind son muy eficaces, pero dependen de que el sistema de archivos de la máquina anfitriona tenga una estructura de directorios específica disponible. Si estás desarrollando nuevas aplicaciones Docker, considera usar volúmenes con nombre en su lugar. No puedes utilizar los comandos de la CLI de Docker para gestionar directamente los bing amount.

- `--mount`: Consiste en múltiples pares clave-valor, separados por comas y cada uno de ellos formado por una tupla <clave>=<valor>. La sintaxis de --mount es más verbosa que -v o --volume, pero el orden de las claves no es significativo y el valor de la bandera es más fácil de entender.
  - El tipo de montaje, que puede ser bind, volumen o tmpfs. Este tema trata sobre montajes bind, por lo que el tipo es siempre bind.
  -  El `source`. En el caso de los montajes bind, se trata de la ruta al archivo o directorio en el host del demonio Docker. Puede especificarse como source o src.
  -  El `destination` toma como valor la ruta donde se monta el archivo o directorio en el contenedor. Puede especificarse como destination, dst o target.
  -  La opción `readonly`, si está presente, hace que el montaje bind se monte en el contenedor como de sólo lectura.
    La opción bind-propagation, si está presente, cambia la propagación de bind. Puede ser una de las opciones rprivate, private, rshared, shared, rslave, slave.
  -  La bandera `--mount` no soporta las opciones z o Z para modificar las etiquetas de selinux.

### Configurar Bind propagation
La `bind propagation` es por defecto rprivate tanto para los `bind propagation` como para los volúmenes. Sólo es configurable para los `bind propagation`, y sólo en máquinas anfitrionas Linux. La propagación de bind es un tema avanzado y muchos usuarios nunca necesitan configurarlo.

La `bind propagation` se refiere a si los montajes creados dentro de un determinado bind-mount pueden o no propagarse a las réplicas de ese montaje. Considere un punto de montaje `/mnt`, que también está montado en `/tmp`. La configuración de propagación controla si un montaje en `/tmp/a` también estará disponible en `/mnt/a` Cada configuración de propagación tiene un contrapunto recursivo. En el caso de la recursión, considere que `/tmp/a` también está montado como `/foo`. La configuración de propagación controla si `/mnt/a` y/o `/tmp/a` existirían.

- shared: Los submontajes del montaje original se exponen a los montajes de réplica, y los submontajes de los montajes de réplica también se propagan al montaje original.
- slave: similar a un montaje compartido, pero sólo en una dirección. Si el montaje original expone un submontaje, el montaje de réplica puede verlo. Sin embargo, si el montaje de réplica expone un submontaje, el montaje original no puede verlo.
- private: 	El montaje es privado. Los submontajes dentro de él no están expuestos a los montajes de réplica, y los submontajes de los montajes de réplica no están expuestos al montaje original
- rshared: Lo mismo que compartido, pero la propagación también se extiende a y desde puntos de montaje anidados dentro de cualquiera de los puntos de montaje originales o réplicas.
- rslave: Lo mismo que esclavo, pero la propagación también se extiende a y desde puntos de montaje anidados dentro de cualquiera de los puntos de montaje originales o de réplica.
- rprivate: 	Por defecto. Lo mismo que privado, lo que significa que ningún punto de montaje en cualquier parte de los puntos de montaje originales o de réplica se propaga en cualquier dirección.
## Crear un Volumen

`docker volume create [Name]`

## Crear volumenes Temporales

`docker run -d -i --name ubuntu18 --tmpfs /datos ubuntu`

## Ver información volumen

`docker volume ls`



## Eliminar una imagen con su volúmenes incluidos

`docker rm -fv thirsth_goodall`

## Porque es importante los volúmenes?
Para mantener la persistencia de los datos que sean importantes en nuestro equipos 

`docker run --name some-mysql -v /miDirectorioLocal/:/directorioContenedor -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag`

`docker run --name some-mysql -v /miDirectorio/:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag`

## Volúmenes de HOST

`docker run -d --name db -p 3306:3306 -e "MYSQL_ROOT_PASSWORD=123456789" -v mydirectory/directory/:/var/lib/mysql/ `

## Volumnenes anonimos 
- tienen nombres aletorias normalmente nombrados con hash
- se crea en un archivo  aletorio del lugar
- cuando se elimina el Container se borra el volumen anonimo


## Volúmenes Nombrados
- se nombra  en los Docker files con VOLUME
- utiliza la misma logica q los VOLUME anonimos

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



# Docker Compose
Es una herramientas que nos ayuda a crear herramientas multi contenedores, donde podemos definir toda la configuraciones necesarias de estas
## Generar Container desde DockerCompose

`docker-compose up -d`

## Las propiedades del DockerCompose
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
## Para detener el servicio docker-compose
`docker down`
## Variables de entorno
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
## Volúmenes en docker compose
### Volúmenes nombrados
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
### Volúmenes host
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
## Construye imágenes con docker-compose.yml

`docker-compose build`
 si tiene un build: . busca un DockerFile por defecto en su ruta de archivo 
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
## Sobrescribir el CMD de un contenedor con COmpose
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