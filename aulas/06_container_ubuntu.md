# Container Ubuntu

##### Pode surgir um questionamento: Quando executamos o container hello-world, ele rodou e parou, logo, é assim que o container funciona? 
Na realidade os containers executam o que tem que executar e depois eles morrem. No caso do hello-world, ele apenas mostrou isso na tela.

##### Mas quem determina o funcionamento de um container? 
São as imagens de um container, a qual possui um passo a passo do que será executado.

## Vamos executar um container que possui a imagem de um SO.
#### Comandos
1) Rodar a imagem do ubuntu (inicialmente ele procura no repositório local, senão busca no dockerhub)
- docker run ubuntu

OBS: Ue, mas não aconteceu nada. 
Exatamente, pois não pedimos para o ubuntu fazer nada. 

2) Escrever na tela: 
docker run ubuntu echo "Pedro Zenatte"

3) Listar diretórios:
docker run ubuntu ls

##### Mas vamos executar comando a comando TODAS as vezes? 
NÃO, podemos utilizar o modo iterativo

## Modo iterativo do Docker
O modo iterativo do Docker (na prática, trabalhar com containers interativos) é quando você roda um container e interage com ele em tempo real, como se fosse um terminal de outro sistema.

Normalmente, containers são usados para rodar algo e terminar (ex: hello-world).
No modo iterativo/interativo, podemos:

- entrar dentro do container
- executar comandos manualmente
- testar coisas passo a passo

OBS: Para sair, basta utilizar 'exit'

##### Comando
- docker run -i -t ubuntu
outra forma, flags juntas
- docker run -it ubuntu

Assim, podemos utilizar como se fosse literalmente um novo SO. 

