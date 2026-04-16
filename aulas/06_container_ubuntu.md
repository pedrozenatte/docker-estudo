# Container Ubuntu

##### Pode surgir um questionamento: quando executamos o container `hello-world`, ele roda e para. Então é assim que containers funcionam?

Sim, esse é o comportamento padrão.  
Um container executa um **processo principal** e, quando esse processo termina, o container é encerrado.

No caso do `hello-world`, ele apenas executa um comando que imprime uma mensagem na tela e finaliza.

##### Mas quem determina o funcionamento de um container?

Quem define isso é a **imagem do container**.

A imagem contém:
- Um sistema base (ex: Ubuntu)
- Bibliotecas e dependências
- Um comando padrão a ser executado

Ou seja, ela define **o que será executado quando o container iniciar**.

---

## Executando um container com a imagem do Ubuntu

#### 1) Rodar a imagem do Ubuntu

- docker run ubuntu  

OBS:  
O Docker primeiro procura a imagem localmente.  
Caso não encontre, ele baixa do Docker Hub.

Pergunta: "Mas não aconteceu nada?"  
Resposta: Sim — porque nenhum comando foi especificado.  
O container inicia e termina imediatamente.

---

#### 2) Executar um comando simples

- docker run ubuntu echo "Pedro Zenatte"  

---

#### 3) Listar diretórios

- docker run ubuntu ls  

---

##### Vamos executar comandos toda vez assim?

Não. Para isso existe o **modo interativo**, que permite trabalhar dentro do container.

---

### Modo interativo do Docker
O modo interativo do Docker (na prática, trabalhar com containers interativos) é quando você roda um container e interage com ele em tempo real, como se fosse um terminal de outro sistema.

Normalmente, containers são usados para rodar algo e terminar (ex: hello-world).
No modo interativo, podemos:

- entrar dentro do container
- executar comandos manualmente
- testar coisas passo a passo

OBS: Para sair, basta utilizar 'exit'

##### Comando
- docker run -i -t ubuntu
outra forma, flags juntas
- docker run -it ubuntu

Assim, podemos utilizar como se fosse literalmente um novo SO. 

OBS: As flags 
- -i: interactive
- -t: terminal
- -a: atach (conectar)

Assim, conseguimos utilizar o container como se fosse um ambiente isolado semelhante a um sistema operacional.

Importante:  
Apesar da aparência, o container **não é um sistema operacional completo**, pois compartilha o kernel do host.

---

### Nomeando um container

- docker run --name nome -it ubuntu  

---

### Executando em background

- docker run -d ubuntu  
- docker run -dit ubuntu  

OBS:  
`-d` (detached) executa o container em segundo plano, liberando o terminal imediatamente.