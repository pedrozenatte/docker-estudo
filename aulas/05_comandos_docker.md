# Comandos básicos do Docker

Aqui teremos comandos de aulas a frente, com o objetivo de manter todos os comandos unificados

---
1) Para verificar se o docker está rodando ou não (duas formas):
- sudo service docker status
- sudo systemctl status docker 

OBS: "service docker 'ação'" é a maneira antiga. Hoje, utiliza-se "systemctl 'ação' docker". 

---

2) Como iniciar o docker (caso esteja desligado):
- sudo systemctl start docker

---

3) Listar containers em execução (duas formas):
- docker ps 
- docker container ls

---

4) Verificar containers que estão parados, em stop (duas formas):
- docker ps -a 
- docker container ls -a

Pergunta: Para que serve um container parado? 
R: Reutilizar sem recriar tudo, ou seja, podemos simplesmente iniciar aquilo: docker start 'id_ou_nome'

---

5) Listar imagens que estão no repositório local:
- docker images

---

6) Excluir containers parados:
- docker rm 'ID do container' 
Ou 
- docker rm 'Nome do container'

OBS: Para pegar o nome do container ou id do container, precisa listar eles (comando 4).

---

6) Excluir imagens do repositório local:
- docker rmi 'Nome da imagem:latest'

OBS: latest é a TAG da imagem.

---

7) Como parar o docker: 
- sudo systemctl stop docker

---

8) Reiniciar o docker: 
- sudo systemctl restart docker

---

9) *Desabilitar na inicialização (boot):
- sudo systemctl disable docker

---

10) Excluir todos os containers (CUIDADO):
- docker container prune

---

11) Criar container e modo iterativo:
- docker run -it ubuntu

---

12) Transformar uma imagem: 
ATENÇÃO: Tudo que é feito dentro de um container fica salvo automaticamente, mesmo se ele parar. Porém, imagine que entramos no ubuntu (modo iterativo), instalamos python e saímos. Esse container está modificado, e podemos modificar essa imagem, de modo a 'criar' uma imagem nova, e com isso, ao instalar a imagem modificada do ubuntu, o python já vem instalado. 
- docker commit 'nome do container' 'nome da imagem'

OBS: O nome pode seguir esse formato --> nome:tag, como meu_ubuntu:v1

---

12) Voltar para um container: 
- docker start -ai 'nome ou id container'