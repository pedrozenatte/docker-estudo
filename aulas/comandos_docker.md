# Comandos básicos do Docker

Aqui reunimos os principais comandos do Docker, com o objetivo de manter tudo organizado em um único lugar para consulta rápida.

---

1) Para verificar se o Docker está rodando (duas formas):

```bash
sudo systemctl status docker
```  

```bash
sudo service docker status 
``` 

OBS: `service` é a forma antiga. Hoje, o padrão é usar `systemctl`.

---

2) Como iniciar o Docker (caso esteja desligado):

```bash
sudo systemctl start docker  
```

Para criar e executar um container:

```bash
docker run 'imagem'  
```

OBS: `docker run` cria e executa um container a partir de uma imagem.

---

3) Listar containers em execução (duas formas):

```bash
docker ps  
```
Ou
```bash
docker container ls  
```

---

4) Listar todos os containers (incluindo parados):

```bash
- docker ps -a  
```
Ou
```bash
- docker container ls -a  
```

OBS: Podemos verificar as camadas de read/write de um container com:
```bash
docker ps -a -s
```

Pergunta: Para que serve um container parado?  
R: Permite reutilizar o container sem precisar recriar tudo.

Para iniciar novamente:

```bash
docker start 'id_ou_nome'  
```

---

5) Listar imagens locais:

```bash
docker images  
```

---

6) Excluir containers:

```bash
docker rm 'ID ou nome do container'  
```

OBS: O container precisa estar parado.  
Para forçar a remoção:

```bash
- docker rm -f 'ID ou nome'  
```

---

7) Excluir imagens:

```bash
docker rmi 'nome:tag'  
```

Exemplo:

```bash
docker rmi ubuntu:latest  
```

OBS: `latest` é a tag padrão da imagem.

---

8) Parar o Docker:

```bash
sudo systemctl stop docker  
```

---

9) Reiniciar o Docker:

```bash
sudo systemctl restart docker  
```

---

10) Desabilitar Docker na inicialização:

```bash
sudo systemctl disable docker  
```

---

11) Excluir todos os containers parados (CUIDADO):

```bash
docker container prune  
```

---

12) Criar container em modo interativo:

```bash
docker run -it ubuntu  
```

Com nome específico:

```bash
docker run --name 'nome' -it ubuntu  
```

OBS: A flag `-it` permite interação com o terminal.

---

13) Criar container em background:

```bash
docker run -d ubuntu  
```

```bash
docker run -dit ubuntu  
```

OBS: `-d` significa execução em segundo plano.

---

14) Parar um container:

```bash
docker stop 'nome ou id'  
```

Parada com tempo:

```bash
docker stop -t 0 'nome/id'  
```

---

15) Parar e remover um container:

```bash
docker rm -f 'nome/id'  
```

---

16) Voltar para um container:
**Parado:**
```bash
docker start -ai 'nome ou id'  
```

OBS: `-a` conecta ao terminal, `-i` mantém interação.

**Rodando:**
Se o container está em segundo plano, para acessar ele no terminal e de forma interativa:
```bash
docker exec -it nome bash
```

---

17) Criar uma nova imagem a partir de um container:
```bash
docker commit 'nome_container' 'nova_imagem:tag'  
```

Exemplo:
```bash
docker commit meu_container meu_ubuntu:v1  
```

OBS: Alterações feitas dentro de um container não alteram a imagem original automaticamente.  
Elas ficam salvas naquele container e só viram uma nova imagem com `commit`.
Imagine que entramos no ubuntu (modo iterativo), instalamos python e saímos. Esse container está modificado, e podemos modificar essa imagem, de modo a 'criar' uma imagem nova, e com isso, ao instalar a imagem modificada do ubuntu, o python já vem instalado.

---

18) Excluir várias imagens de uma vez:
```bash
docker rmi $(docker images -q)
```

---

19) Executar um comando específico em um docker que está em segundo plano: 
```bash
docker exec nome apt update
```

**Para saídas mais complexas:**
```bash
docker exec -it nome apt update
```

---

20) Ver as camadas de uma imagem:
```bash
docker history 'nome da imagem'
```

---

21) Construção de uma imagem a partir de um dockerfile:
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

23) Como criar volumes/bind mount ligando com uma pasta do container:
**Volumes**
```bash
docker run -it -v meu_volume:/dados ubuntu
```

**Bind Mount**
```bash
docker run -it -v /pasta/no/host:/pasta/no/container nome_da_imagem
```

OBS: Perceba que se a origem for um caminho, então é bind mount, se for só um nome, é um volume.

---

24) Como criar volumes:
```bash
docker volume create 'nome_volume'
```

OBS: Isso apenas cria o volume

25) Excluir volume:
```bash
docker volume rm 'nome_volume'
```

26) Inspecionar um volume:
```bash
docker volume inspect meu_volume
```

27) Listar volumes:
```bash
docker volume ls
```

28) Criar uma montagem `TMPFS`: 
```bash
docker run -it --tmpfs=/nome-do-diretorio nome_da_imagem
```

## Observações gerais

- `run` → cria e executa container  
- `start` → inicia container parado  
- `stop` → para container  
- `rm` → remove container  
- `rmi` → remove imagem  
- `ps` → lista containers  


