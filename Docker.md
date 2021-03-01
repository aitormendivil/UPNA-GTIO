# Introduction to Docker

*Aitor Mendivil grau*

Desventajas de las aplicaciones monoliticas:
* Desde el punto de vista de la aplicacion:
    * La replicacion supone una copia entera de la aplicacion aunque solo se este usando un componente especifico
    * Las bases de datos relacionales no estan pensadas para ser replicadas
* Desde el punto de vista del equipo de desarrollo:
    * Cualquier cambio supone el despliegue entero de toda la aplicacion.
    * Dificil de testear si tiene mucha dependencia interna.
    
Como se pueden resolver:
* Desarrollar cada componente en un repositorio diferente
* Es necesaria una matriz de compatibilidades para fijar con que versiones de los otros componentes el componente actual funciona.
* Se crea un problema a la hora de desplegar nuevas versiones para las pruebas de integracion que necesitan de coordinacion adicional.

## Why Docker?
* Very Useful, you will realise it later on
* Easy to use
* Major Companies use it
* Companies around us use it, so it is a plus for finding the best job

## Docker Containers
A file system made of layers and a process

Docker se aisla del sistema operativo 
OS - FS- PID
Permite definir una capa de lectura y otra de lectura gestionado por Docker y se lanzan los procesos.
Tendriamos varias capas del FS en modo read /r y encima como ultima capa una de escritura /rw.

## Containers Vs Virtual Machines

##### Docker Pros
* Easy to Use
* Lightweight and Powerful
* Fast to deploy
* Easy to share
* Microservice architectures
* No es necesario copiar todo el sistema de ficheros (fichero Dockerfile donde se define el sistema de ficheros y los ficheros)
   * Se puede añadir al repositorio
   * En cualquier sistema linux funciona igual
   * Perfecto para equipos de desarrollo de microservicios con integracion continua.
   * Mismo despliegue

##### Docker Cons
* Only Linux
* Not as good performance (but almost) as a similar on-premise installation

##### VM Pros
* Largely adopted
* Useful for managing DPCs and IaaS
* Hypervisors are very powerful managing shared hardware resources

##### VM Cons
* Slow to update/mantain/deploy
* Not easy share
* More complex (networking)

## Docker Basic Components
Dockerfile 
Dealer build
Register

Run (no apuntar)
### Docker Engine

#### Installation

Antes de nada utiliza la opción:

```sudo -s```

Para no poner sudo antes de cada comando

https://docs.docker.com/engine/install/ubuntu/

```shell
# Docker installation
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install docker-ce
```

Once you are done installing Docker, test your Docker installation by running the following:
```
$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
03f4658f8b78: Pull complete
a3ed95caeb02: Pull complete
Digest: sha256:8be990ef2aeb16dbcb9271ddfe2610fa6658d13f6dfb8bc72074cc1ca36966a7
Status: Downloaded newer image for hello-world:latest

Hello from Docker.
This message shows that your installation appears to be working correctly.
...
```

### Docker Images
A Docker Image is a type of container. Docker images have intermediate layers that increase reusability, decrease disk usage, and speed up docker build by allowing each step to be cached. These intermediate layers are not shown by default.
```
# To List images:
Usage:  docker images [OPTIONS] [REPOSITORY[:TAG]]
```

### Docker Hub
[DockerHub](http://hub.docker.com)


##### CHALLENGE 1
```
# Find an image that you can use daily (for example Nginx) and get familiar with the Main Page
```

## Using Docker

### Getting Images from the Hub/Registry
```
# pull command will only download the image.
docker pull ubuntu:zesty
```

To get started, let's run the following in our terminal:
```
$ docker pull ubuntu:zesty
```

The `pull` command fetches the alpine **image** from the **Docker registry** and saves it in our system. You can use the `docker images` command to see a list of all images on your system.
```
$ docker images
REPOSITORY              TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
alpine                 latest              c51f86c28340        4 weeks ago         1.109 MB
ubuntu:zesty           latest              690ed74de00f        5 months ago        960 B
```

##### CHALLENGE 2
```
# Get and list the previous image from Challenge 1
```

### Running Containers

https://docs.docker.com/engine/reference/commandline/run/

There are a lot of options for running containers. These are the most common:
```
Usage: docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
--help                  Print usage
--env , -e              Set environment variables
--interactive , -i      Keep STDIN open even if not attached
--name                  Assign a name to the container
--publish , -p          Publish a container’s port(s) to the host
--tty , -t              Allocate a pseudo-TTY
--volume , -v           Bind mount a volume
...
```

Great! Let's now run a Docker **container**. To do that you are going to use the `docker run` command.

```
$ docker run ubuntu:zesty ls -l
total 64
drwxr-xr-x   2 root root 4096 Nov 22  2017 bin
drwxr-xr-x   2 root root 4096 Apr 10  2017 boot
drwxr-xr-x   5 root root  340 Oct  3 08:28 dev
drwxr-xr-x   1 root root 4096 Oct  3 08:28 etc
drwxr-xr-x   2 root root 4096 Apr 10  2017 home
drwxr-xr-x   8 root root 4096 Feb 16  2017 lib
drwxr-xr-x   2 root root 4096 Nov 22  2017 lib64
drwxr-xr-x   2 root root 4096 Nov 22  2017 media
drwxr-xr-x   2 root root 4096 Nov 22  2017 mnt
drwxr-xr-x   2 root root 4096 Nov 22  2017 opt
dr-xr-xr-x 445 root root    0 Oct  3 08:28 proc
drwx------   2 root root 4096 Nov 22  2017 root
drwxr-xr-x   1 root root 4096 Dec 14  2017 run
drwxr-xr-x   1 root root 4096 Dec 14  2017 sbin
drwxr-xr-x   2 root root 4096 Nov 22  2017 srv
dr-xr-xr-x  13 root root    0 Oct  3 08:28 sys
drwxrwxrwt   2 root root 4096 Nov 22  2017 tmp
drwxr-xr-x   1 root root 4096 Nov 22  2017 usr
drwxr-xr-x   1 root root 4096 Nov 22  2017 var
```

What happened? When you call `run` it is like a shortcut that does several things:
1. The Docker daemon checks local store if the image (alpine in this case) is available locally, and if not, downloads it from Docker Store. (Since we have issued `docker pull alpine` before, the download step is not necessary)
2. The Docker daemon creates the container and then runs a command in that container. The command is the first process that will be executed inside the container.
3. Docker streams the output of the command to the standard output (your shell)

When you run `docker run ubuntu:zesty`, you provided a command (`ls -l`), so Docker started the command specified and you saw the listing. More on commands later.

Let's now try to launch a shell inside our container, in order to interact with it, just as we do with our host computer:
```
$ docker run ubuntu:zesty /bin/sh
```

Wait, nothing happened! Is that a bug? Well, no. These interactive shells will exit after running any scripted commands, unless they are run in an interactive terminal - so for this example to not exit, you need to `docker run -it ubuntu:zesty /bin/sh`.

You are now inside the container shell and you can try out a few commands like `ls -l`, `ps axu`, `top` (to view resources) and others. Exit the container by executing the `exit` command.


### Listing Containers

`docker ps` command shows you all containers that are currently running

```
Usage: docker ps [OPTIONS]
--all , -a          Show all containers (default shows just running)
--filter , -f       Filter output based on conditions provided
--format            Pretty-print containers using a Go template
--last , -n -1      Show n last created containers (includes all states)
--latest , -l       Show the latest created container (includes all states)
--no-trunc          Don’t truncate output
--quiet , -q        Only display numeric IDs
--size , -s         Display total file sizes
```

try it:
```
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

If you want to see previous ran containers, you can use the option `-a`. Try runnig:
```
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
967bf511e52a        ubuntu:zesty             "/bin/sh"                6 minutes ago       Exited (0) 6 minutes ago                               romantic_mayer
7cd8e0cf10f1        ubuntu:zesty             "ls -l"                  13 minutes ago      Exited (0) 13 minutes ago                              flamboyant_lewin
5fea3d29d038        b7d15a7e8ffd             "/bin/bash"              8 days ago          Exited (127) 8 days ago                                keen_rosalind
...
```

##### CHALLENGE 3
```
# Find an image that is useful for your daily job in the Docker Hub and try to run it. For example: nginx, alpine, python, java...
```

## Run a static website

The image that you are going to use is a single-page website that was already created for a Docker 101 course and is available on the Docker Store as [`dockersamples/static-site`](https://store.docker.com/community/images/dockersamples/static-site). You can download and run the image directly in one go using `docker run` as follows.

```
$ docker run -d dockersamples/static-site
```

>**Note:** The current version of this image doesn't run without the `-d` flag. The `-d` flag enables **detached mode**, which detaches the running container from the terminal/shell and returns your prompt after the container starts. We are debugging the problem with this image but for now, use `-d` even for this first example.

But we can't access the website yet! The container is executed inside it's own network, so we need ports in our host to access it!

Let's re-run the command with some new flags to publish ports and pass your name to the container to customize the message displayed. We'll use the *-d* option again to run the container in detached mode.

Stop the container that you have just launched. In order to do this, we need the container ID.

### Stopping/killing Containers

```
# Stopping
Usage: docker stop [OPTIONS] CONTAINER [CONTAINER...]
# Killing
Usage: docker kill [OPTIONS] CONTAINER [CONTAINER...]
```

but first we need to get its ID: (First column)

```
$ docker ps
CONTAINER ID        IMAGE                  COMMAND                  CREATED             STATUS              PORTS               NAMES
f7e1e504ca3e        dockersamples/static-site   "/bin/sh -c 'cd /usr/"   28 seconds ago      Up 26 seconds       80/tcp, 443/tcp     crazy_galileo
```

And now stop and remove it!
```
$ docker stop f7e1e504ca3e
$ docker rm   f7e1e504ca3e
```

Let's run it properly exposing the ports! 

```
$ docker run --name static-site -d -P dockersamples/static-site
```

In the above command:

*  `-d` will create a container with the process detached from our terminal
* `-P` will publish all the exposed container ports to random ports on the Docker host.
* `-e` is how you pass environment variables to the container
* `--name` allows you to specify a container name

with `-P` the ports are assigned automatically. We can check them using:

```
$ docker ps
CONTAINER ID        IMAGE                       COMMAND                  CREATED             STATUS              PORTS                                           NAMES
f7e1eb4fc224        dockersamples/static-site   "/bin/sh -c 'cd /usr…"   4 minutes ago       Up 4 minutes        0.0.0.0:32769->80/tcp, 0.0.0.0:32768->443/tcp   static-site
```

or:

```
$ docker port static-site
443/tcp -> 0.0.0.0:32772
80/tcp -> 0.0.0.0:32773
```

now try to access http://localhost:32772 in your web browser. (Replace the port with your own `http://<YOUR_IPADDRESS>:[YOUR_PORT_FOR 80/tcp]`)

you can also specify your own port with `-p` option. Is mandatory to know the exposed ports.

```
$ docker run --name static-site-2 -d -p 8888:80 dockersamples/static-site
```

Let's remove all proof of existence of the previous containers ;)

```
$ docker rm -f static-site
$ docker rm -f static-site-2
```

Remove all uneeded containers and check your environment is clean:

Run `docker ps` to make sure the containers are gone.

```
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

## Building Your Own Docker Image
[Image Building Reference](https://docs.docker.com/engine/reference/builder/)

An important distinction with regard to images is between _base images_ and _child images_.

- **Base images** are images that have no parent images, usually images with an OS like ubuntu, alpine or debian.

- **Child images** are images that build on base images and add additional functionality.

Another key concept is the idea of _official images_ and _user images_. (Both of which can be base images or child images.)

- **Official images** are Docker sanctioned images. Docker, Inc. sponsors a dedicated team that is responsible for reviewing and publishing all Official Repositories content. This team works in collaboration with upstream software maintainers, security experts, and the broader Docker community. These are not prefixed by an organization or user name. In the list of images above, the `python`, `node`, `alpine` and `nginx` images are official (base) images. To find out more about them, check out the [Official Images Documentation](https://docs.docker.com/docker-hub/official_repos/).

- **User images** are images created and shared by users like you. They build on base images and add additional functionality. Typically these are formatted as `user/image-name`. The `user` value in the image name is your Docker Store user or organization name.

### Step By Step Guide

1. Create a file called **Dockerfile** in your work directory, and add content to it as described below.

  ```
  # Simple Server with Docker

  # 1. Create your work directory
  mkdir -p /home/<username>/dev/simple_server
  cd /home/<username>/dev/simple_server
  # 2. Create a Dockerfile
  touch Dockerfile
  # 3. Edit the Dockerfile with your own commands. Example:
  vim Dockerfile
  ```

  We'll start by specifying our base image, using the `FROM` keyword:

  ```
  FROM ubuntu
  ```

2. We are going to define ENV vars. can be changed during the container execution (`run` command)
  ```
  ENV PORT 8080
  ENV WORKDIR /tmp/server
  ```

3. In our work folder, we are going to create an HTML file `index.html`

  ```
  <!doctype html>
  <html>
    <head>
      <title>This is my docker website!</title>
    </head>
    <body>
      <p>This is an example paragraph. Anything in the <strong>body</strong> tag will appear on the page, just like this <strong>p</strong> tag and its contents.</p>
    </body>
  </html>
  ```

4. We add the command to create a workdir in our Dockerfile:  

  ```
  RUN mkdir ${WORKDIR}
  ```

5. Now, we can copy the `index.html` from our host computer to the workdir in the container. Check out that workdir is an ENV var that can be changed during container execution.

  ```
  COPY index.html ${WORKDIR}
  ```

6. We are going to use Python `SimpleHTTPServer` as our server, so we need to install python:

  ```
  RUN apt-get install -y python
  ```

7. We also have to specify the port number which needs to be exposed. It is our other ENV vart:

  ```
  EXPOSE ${PORT}
  ```

8. The last step is the command for running the application. Use the [CMD](https://docs.docker.com/engine/reference/builder/#cmd) command to do that:

  ```
  CMD cd ${WORKDIR} && python -m SimpleHTTPServer ${PORT}
  ```

### Building it!

Now that you have your `Dockerfile`, you can build your image. The `docker build` command creates a docker image from a `Dockerfile`.

The `docker build` command is quite simple - it takes an optional tag name with the `-t` flag, and the location of the directory containing the `Dockerfile` - the `.` indicates the current directory:

```
sudo docker build -t simplehttpserver:latest .
```

>**Caution** Don't forget the dot to indicate the directory!

### Running it!

The next step in this section is to run the image and see if it actually works!

```
sudo docker run -p 80:8080 simplehttpserver:latest
```

##### CHALLENGE 4

Create your own website using Docker.

```
Following the previous steps and the docs, build your own Docker Image. Don't just copy the commands, try it in another language, or use nginx instead of python
```

A cool thing about Docker is that you only need a Dockerfile, and your code to recreate your image and run your container anywhere, this makes it perfect to store it in a repo, and much more easy to integrate with CI systems such as Jenkins

### Docker Registry

It's your own local Hub. You can run it using the following commands:

```
docker run -d -p 5000:5000 --name registry registry:2
```

#### Docker Naming
```
docker pull <my_registry_endpoint>:<your/docker/image/repo>:<version_tag>
```

Docker pulling and pushing example
```
docker run -d -p 5000:5000 --name registry registry:2
docker pull ubuntu
docker tag ubuntu localhost:5000/myfirstimage
docker push localhost:5000/myfirstimage
docker pull localhost:5000/myfirstimage
docker stop registry && docker rm -v registry
```

##### CHALLENGE 5
```
# Push your image from Challenge 4 to your local registry
```

## Docker Networking

* Bridge: All docker has its own IP  inside the Docker0 network (type `ifconfig -a` to check it out)
* Host: Containers and Host share the same network (Caution with the ports!)
* None: No network interface

```
# try this:
docker network create --driver bridge isolated_nw
docker network inspect isolated_nw
docker network ls


docker run --network=isolated_nw -itd --name=example busybox
```

##### CHALLENGE 6
```
# Run two containers in the same bridge network (a custom network made by you) and check if their IPs are in the same range (docker inspect command) Also, check the communication between containers is possible (for example with netcat, telnet or ping)
```

## Docker Compose

Compose is a tool for defining and running multi-container Docker applications.

[Docker Compose Docs](https://docs.docker.com/compose/overview/)
[Docker Compose Github]()

##### CHALLENGE 7

Install Docker Compose!

```
sudo su
sudo curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
$ docker-compose --version
docker-compose version 1.22.0, build 1719ceb
```

##### CHALLENGE 8

Get familiar with Docker and Docker Compose by doing the [Getting started Guide](https://docs.docker.com/compose/gettingstarted/)

##### CHALLENGE 9

Create your own Dockerized App (Can be a very simple http API) that depends on a database (MySQL, PostgreSQL, the one you like) if you don't have time you can use something that already exists, for example, Wordpress, then, create the Docker Compose that deploys both containers. You have succesfully created a microservice oriented architecture!

## Additional Contents

### Glossary of Terms

- *Images* - The file system and configuration of our application which are used to create containers. To find out more about a Docker image, run `docker inspect alpine`. In the demo above, you used the `docker pull` command to download the **ubuntu/zesty** image. When you executed the command `docker run hello-world`, it also did a `docker pull` behind the scenes to download the **hello-world** image.
- *Containers* - Running instances of Docker images &mdash; containers run the actual applications. A container includes an application and all of its dependencies. It shares the kernel with other containers, and runs as an isolated process in user space on the host OS. You created a container using `docker run` which you did using the alpine image that you downloaded. A list of running containers can be seen using the `docker ps` command.
- *Docker daemon* - The background service running on the host that manages building, running and distributing Docker containers.
- *Docker client* - The command line tool that allows the user to interact with the Docker daemon.

### Dockerfile commands summary

Here's a quick summary of the few basic commands we used in our Dockerfile.

* `FROM` starts the Dockerfile. It is a requirement that the Dockerfile must start with the `FROM` command. Images are created in layers, which means you can use another image as the base image for your own. The `FROM` command defines your base layer. As arguments, it takes the name of the image. Optionally, you can add the Docker Cloud username of the maintainer and image version, in the format `username/imagename:version`.

* `RUN` is used to build up the Image you're creating. For each `RUN` command, Docker will run the command then create a new layer of the image. This way you can roll back your image to previous states easily. The syntax for a `RUN` instruction is to place the full text of the shell command after the `RUN` (e.g., `RUN mkdir /user/local/foo`). This will automatically run in a `/bin/sh` shell. You can define a different shell like this: `RUN /bin/bash -c 'mkdir /user/local/foo'`

* `COPY` copies local files into the container.

* `CMD` defines the commands that will run on the Image at start-up. Unlike a `RUN`, this does not create a new layer for the Image, but simply runs the command. There can only be one `CMD` per a Dockerfile/Image. If you need to run multiple commands, the best way to do that is to have the `CMD` run a script. `CMD` requires that you tell it where to run the command, unlike `RUN`. So example `CMD` commands would be:

```
  CMD ["python", "./app.py"]

  CMD ["/bin/bash", "echo", "Hello World"]
```

* `EXPOSE` creates a hint for users of an image which ports provide services. It is included in the information which
 can be retrieved via `$ docker inspect <container-id>`.     

>**Note:** The `EXPOSE` command does not actually make any ports accessible to the host! Instead, this requires
publishing ports by means of the `-p` flag when using `$ docker run`.  

* `PUSH` pushes your image to Docker Cloud, or alternately to a [private registry](https://docs.docker.com/registry/)

>**Note:** If you want to learn more about Dockerfiles, check out [Best practices for writing Dockerfiles](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/).

### Docker CheatSheets

http://files.zeroturnaround.com/pdf/zt_docker_cheat_sheet.pdf

https://reinvent.awsevents.com/_media/docs/sponsors/gold/Docker-Inc_Commands-Cheat-Sheet.pdf
