# Variáveis de Ambiente no Docker

## O que são variáveis de ambiente?

Variáveis de ambiente são valores configuráveis disponíveis dentro do container e usados para definir ou influenciar o comportamento de programas e serviços.
Elas são muito úteis para passar configurações sem precisar alterar o código da aplicação.

Um exemplo clássico é:

```bash
ROS_MASTER_URI=http://192.168.0.102:11311
```

Nesse caso, essa variável informa ao ROS onde está o **master**.
Ou seja, em vez de deixar esse valor fixo no código, podemos defini-lo como variável de ambiente e mudar a configuração com mais facilidade.

## Principais formas de definir variáveis de ambiente no Docker

No Docker, existem duas formas principais de trabalhar com variáveis de ambiente:

- definir a variável dentro da imagem, usando `ENV` no Dockerfile;
- definir a variável ao executar o container, usando `-e` no comando `docker run`.

### 1. Definindo a variável dentro da imagem com `ENV`

Essa configuração é feita no Dockerfile.

Exemplo:

```bash
FROM ubuntu:20.04
ENV ROS_MASTER_URI=http://192.168.0.102:11311
```

#### O que isso significa?

Significa que, toda vez que um container for criado a partir dessa imagem, a variável `ROS_MASTER_URI` já estará definida automaticamente dentro dele.

Ou seja, ao executar:

```bash
docker run minha_imagem
```

a variável já existirá no ambiente interno do container.

#### Características do `ENV`

- a variável fica incorporada à imagem;
- ela passa a existir por padrão em todos os containers criados a partir dessa imagem;
- é útil quando queremos uma configuração padrão;
- não é a forma mais flexível quando precisamos mudar o valor com frequência.

### Testando dentro do container

Para verificar o valor da variável dentro do container, podemos usar:

```bash
echo $ROS_MASTER_URI
```

### 2. Definindo a variável ao rodar o container com `-e`

Outra forma é passar a variável no momento da execução do container.

Exemplo:

```bash
docker run -e ROS_MASTER_URI=http://192.168.0.102:11311 -it imagem
```

#### O que isso significa?

Nesse caso, a variável será definida apenas naquele container que está sendo criado naquele momento, ou seja, ela não fica gravada como padrão dentro da imagem. Ela vale apenas para a execução atual.


## Passando uma variável do sistema host para o container

Também é possível aproveitar uma variável que já existe na máquina host e repassá-la para o container.

Exemplo:

```bash
docker run -e ROS_MASTER_URI=$ROS_MASTER_URI -it imagem
```

Nesse caso:

- o Docker pega o valor da variável `ROS_MASTER_URI` do seu sistema;
- esse valor é enviado para dentro do container;
- a variável passa a existir lá com o mesmo conteúdo.

#### Exemplo completo

Primeiro, no host, definimos a variável:

```bash
export ROS_MASTER_URI=http://192.168.0.102:11311
```

Depois, executamos o container repassando esse valor:

```bash
docker run -e ROS_MASTER_URI=$ROS_MASTER_URI -it ubuntu bash
```

Dentro do container, podemos verificar com:

```bash
echo $ROS_MASTER_URI
```

O valor exibido será o mesmo que estava definido no host.
