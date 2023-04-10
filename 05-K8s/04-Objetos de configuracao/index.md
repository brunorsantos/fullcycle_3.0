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

