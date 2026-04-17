# Comandos básicos do Docker

Aqui teremos comandos de aulas a frente, com o objetivo de manter todos os comandos unificados

# Comandos básicos do Docker

Aqui reunimos os principais comandos do Docker, com o objetivo de manter tudo organizado em um único lugar para consulta rápida.

---

1) Para verificar se o Docker está rodando (duas formas):

- sudo systemctl status docker  
- sudo service docker status  

OBS: `service` é a forma antiga. Hoje, o padrão é usar `systemctl`.

---

2) Como iniciar o Docker (caso esteja desligado):

- sudo systemctl start docker  

Para criar e executar um container:

- docker run 'imagem'  

OBS: `docker run` cria e executa um container a partir de uma imagem.

---

3) Listar containers em execução (duas formas):

- docker ps  
- docker container ls  

---

4) Listar todos os containers (incluindo parados):

- docker ps -a  
- docker container ls -a  

OBS: Podemos verificar as camadas de read/write de um container com:
```bash
docker ps -a -s
```

Pergunta: Para que serve um container parado?  
R: Permite reutilizar o container sem precisar recriar tudo.

Para iniciar novamente:

- docker start 'id_ou_nome'  

---

5) Listar imagens locais:

- docker images  

---

6) Excluir containers:

- docker rm 'ID ou nome do container'  

OBS: O container precisa estar parado.  
Para forçar a remoção:

- docker rm -f 'ID ou nome'  

---

7) Excluir imagens:

- docker rmi 'nome:tag'  

Exemplo:

- docker rmi ubuntu:latest  

OBS: `latest` é a tag padrão da imagem.

---

8) Parar o Docker:

- sudo systemctl stop docker  

---

9) Reiniciar o Docker:

- sudo systemctl restart docker  

---

10) Desabilitar Docker na inicialização:

- sudo systemctl disable docker  

---

11) Excluir todos os containers parados (CUIDADO):

- docker container prune  

---

12) Criar container em modo interativo:

- docker run -it ubuntu  

Com nome específico:

- docker run --name 'nome' -it ubuntu  

OBS: A flag `-it` permite interação com o terminal.

---

13) Criar container em background:

- docker run -d ubuntu  
- docker run -dit ubuntu  

OBS: `-d` significa execução em segundo plano.

---

14) Parar um container:

- docker stop 'nome ou id'  

Parada imediata:

- docker stop -t 0 'nome/id'  

---

15) Parar e remover um container:

- docker rm -f 'nome/id'  

---

16) Voltar para um container:
**Parado:**
- docker start -ai 'nome ou id'  

OBS: `-a` conecta ao terminal, `-i` mantém interação.

**Rodando:**
Se o container está em segundo plano, para acessar ele no terminal e de forma interativa:
- docker exec -it nome bash

---

17) Criar uma nova imagem a partir de um container:

- docker commit 'nome_container' 'nova_imagem:tag'  

Exemplo:

- docker commit meu_container meu_ubuntu:v1  

OBS: Alterações feitas dentro de um container não alteram a imagem original automaticamente.  
Elas ficam salvas naquele container e só viram uma nova imagem com `commit`.
Imagine que entramos no ubuntu (modo iterativo), instalamos python e saímos. Esse container está modificado, e podemos modificar essa imagem, de modo a 'criar' uma imagem nova, e com isso, ao instalar a imagem modificada do ubuntu, o python já vem instalado.

---

18) Excluir várias imagens de uma vez:
- docker rmi $(docker images -q)

---

19) Executar um comando específico em um docker que está em segundo plano: 
- docker exec nome apt update

**Para saídas mais complexas:**
- docker exec -it nome apt update

---

20) Ver as camadas de uma imagem:
- docker history 'nome da imagem'

---

21) Construção de uma imagem a partir de um dockerfile
**Quando o arquivo se chama `Dockerfile`**
```bash
docker build -t minha_imagem:v1 
```

**Quando o arquivo possui outro nome, como `nome.dockerfile`**
```bash
docker build -t minha_imagem:v1 -f nome.dockerfile 
```

---

22) Inspecionar um Container: 
```bash
docker inspect 'nome/id'
```

---

## Observações gerais

- `run` → cria e executa container  
- `start` → inicia container parado  
- `stop` → para container  
- `rm` → remove container  
- `rmi` → remove imagem  
- `ps` → lista containers  


