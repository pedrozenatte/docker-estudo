# Comandos do Docker
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