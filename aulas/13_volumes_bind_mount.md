# Volumes e Bind Mount - Persistência de Dados

## O que são volumes e Bind Mount no Docker?

Volumes e Bind Mounts são mecanismos de persistência de dados no Docker. Eles permitem armazenar dados fora da camada de escrita do container, de modo que essas informações não sejam perdidas quando o container for removido.
Na prática, isso significa que o Docker pode manter os dados em uma área separada do container e disponibilizá-los novamente sempre que necessário.
Também é possível fazer a montagem de diretórios entre o Docker Host e o container, de forma que arquivos da máquina possam ser acessados dentro do container.

Em outras palavras, o volume é uma forma de desacoplar os dados da vida útil do container.

#### O que acontece quando removemos um container?

Quando um container é removido, sua camada de escrita também é removida.
Isso significa que tudo o que foi salvo apenas dentro do container, sem volume, é perdido.

Ou seja:

- dados criados somente na camada R/W do container são excluídos;
- arquivos persistidos em volumes continuam existindo;
- o container pode ser apagado sem necessariamente apagar os dados persistidos.

#### Por que usar volumes?

O uso de volumes é importante porque permite:

- persistir dados mesmo após a remoção do container;
- compartilhar arquivos entre host e container;
- separar aplicação e dados;
- facilitar backup, reutilização e manutenção.

## Como criar um volume com `-v`

Uma forma comum de utilizar volumes é com a flag `-v` no comando `docker run`.

Exemplo geral:

```bash
docker run -it -v origem:destino nome_da_imagem
```

Nesse comando:

- `origem` representa o local do dado que será persistido;
- `destino` representa o caminho dentro do container;
- `nome_da_imagem` é a imagem usada para criar o container.

OBS: Se a origem ou o destino não existirem, serão criados. 

#### Entendendo a montagem

Quando usamos `-v`, o Docker faz uma associação entre um diretório no host e um diretório dentro do container.
Assim, tudo o que for salvo nesse diretório montado poderá permanecer mesmo que o container seja encerrado ou removido, dependendo do tipo de montagem utilizada.

Isso permite, por exemplo:

- editar arquivos no host e visualizá-los no container;
- gerar arquivos dentro do container e acessá-los no host;
- manter dados importantes sem depender apenas da camada do container.

## Diferença entre volume e bind mount

Embora os dois sejam usados para persistir ou compartilhar dados, eles não são a mesma coisa.

### Volume

No **volume**, o armazenamento é **gerenciado pelo próprio Docker**. Dessa forma, os dados ficam em uma área controlada pelo Docker dentro do host, e não em uma pasta qualquer escolhida manualmente pelo usuário.

Exemplo:

```bash
docker run -it -v meu_volume:/dados ubuntu
```

Nesse caso:

- `meu_volume` é um volume gerenciado pelo Docker;
- `/dados` é o diretório dentro do container.

A principal característica é que o Docker administra onde esse volume fica salvo no host (ainda assim está na máquina, mas a pasta fica como se fosse 'oculta').

OBS: Também podemos criar um volume diretamente com:
```bash
docker volume create 'nome_volume'
```

#### Como acessar um volume no host?

Como o volume é gerenciado pelo Docker, normalmente ele não fica em um caminho que escolhemos manualmente.

Para descobrir onde ele está armazenado, podemos usar:

```bash
docker volume inspect meu_volume
```

Esse comando mostra informações do volume, inclusive o caminho físico no host onde os dados estão salvos. 
Além disso, para acessar o caminho físico, precisa de permissão de super usuário (sudo)

Também é possível listar os volumes existentes com:

```bash
docker volume ls
```

Volumes são mais organizados e mais portáveis para uso com containers, sendo bastante indicados para bancos de dados, dados persistentes de aplicações e situações em que não queremos depender de uma pasta específica do sistema.

### Bind mount

No **bind mount**, quem define a origem dos dados é o usuário, ou seja, escolhemos explicitamente uma pasta ou arquivo da máquina host para ser montado dentro do container.

#### Exemplo conceitual

Suponha que desejamos montar uma pasta da máquina dentro do container. A estrutura seria assim:

```bash
docker run -it -v /pasta/no/host:/pasta/no/container nome_da_imagem
```

Nesse caso:

- `/pasta/no/host` é o diretório da máquina;
- `/pasta/no/container` é o diretório visível dentro do container.

Tudo o que estiver sincronizado nesse caminho poderá ser acessado dos dois lados.

A principal característica do bind mount é que ele aponta diretamente para um caminho já existente ou escolhido no host.

Isso é muito útil quando queremos:

- editar arquivos do projeto no host e enxergá-los imediatamente no container;
- desenvolver código localmente usando ferramentas instaladas no container;
- compartilhar arquivos específicos da máquina com o container.

## Resumindo a diferença

#### Volume

- é gerenciado pelo Docker;
- o Docker decide onde ele fica salvo no host;
- é mais desacoplado da estrutura de pastas do sistema;
- costuma ser mais indicado para persistência de dados da aplicação.

#### Bind mount

- é gerenciado pelo usuário;
- o usuário escolhe o caminho exato no host;
- depende diretamente da estrutura de diretórios da máquina;
- costuma ser mais indicado para desenvolvimento e compartilhamento direto de arquivos.

### Exemplos comparando os dois

#### Exemplo com volume

```bash
docker run -it -v dados_app:/var/lib/app ubuntu
```

Aqui, `dados_app` é um volume controlado pelo Docker.

#### Exemplo com bind mount

```bash
docker run -it -v /home/usuario/app:/var/lib/app ubuntu
```

Aqui, `/home/usuario/app` é uma pasta real da máquina host.


### PORTANTO, atenção ao uso da flag `-v`

A flag `-v` pode ser usada em diferentes contextos, mas é importante lembrar que ela trabalha com o mapeamento entre uma origem e um destino, e a forma como é feita é escrita a origem determina se é volume ou bind mount.


## Observações

Volumes são a principal forma de persistir dados no Docker. Sem eles, os arquivos gravados apenas dentro do container são perdidos quando o container é removido.
Por isso, sempre que houver dados importantes, bancos, arquivos de configuração, logs ou qualquer conteúdo que precise continuar existindo, o ideal é utilizar volumes.