# Docker Stop/Start vs Docker Pause/Unpause

Neste exemplo, vamos comparar os comportamentos de:
- `docker stop/start`
- `docker pause/unpause`

usando um container real com carga de CPU/memória.

---

1) Criando um container que “dorme” por 1 dia

    - docker run -dit --name teste ubuntu sleep 86400

2) Entrando no container
    - docker exec -it teste bash

3) Gerando carga de 1GB por 500s
    - apt update
    - apt install -y stress
    - stress --vm 1 --timeout 500

4) Saindo do container sem parar ele
Pressione:

    - CTRL + P
    depois
    - CTRL + Q

5) Verificar os processos dentro do container
    - docker exec -it teste top

---

## Caso 1) — Docker pause
- docker pause teste

**O que acontece:**
- O container é congelado
- Os processos são pausados (freezing)
- CPU cai praticamente para 0%
- Memória continua alocada

Retomar: 
- docker unpause teste

O processo continua exatamente de onde parou

---

## Caso 2) Docker stop
- docker stop teste

O que acontece:
- O container é encerrado
- Todos os processos são finalizados
- Memória é liberada
- CPU vai para 0%

Retomar:
- docker start teste

O container reinicia do zero
O comando stress NÃO continua