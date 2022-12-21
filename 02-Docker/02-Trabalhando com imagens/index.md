## Utilizando imagens


### Criação de imagem
```
docker build -t [tag] .
```
Cria a imagem a partir das definições do Dockerfile
O ponto (.) é o caminho para o arquivo - neste caso o diretório atual


### Dockerfile

``` Dockerfile
FROM nginx:latest
```
Define a imagem base 

``` Dockerfile
WORKDIR /the/workdir/path
```
Diretório que será usado dentro do container. Caso não exista, será criado e redirecionado


``` Dockerfile
RUN [comando] && [comando]
```

``` Dockerfile
COPY path/host /path/container
```


### CMD x ENTRYPOINT

Entrypoint é um comando fixo, enquanto cmd é um comando variável que entra como parâmetro para o entrypoint. 

Quando existe apenas o CMD, ele passa a ser um comando que pode ser substituído na hora de iniciar o container (docker run).

------
Dockerfile

```
CMD [ "echo", "Hello World"]
```

Execução

````
docker run --rm mb/hello
````

Saída

````
Hello World
````

-------

Dockerfile

```
CMD [ "echo", "Hello World"]
```

Execução

````
docker run --rm mb/hello echo oi
````

Saída

````
oi
````
------

Dockerfile

```
ENTRYPOINT [ "echo", "Hello"]
CMD [ "World"]
```

Execução

````
docker run --rm mb/hello 
````

Saída

````
Hello World
````

-------

Dockerfile

```
ENTRYPOINT [ "echo", "Hello"]
CMD [ "World"]
```

Execução

````
docker run --rm mb/hello mb 
````

Saída

````
Hello mb
````

