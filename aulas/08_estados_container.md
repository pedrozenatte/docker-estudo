# Estados de um Container

Um container Docker passa por diferentes estados ao longo do seu ciclo de vida.  
Esses estados representam desde a criação até a execução, pausa e remoção.

---

## Estado de criação

O container é criado, mas ainda não está em execução.

- docker create -it ubuntu  

Nesse estado, o container já existe, porém ainda não iniciou seu processo principal.

A partir daqui, podemos:
- Iniciar o container (ir para running)
- Remover o container (delete)


#### Estado de execução (running)

O container está ativo e executando seu processo principal.

- docker start 'nome/id'  

OBS:  
O comando `docker run` já faz duas coisas automaticamente:
- Cria o container  
- Inicia o container  

Ou seja, ele passa direto pelos estados de criação → execução.

Também é possível reiniciar um container:

- docker restart 'nome/id'  



#### Estado de remoção (delete)

O container é completamente removido do sistema.

- docker rm 'nome/id'  

Após isso, ele deixa de existir e não pode ser reutilizado.

---

## A partir do estado de running

Quando o container está em execução, ele pode:

- Ser parado  (stop ou kill)
- Ser pausado  (pause)


#### Estado de parado (stop)

O container é encerrado de forma controlada, permitindo que os processos finalizem corretamente.

- docker stop 'nome/id'  


#### Estado de parado (kill)

O container é encerrado imediatamente, sem esperar os processos finalizarem.

- docker kill 'nome/id'  

OBS:  
- `stop` → parada segura (graceful shutdown)  
- `kill` → parada forçada (imediata)  


#### Estado de pausado (paused)

O container continua existente, mas sua execução é congelada.

- docker pause 'nome/id'  

Nesse estado:
- Os processos ficam congelados
- O container não consome CPU (ou consome muito pouco)
- A memória permanece alocada

---

## Diferença entre parado e pausado

- **Parado (stopped)**: o container é desligado. Ao iniciar novamente, o processo recomeça.  
- **Pausado (paused)**: o container é congelado. Ao retomar, ele continua exatamente de onde parou.  

---

## A partir do estado paused

O container pode apenas voltar à execução:

- docker unpause 'nome/id'  

---

## A partir do estado de parado

Um container parado pode:

#### Voltar a executar

- docker start 'nome/id'  


#### Ser removido

- docker rm 'nome/id'  

OBS:  
Para remover, o container precisa estar parado.

---

## Resumo do ciclo de vida

create → running → (paused / stopped) → running → stopped → delete

---

## Observação importante

Containers são projetados para serem **efêmeros**:
- Podem ser criados e destruídos rapidamente  
- Não são pensados para armazenar estado permanente (isso é feito com volumes)  