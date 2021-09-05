# Instalación de Hyperledger Fabric
Autor: Oscar Leiva

Email: oscarleiva@klusterone.com / cheleleiva@gmail.com

---

Para esta instalación seguiremos los siguientes pasos:

1. Actualización de respositorios y actualización del Servidor

2. Instalar dependencias para Docker y Docker Compose

3. Instalación de Docker

4. Instalación de Docker Compose

5. Instalación de Go

6. Descarga de Fabric (Binarios, ejemplos e imagenes de Docker).

7. Ejecución del ejemplo **First-Network**.
-----

## Actualizar Repositorios de Servidor

```sh
sudo apt update
```
```sh
sudo apt upgrade
```

## Instalar dependencias

```sh
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```
---
## Instalar Docker

Se debe de agregar el repositorio de Docker al manejador de paquetes de Ubuntu

```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo apt-key fingerprint 0EBFCD88

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

sudo apt update

sudo apt install docker-ce docker-ce-cli containerd.io

```

Pasos Post Instalación de Docker (Ejecución sin sudo) [Mas Info](https://docs.docker.com/engine/install/linux-postinstall/)

```sh
sudo groupadd docker

sudo usermod -aG docker $USER
```

**Importante:** Luego de ejecutar los últimos comandos debemos de cerrar la cesión del usuario e iniciarla nuevamente para que surtan efecto los cambios. Para cerrar sesión desde la consola web de Google Cloud, podemos ejecutar el comando `exit`.


Probamos la instalación de Docker

```sh
docker --version

docker ps -a

```
---
## Instalar Docker Compose

[Documentación Oficial Instalación de Docker Compose](https://docs.docker.com/compose/install/)

**Importante:** No debemos confundir Docker Compose, con [Hyperledger Composer](https://hyperledger.github.io/composer/latest/).

Docker Compose es una herramienta para definir y ejecutar aplicaciones Docker multicontenedor. Con Compose, se utiliza un archivo YAML para configurar los servicios de la aplicación. [Mas Info](https://docs.docker.com/compose/)

Primero descargamos Docker Compose

```sh

 sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
Luego tenemos que aplicar permisos de ejecución al archivo binario

```sh
sudo chmod +x /usr/local/bin/docker-compose
```

Podemos verificar la instalación de Docker Compose con el comando

```sh
docker-compose --version
```

---

## Instalar Go

Asegurarnos de estar en la carpeta `home`

```sh
cd ~
```
Descargamos y descomprimimos Go

```sh
sudo curl -O https://dl.google.com/go/go1.13.3.linux-amd64.tar.gz

sudo tar -xvf go1.13.3.linux-amd64.tar.gz

```

Debemos editar el archivo `~./bashrc` para agregar los paths de Go y agregarlos a nuestro `PATH`

```sh
sudo vi ~/.bashrc
```

Agregar las siguientes lineas al final del fichero

```sh
export GOROOT=$HOME/go
export GOPATH=$HOME/work
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```

Recargamos el archivo `~./bashrc` para que los efectos tengan validez

```sh
source ~./bashrc
```

Comprobamos que Go esta instalado

```sh
go version

```
---
## Instalación de Fabric y Descarga de Ejemplos

Debemos de crear las carpetas `work` y `src` que son necesarias por Go para ejecutar y compilar el código.

```sh
cd ~

mkdir work && cd work

mkdir src && cd src
```

Clonamos el repositorio `fabric-samples` en la rama v1.4.0.

Al ejecutar el siguiente comando descargamos un script que descarga los archivos necesarios para ejecutar Fabric y las imágenes de Docker para su funcionamiento.

```sh
curl -sSL http://bit.ly/2ysbOFE | bash -s -- 1.4.0 1.4.0
```

Ingresamos a la carpeta `fabric-samples`

```sh
cd first-network
```
---
## Ejemplo First Network

```sh
./byfn.sh -m generate

./byfn.sh -m up
```

## Contenedores Creados

Para verificar los contenedores que se han creado del ejemplo `first-network` ejecutamos el comando

```sh
docker ps -a
```


