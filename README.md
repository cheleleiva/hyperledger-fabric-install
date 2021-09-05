# Instalación de Hyperledger Fabric

## Actualizar Repositorios de Servidor

```
sudo apt update
```
```
sudo apt upgrade
```

## Instalar dependencias

```
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

## Instalar Docker

Se debe de agregar el repositorio de Docker al manejador de paquetes de Ubuntu

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo apt-key fingerprint 0EBFCD88

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

sudo apt update

sudo apt install docker-ce docker-ce-cli containerd.io

```

Pasos Post Instalación de Docker (Ejecución sin sudo)

```
sudo groupadd docker

sudo usermod -aG docker $USER
```


Probamos la instalación de Docker

```
docker --version

docker ps -a

```

## Instalar Go

Asegurarnos de estar en la carpeta `home`

```
cd ~
```
Descargamos y descomprimimos Go

```
sudo curl -O https://dl.google.com/go/go1.13.3.linux-amd64.tar.gz

sudo tar -xvf go1.13.3.linux-amd64.tar.gz

```

Debemos editar el archivo `~./bashrc` para agregar los paths de Go y agregarlos a nuestro `PATH`

```
sudo vi ~/.bashrc
```

Agregar las siguientes lineas al final del fichero

```
export GOROOT=$HOME/go
export GOPATH=$HOME/work
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```

Recargamos el archivo `~./bashrc` para que los efectos tengan validez

```
source ~./bashrc
```

Comprobamos que Go esta instalado

```
go version

```

## Instalación de Fabric y Descarga de Ejemplos

Debemos de crear las carpetas `work` y `src` que son necesarias por Go para ejecutar y compilar el código.

```
cd ~

mkdir work && cd work

mkdir src && cd src
```

Clonamos el repositorio `fabric-samples` en la rama v1.4.0.

Al ejecutar el siguiente comando descargamos un script que descarga los archivos necesarios para ejecutar Fabric y las imágenes de Docker para su funcionamiento.

```
curl -sSL http://bit.ly/2ysbOFE | bash -s -- 1.4.0 1.4.0
```

Ingresamos a la carpeta `fabric-samples`

```
cd fabric-samples
```

Ejecutamos el ejemplo

```
./byfn.sh -m generate

./byfn.sh -m up
```


