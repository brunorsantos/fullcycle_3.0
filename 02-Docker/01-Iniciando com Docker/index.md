## Utilizando o Docker

----

```docker ps```

 Lista os containers em execução atualmente

 ----
 ```docker ps -a```

 Lista o histórico de containers

 ----

 ```docker run <image>```

Inicia o container da imagem 

** Caso o ENTRYPOINT definido não mantenha um processo em execução, o container morre após finalizar a operação

----
```docker run [parametro] [image:tag] [comando]```

** Caso não seja informada uma tag, será considerada latest

** comando -> ex.:bash

Parâmetros:

**-it** -> atacha o terminal no container e permite interação 

exemplo:

```docker run -it ubuntu bash```

** Irá iniciar o container com a imagem Ubuntu do DockerHub e permitir iteração com o container através do bash. 

**-rm** -> remove o container do histórico após da sua finalização

**-p** -> faz o mapeamento de portas entre o host (nossa máquina) com o container  (p de publicação)

exemplo:

```docker run -p 8080:80 nginx```

** ao acessar a porta 8080 da máquina, é possível acessar a porta 80 do container

**--name** -> informa um nome para o container

**-d** -> não prende o terminal

**-v [path do host]:[path container]** -> monta um volume (caso o path do host não exista, ele será criado)

**--mount type=bind,source=[path do host], target=[path do container]** -> monta um bind (caso o path não exista, haverá erro)

-------

```docker stop [nome ou id]```

** finaliza o container

-----

```docker rm [nome ou id]```

** remove o container já finalizado do histórico 

-----

```docker exec [nome ou id] [comando]```

** executa o comando no container que está up


## Trabalhando com volume

Quando mapeamos volumes utilizando -v + path estamos utilizando bind com tipo mount
É possivel utilizar bind com tipo volume. Em que esses volumes sao criados previamente.

```
docker volumes create [nome do volume]
```

Este modo possui a vantagem de criar volumes independente do container, podendo inclusive ser compartilhado entre conteinerers diferentes

Para criar o container utilizando o volume previamente criado

```
docker run --mount type=source=[nome do volume],target=[path no container] [imagem]
```

Pode ser tambem utilizar -v
```
docker run -v [nome do volume]:[path no container] [imagem]
```
Mais:

--- 
```
docker volume inspect [nome do volume]
```

Mostra detalhes do volume
