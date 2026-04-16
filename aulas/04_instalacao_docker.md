# Instalação do Docker - LINUX

## Instalação 

Para instalar, acesse o site da documentação oficial do docker: https://docs.docker.com/engine/install/ubuntu/

Quando for testar:
- sudo systemctl status docker
- sudo systemctl start docker
- sudo docker run hello-world

O comando de start docker pode não precisar, pois normalmente é inicializado com o SO normalmente, então ele vai subir junto com o sistema. 

## Retirar a necessidade de utilizar 'sudo' em tudo: 
1) 
    sudo groupadd docker
    sudo gpasswd -a $USER docker
    newgrp docker

Ou, de forma mais compacta:

2) 
    sudo usermod -aG docker $USER
    newgrp docker


## Visão da arquitetura do docker

O que acontece por trás dos panos quando rodamos o comando: 
- sudo docker run hello-world

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
4f55086f7dd0: Pull complete 
Digest: sha256:f9078146db2e05e794366b1bfe584a14ea6317f44027d10ef7dad65279026885
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/


A princípio, não temos a imagem hello-world, então ele mostra nos passos apresentados o que foi feito.
Portanto, foi rodado o comando no Cliente, o qual fez a comunicação com o Docker Daemon, e esse procurou a imagem localmente, não encontrou, e foi buscar no Registry, que por padrão está configurado para DockerHub. 