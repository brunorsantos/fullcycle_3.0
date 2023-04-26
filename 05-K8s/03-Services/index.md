# Service

O objeto do tipo service, serão as portas de entrada para a aplicacao.

Ele quem irá decidir qual das pods serão acessados em uma determinada requisicao.
Existem alguns tipos de services que se diferenciam na maneira como eles disponibilizam as portas.

Aplicamos o service da mesma forma que os outros objetos `kubectl apply -f`

### Selector

Independente do tipo do service, eles utilizam um especificacao de selector, que consiste em como localizar as pods(podendo ser atraves do deployment).


Ex: Dado um selector especificado no deployment como:

```
spec:
  selector: 
    matchLabels:
      app: goserver 

```

O service localizara as pods criadas por ele utilizando um selector como:

```
spec:
  selector:
    app: goserver
```

### Ports

Definimos na especificacao de portas quais as portas do service estarão disponiveis para ser acessadas. Elas redirecionarão para outra porta dos Pods(targetPort).

```
  ports: 
  - name: goserver-service
    port: 80
    targetPort: 80
    protocol: TCP
```

O Valor do `targetPort` se nao definido será igual ao do `port`

## Service - ClusterIP

É diferenciado na spec como `type: ClusterIP`

Gera um service com um ip interno dentro do cluster para o serviço.

Apenas quem estiver dentro do cluster conseguirá acessar o service. O acesso pode ser pelo ip ou proprio nome do serviço

Exemplo em [service.yaml](https://github.com/brunorsantos/fullcycle_3.0/blob/main/05-K8s/03-services/k8s/service.yaml)

É possivel fazer um redirecionamento de portas para acessar de fora do cluster.

```
kubeclt port-forward svc/[nome do service] 8000:80
```

## Service - NodePort

É mais antigo e não muito utilizado. 

Nesse tipo, voce pode escolher uma porta (acima de 30000) que o servico vai expor essa porta em todos os seus nodes. Em que voce que pode acessar externamente via ip do node essa porta (acima 30000), havera um direcionamento para o porta definida do service.


## Service - LoadBalancer

Quando utilizado a aplicacao vai gerar um ip externo.

Porem para isto é necessario um cluster gerenciado(geralmente por provedor de nuvem). Que terá os drivers configurados para conseguir gerar um ip externo.


Exemplo em: [service_lb.yaml](https://github.com/brunorsantos/fullcycle_3.0/blob/main/05-K8s/03-services/k8s/service_lb.yaml)