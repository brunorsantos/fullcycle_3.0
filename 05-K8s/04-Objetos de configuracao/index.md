# Objetos de configuracao

## Variaveis de ambiente

É possivel definir nas especificacoes do um container variaveis de ambiente.

```
spec:
    containers:
    - name: goserver
        image: "brsds2000/hello-go:v4"
        env:
        - name: NAME 
            value: "Wesley"
        - name: AGE
            value: "36"
```


## ConfigMap

É um objeto que é utilizado como mapa de configuracoes da aplicacao

Definimos ele com `kind: ConfigMap`. E definimos os valores das configuracoes como no [exemplo](https://github.com/brunorsantos/fullcycle_3.0/blob/main/05-K8s/04-Objetos%20de%20configuracao/k8s/configmap-env.yaml)

E podemos definir os valores das variaveis de ambiente referenciando os valores do objeto. Como no [exemplo](https://github.com/brunorsantos/fullcycle_3.0/blob/main/05-K8s/04-Objetos%20de%20configuracao/k8s/deployment.yaml)


É possivel tambem utilizar todas as keys do configMap no seu pod ao inves de definir um por um. Como no [exemplo](https://github.com/brunorsantos/fullcycle_3.0/blob/main/05-K8s/04-Objetos%20de%20configuracao/k8s/deployment2.yaml)

Obs: Alterar o objeto de config map nao atualiza automaticamente os containers, para isso é necessario alterar diretamente a pod, ou deployment ou replicaset...

### Injeção do ConfigMap

Necessario quando queremos utilizar arquivos de configuracao. 
Podemos ter esse arquivo fisico injetando ele dentro do container.

Utilizando um configMap comum, podemos criar um volume com as keys desejadas dessse configMap e montar dentro do container do Pod.

Podemos criar esse volume por exemplo na cricao do deployment, sendo que esse volume poderá ser montado em todos os containers

Utilizando o configMap de [exemplo](https://github.com/brunorsantos/fullcycle_3.0/blob/main/05-K8s/04-Objetos%20de%20configuracao/k8s/configmap-family.yaml), podemos criar o deployment como o [exemplo](https://github.com/brunorsantos/fullcycle_3.0/blob/main/05-K8s/04-Objetos%20de%20configuracao/k8s/deployment03.yaml)

## Secret

É um objeto similar ao ConfigMap em que os valores das configs devem ser declaradas utilizando Base64, como o [exemplo](https://github.com/brunorsantos/fullcycle_3.0/blob/main/05-K8s/04-Objetos%20de%20configuracao/k8s/secret.yaml).

Ao utilizar nos conteineres é decodificado o Base64
E podemos utilizar com:

```
    spec:
      containers:
        - name: goserver
          image: "xxx/xx-xx:v5"
          envFrom:
            - secretRef:
                name: goserver-secret
```



Lembrando que a codificacao em base64 não serve como segurança adequada para as secrets

