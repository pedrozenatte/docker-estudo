# Criando imagens com Dockerfile

## O que é um Dockerfile?

Um **Dockerfile** é um arquivo de texto que descreve, passo a passo, como uma imagem Docker deve ser construída. Nele, são definidas a imagem base, os comandos que devem ser executados, os pacotes que devem ser instalados e outras configurações necessárias para gerar a imagem final.

Esse arquivo pode ser criado de duas formas:

- com o nome `Dockerfile`
- com um nome personalizado, como `nome.dockerfile`

**Observação:** o formato `nome.dockerfile` é bastante utilizado em projetos que possuem mais de uma imagem, pois ajuda a organizar melhor os arquivos.

O uso de Dockerfile traz várias vantagens, como:

- mais praticidade na criação de imagens;
- controle de versão;
- facilidade de colaboração;
- maior legibilidade;
- possibilidade de recriar a imagem sempre da mesma forma.

## Como criar uma imagem com Dockerfile?

### Primeiro passo: criar o arquivo Dockerfile

Na raiz do projeto, crie um arquivo de texto chamado `Dockerfile` ou outro arquivo com extensão `.dockerfile`.

A estrutura mais básica é a seguinte:

```bash
FROM imagem_base:versao

# Comentários são feitos com #
# Se a versão não for informada, o Docker usa por padrão a tag latest.
# Porém, não é recomendado depender de latest,
# pois ela pode mudar com o tempo.

RUN comando
```

#### Explicando os principais comandos

- `FROM` define a imagem base que será usada para construir a nova imagem.
- `RUN` executa comandos durante o processo de build da imagem.
- `#` é usado para comentários.

##### Exemplo simples

Vamos criar uma imagem Docker a partir do Ubuntu 18.04 e instalar alguns pacotes.

```bash
FROM ubuntu:18.04

RUN apt-get -y update
RUN apt-get -y upgrade

RUN apt-get install -y python3.7-dev
```

#### Explicação do exemplo

No código acima, a linha:

```bash
FROM ubuntu:18.04
```

indica que a imagem base será a imagem `ubuntu` na versão `18.04`.

Assim, os nomes das imagens normalmente seguem a estrutura:

```bash
NOME:VERSAO
```

No caso, temos:

- `ubuntu` como nome da imagem;
- `18.04` como versão.

Já o comando `RUN` serve para executar instruções dentro da imagem durante sua construção, como se estivéssemos rodando comandos no terminal.

Portanto, na linha:

```bash
RUN apt-get -y update
```

o Docker executará:

```bash
apt-get -y update
```

Na linha:

```bash
RUN apt-get -y upgrade
```

o Docker executará:

```bash
apt-get -y upgrade
```

E na linha:

```bash
RUN apt-get install -y python3.7-dev
```

o Docker executará:

```bash
apt-get install -y python3.7-dev
```

Ou seja, cada instrução `RUN` cria uma nova camada na imagem e registra aquela etapa da construção.

### Segundo passo: construir a imagem

Depois de criar o Dockerfile com as instruções da imagem, é preciso entrar no diretório onde ele está salvo e executar o comando de build.

##### Quando o arquivo se chama `Dockerfile`

```bash
docker build -t minha_imagem:v1 
```

##### Quando o arquivo possui outro nome, como `nome.dockerfile`

```bash
docker build -t minha_imagem:v1 -f nome.dockerfile 
```

#### Explicando o comando `docker build`

- `docker build` inicia a construção da imagem;
- `-t` define o nome e a tag da imagem;
- `minha_imagem:v1` significa:
  - `minha_imagem` = nome da imagem;
  - `v1` = versão da imagem;
- `-f` é usado para indicar qual arquivo Dockerfile deve ser utilizado, caso ele não se chame exatamente `Dockerfile`.

### Observação sobre a tag `latest`

Se nenhuma tag for informada, o Docker pode considerar `latest` como padrão. Porém, isso não é o mais indicado, porque a versão `latest` pode mudar ao longo do tempo e comprometer a reprodutibilidade do projeto.
Por isso, o ideal é sempre informar explicitamente a versão da imagem base e também a tag da imagem que você está criando.

### Observações finais
O Dockerfile é a forma mais recomendada de criar imagens Docker, pois permite registrar todas as etapas da construção de forma clara, organizada e reproduzível.
Diferente do `docker commit`, ele facilita manutenção, versionamento e colaboração, além de deixar explícito tudo o que foi feito para gerar a imagem.