## Pod

Podemos criar um pod diretamente utilizando o `kubeclt` e arquivos yaml

Um aquivo de pod como o [pod.yml](https://github.com/brunorsantos/fullcycle_3.0/blob/main/05-K8s/02-Primeiros%20passos%20na%20pr%C3%A1tica/k8s/pod.yaml) terá o `kind: Pod` e as especificacoes que serão referentes ao container como o nome dele e a imagem da aplicacao. 

É possivel aplicar a pod com:

```
kubeclt apply -f k8s/pod.yml
```

E listar o pod criado com

```
kubeclt get pods
```

Uma possibilidade de acessar diretamente seu pod via http é redirecionando a porta com:

```
kubeclt port-forward pod/[nome do pod] [porta do host]:[porta do pod]
```

Criando dessa forma, caso o pod seja deletado, o mesmo nao sera recriado

Mostra mais informacoes da pod (como a tag da imagem sendo utilizada)

```
kubeclt describe pod [nome do pod]
```

## ReplicaSet

É o objeto que gerencia os pods e quantidade de replicas deles

Um arquivo de definicao de replicaSet como o [repiclaSet.yaml](https://github.com/brunorsantos/fullcycle_3.0/blob/main/05-K8s/02-Primeiros%20passos%20na%20pr%C3%A1tica/k8s/replicaset.yaml), conterá as especificacões do numero de replicas e o template da criacao do pod.

Aplicamos da mesma forma

```
kubeclt apply -f k8s/repicaSet.yaml
```
E listar a replicaSet criada com

```
kubeclt get replicasets
```

A replicaSet gerencia a quantidade de pods em execução para atingir a configuração definida, ou seja se um pod deixar de ser executado por algum motivo, o replicaSet automaticamente vai criar um novo.

Os pods criados pelo replicaSet terao um id acrescentado ao nome deles(definido no yaml)

O replicaSet não consegue manter o gerenciamento da modificacoes ou versao da pod.

Por exemplo, quando ha uma atualizacao da imagem da pod(aplicacao) e essa atualizacao é aplicada, os pods ja em execução nao serao atualizados automaticamente, a mudança so será refletida caso a pod seja deleta e recriada

## Deployment

O arquivo de deployment é bem similar ao arquivo do replicaSet, alterando o kind como o arquivo [deployment.yaml](https://github.com/brunorsantos/fullcycle_3.0/blob/main/05-K8s/02-Primeiros%20passos%20na%20pr%C3%A1tica/k8s/deployment.yaml)


Aplicamos da mesma forma

```
kubeclt apply -f k8s/deployment.yaml
```


Quando o deployment for aplicado ele criará um replicaSet que possuirá um id espefico. Na listagem dos pods (deste replicaSet) eles terao em seu nome o id do pod e do replicaSet.

Quando aplicamos novamente o deployment com uma alteracao de versao, os pods antigos serao removidos e os novos pods(de um novo replicaSet) serão criados

O replicaSet antigo continua existente porem com 0 pods associados. 

Sendo assim o deployment resolve a necessidade de manter uma versao de pods melhor gerenciada


O historico da versao do deployment pode ser acessado com:

```
kubeclt rollout history deployment [nome do deployment]
```

É possivel fazer o voltar a versao anterior com:

```
kubeclt rollout undo deployment [nome do deployment]
```

O comando funciona como se fizesse um apply na versao antiga do deployment