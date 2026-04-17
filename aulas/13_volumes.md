# Volumes - Persistência de Dados

## O que são volumes no Docker?

Volumes são mecanismos de persistência de dados no Docker. Eles permitem armazenar dados fora da camada de escrita do container, de modo que essas informações não sejam perdidas quando o container for removido.
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

#### Entendendo a montagem

Quando usamos `-v`, o Docker faz uma associação entre um diretório no host e um diretório dentro do container.
Assim, tudo o que for salvo nesse diretório montado poderá permanecer mesmo que o container seja encerrado ou removido, dependendo do tipo de montagem utilizada.

Isso permite, por exemplo:

- editar arquivos no host e visualizá-los no container;
- gerar arquivos dentro do container e acessá-los no host;
- manter dados importantes sem depender apenas da camada do container.

#### Exemplo conceitual

Suponha que desejamos montar uma pasta da máquina dentro do container. A estrutura seria assim:

```bash
docker run -it -v /pasta/no/host:/pasta/no/container nome_da_imagem
```

Nesse caso:

- `/pasta/no/host` é o diretório da máquina;
- `/pasta/no/container` é o diretório visível dentro do container.

Tudo o que estiver sincronizado nesse caminho poderá ser acessado dos dois lados.

#### Atenção ao uso da flag `-v`

A flag `-v` pode ser usada em diferentes contextos, mas é importante lembrar que ela trabalha com o mapeamento entre uma origem e um destino.
Por isso, escrever apenas um diretório isolado pode não deixar claro se se trata de um volume nomeado ou de um bind mount.

A forma mais didática para entender a persistência costuma ser:

```bash
docker run -it -v caminho_no_host:caminho_no_container nome_da_imagem
```

## Observações

Volumes são a principal forma de persistir dados no Docker. Sem eles, os arquivos gravados apenas dentro do container são perdidos quando o container é removido.
Por isso, sempre que houver dados importantes, bancos, arquivos de configuração, logs ou qualquer conteúdo que precise continuar existindo, o ideal é utilizar volumes.