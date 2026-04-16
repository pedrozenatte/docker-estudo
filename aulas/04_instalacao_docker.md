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