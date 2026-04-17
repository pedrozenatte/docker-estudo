# Criando as próprias imagens - Forma 1: `docker commit`

Até o momento, utilizamos imagens do Docker Hub, ou seja, imagens criadas e publicadas por outras pessoas. Porém, também é possível criar nossas próprias imagens a partir de uma imagem base já existente.

## O que as imagens vão ter?

As imagens Docker possuem uma sequência de passos que define como um container será montado e executado.

**Atenção:** cada passo realizado na construção da imagem corresponde a uma **camada**.

Isso é importante porque as imagens Docker são organizadas em camadas, o que facilita o reaproveitamento de partes já existentes e também ajuda no armazenamento.

## Como ver as camadas de uma imagem?

É possível visualizar o histórico de camadas de uma imagem com o comando:

- `docker history nome_da_imagem`

Esse comando permite enxergar como aquela imagem foi construída.

## Como criar uma imagem Docker?

De forma geral, uma imagem nova costuma ser criada a partir de uma imagem já existente, chamada de **imagem base**.
Essa imagem base normalmente contém o mínimo necessário para funcionamento, como:

- sistema operacional;
- bibliotecas essenciais;
- ferramentas básicas.

**É possível criar uma imagem do zero?**
Sim. Porém, isso costuma ser mais complexo e menos prático, principalmente no início.

Por isso, o mais comum é partir de uma imagem já pronta e personalizá-la.

## Criando uma imagem com `docker commit`

Uma maneira de criar uma nova imagem é iniciar um container a partir de uma imagem base, fazer alterações dentro dele e depois salvar esse estado em uma nova imagem com `docker commit`.

#### Exemplo

Deseja-se criar uma nova imagem chamada `ubuntu-potencializado` a partir da imagem `ubuntu`, contendo os pacotes:

- `curl`
- `vim`
- `iputils-ping`

Passo a passo:

- `docker run -it ubuntu`
- `apt update`
- `apt install curl vim iputils-ping -y`

Após isso, as modificações estarão instaladas **no container em execução**.

## Atenção: as mudanças ocorrem no container, não na imagem original

As imagens Docker são **read only**, ou seja, somente leitura.
Isso significa que a imagem original não é modificada diretamente. Quando criamos um container a partir de uma imagem, o Docker adiciona uma camada de escrita sobre ela. Sendo assim, todas as alterações feitas durante o uso ficam nesse container.

Portanto:

- a imagem original continua intacta;
- quem recebe as alterações é o container;
- para transformar essas alterações em uma nova imagem, usamos `docker commit`.

## Criando a nova imagem

Depois de fazer as alterações no container, basta executar:

- `docker commit nome_container nova_imagem:tag`

Exemplo:

- `docker commit meu_container ubuntu-potencializado:1.0`

Dessa forma, o Docker cria uma nova imagem com base no estado atual daquele container.

## O que acontece nas camadas dessa nova imagem?

Ao observar o histórico dessa nova imagem, normalmente aparece uma camada criada a partir de `/bin/bash`, pois foi dentro do shell do container que as alterações foram feitas manualmente.

O problema é que isso gera algumas desvantagens:

- não fica claro exatamente quais comandos foram executados;
- a camada criada funciona como uma espécie de “caixa-preta”;
- a imagem pode ocupar mais espaço do que o necessário;
- o processo fica pouco reproduzível.

Ou seja, alguém consegue ver que houve uma alteração, mas não consegue entender com facilidade tudo o que foi feito.

## Fazer um `commit` a cada alteração resolve?

Uma possível tentativa de melhorar isso seria fazer um `commit` a cada mudança importante.

Assim, em vez de concentrar tudo em uma única camada grande, haveria uma separação maior entre as alterações.

Mesmo assim, esse método continua sendo pouco prático, pois:

- ainda é manual;
- ainda é difícil de manter;
- ainda não documenta bem o processo;
- ainda não é a melhor opção para reproduzir a imagem no futuro.
