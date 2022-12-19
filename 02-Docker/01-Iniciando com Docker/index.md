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
```docker run <parametro> <image:tag> <comando>```

** Caso não seja informada uma tag, será considerada latest

** comando -> ex.:bash

Parâmetros:

**-it** -> atacha o terminal no container e permite interação 

exemplo:

```docker run -it ubuntu bash```

** Irá iniciar o container com a imagem Ubuntu do DockerHub e permitir iteração com o container através do bash. 

**-rm** -> remove o container do histórico após da sua finalização

**-d** -> não prende o terminal

**--name** > informa um nome para o container

**-p** -> faz o mapeamento de portas entre o host (nossa máquina) com o container  (p de publicação)

exemplo:

```docker run -p 8080:80 nginx```

** ao acessar a porta 8080 da máquina, é possível acessar a porta 80 do container

-------

```docker stop <nome ou id>```

** finaliza o container

-----

```docker rm <nome ou id>```

** remove o container já finalizado do histórico 

-----

```docker exec <nome ou id> <comando>```

** executa o comando no container que está up




