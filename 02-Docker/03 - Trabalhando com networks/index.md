## Tipos de networks

- Bridge - Quando nao é informado esse é utilizado... Os containeres podem se enxergar

- Host - O container a maquina host podem se acessar, sem ter que fazer mapeamento de porta

- Overlay - 

- Macvlan

- None

## Bridge

Quando nao se cita rede o docker vai usar a rede com nome 'bridge' default. 
Sendo assim os container vao se enxergar utilizando ip.

---

É possivel criar uma rede propria com

```sh
docker network create --driver bridge [nome da rede]
```

E utilizar a rede ao inciar um container com `--network [nome da rede]`

```sh
docker run -it --name ubuntu1 --network [nome da rede] bash
```

Desta forma ao se utilizar uma rede propria é possivel um container enxergar o outro na rede utilizando o nome do container

## Host

So funciona no linux

## Acessando a marquina host

Basta utilizando dentro do container, `host.docker.internal`