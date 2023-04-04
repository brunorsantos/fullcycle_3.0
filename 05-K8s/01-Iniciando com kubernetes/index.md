# K8s

É um orquestrador de containers. 
Veio do google de um projeto interno chamado borg


## Conceitos

É disponibilizado atraves de um conjunto de apis, principalmente com o uso do `kubectl`. 
Tudo é baseado em estado, o que fazemos é configurar o estado dos objetos.

Ex: Alterando arquivos Yaml que representam o estado, e depois aplicando esse aquivo usando o kubeclt.

- Cluster é um conjunto de maquinas(nós), sendo que cada maquina possui uma quantidade de cpu e memoria

- O Cluster sempre tera um nó master, que controla o que os outros nós vao fazer

- Dentro de um nó vamos ter as pods, que sao onde estará os containers em execucao(geralmente um só)

- Deployment tem o objetivo de provisionar os pods com configuracoes. Ex: quantas replicas (baseado em replicaSets) são necessarias. Pode ocorrer por exemplo de um deployment ter pods em diferentes nós dependendo de recursos disponiveis (memoria, cpu)



## Kind

[kind ](https://kind.sigs.k8s.io/) é uma ferramenta para utilizar localmente um cluster k8s rodando conteineres docker.

É possivel por exemplo configurar diversos nós

Para criar um cluster podemos utilizar

```
kind create cluster
```

Que criaria um cluster padrao com um node.

Apos a criacao, para utilizar (conectar) o cluster podemos utilizar

```
kubeclt cluster-info --context kind-kind
```

Para listar os cluster do kind usamos

```
kind get clusters
```

Para deletar

```
kind delete clusters [nome do cluster]
```

É possivel criar um yaml com a definição de como será o cluster a ser criado pelo kind. Por [exemplo](https://github.com/brunorsantos/fullcycle_3.0/blob/main/05-K8s/01-Iniciando%20com%20kubernetes/kind.yaml) configuarando mais de um node

E criar o cluster nele com:

```
kind create cluster --config=path_to.yml --name=nome
```

## Kubectl

É necessario instalar o kubeclt para se comunicar com o cluster

Utilizamos o kubeclt atraves de contextos para acessar o cluster. Ele mantem um arquivo com todos os contextos configurados (em ~/.kube/config).

Sendo assim sempre teremos um contexto selecionado em que ao utilizar o comando `kubeclt` estaremos nos refererindo a ele.


Para listar os contextos configurados:

```
kubectl config get-contexts    
```

Para listar os clusters configurados:

```
kubectl config get-clusters    
```

Para listar os nodes do cluster atual

```
kubeclt get nodes
```

Para alterar o contexto atual

```
kubectl config use-context [nome do contexto]
```




