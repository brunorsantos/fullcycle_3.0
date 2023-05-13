# Gateway

Gerencia a entrada e saída do trafego. Trabalha no layers 4-6, garantindo o gerenciamento de portas, host e TLS. É conectado diretamente a um Virtual service que será responsavel pelo roteamento

# Virtual Service

Permite voce configurar como a requisiçoes serao roteadas para um serviço. Ela possui uma série de regras que quando aplicadas farão com que a requisição seja direcionada ao destino correto.

- roteamento de trafego
- Subsets
- Fault injection
- Retries
- Timeout

# Destination rules

A destination rule é usada para configurar o que acontece com o trafego quando ele chega naquele destino

# Criando gerenciamento de trafego

Utilizando no istio, o virtual service juntamente com a destination rule. 

```yml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: nginx-vs 
spec:
  hosts: 
  - nginx-service
  http:
    - route: 
      - destination: 
          host: nginx-service 
          subset: v1 
        weight: 90
      - destination: 
          host: nginx-service 
          subset: v2 
        weight: 10
```

Em que o virtual service vinculado ao service de nome `nginx-service` tera 2 possiveis roteamentos com pesos diferentes para subsets diferentes

```yml
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: nginx-dr 
spec:
  host: nginx-service
  subsets:
    - name: v1 
      labels:
        version: A
    - name: v2 
      labels:
        version: B
```

O que os subsets fazem são definidos no especificacao do DestinationRule vinculando o name do subsets com a version das pods definida na deployment.

É possivel definir no destinationRule uma traffic policy (algoritmo utilizado pelo load balancer) tanto nas especificacao geral(logo será utilizado por todos os subsets) ou individualmente em um subset.

```yml
trafficPolicy:
    loadBalancer:
        simple: LEAST_CONN
```

## Stick Session

Garante que um usuario que usou uma versao(de teste AB por exmeplo) continue utilze a mesma versão nas proximas requisiçoes

### Consistent Hash

O istio a partir de um cookie definido, header, ip ou queryString, gera um hash que a partir dele ele direcionara sempre para o mesmo local a partir desse hash

(Ainda nao funciona com pesos)

Exemplo em: [consistent-hash.yaml](consistent-hash.yaml)



## Fault injection

É possivel adicionar uma falha, utilizando uma rota do do virtualService por exemplo

```yml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: nginx-vs 
spec:
  hosts: 
  - nginx-service
  http:
    - fault:
        # delay:
        #   fixedDelay: 10s
        #   percentage:
        #     value: 100
        abort:
          httpStatus: 500
          percentage:
            value: 100
      route: 
      - destination: 
          host: nginx-service 
          subset: all 
```


## Circuit breaker

É definido na DestinationRule

```yml
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: circuit-breaker-servicex
spec:
  host: servicex-service.default.svc.cluster.local
  trafficPolicy:
    outlierDetection:
      # consecutive5xxErrors: 20
      consecutiveGatewayErrors: 10
      interval: 20s
      baseEjectionTime: 30s
      maxEjectionPercent: 100
```

## Gateway

Acessando servicos externamente batendo diretamente no service (acessando pela maquine por exemplo). O controle de tragego do istio nao funcionará, pois esse acesso nao possui um sidecar proxy para respeitar as rules do VirtualService e do destinationRule.

Para resolver isso precisamos ter um gateway, que terá um proxy.
