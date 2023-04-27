# Ingress

A ideia do ingress é ser um ponto unico de entrada para o cluster k8s.
Isto é, caso tenhamos varias aplicacoes deployadas dentro do cluster, nao utilizaremos um service como loadbalancer para cada uma delas, causando custo extra. O ingress será responsavel de fazer o roteamento para o serviço

Ele pode ser instalado no cluster seguindo as instrucoes em [NGINX ingress controller](https://kubernetes.github.io/ingress-nginx/deploy/)

Apos a instalacao será criado um novo service de ingress controller do tipo loadbalancer, que terá um IP externo(Esse ip externo pode ser configurado no servidor de DNS)

O arquivo do ingress é definido da seguinte forma:

```yml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress 
metadata:
  name: ingress-host
  annotations:
    kubernetes.io/ingress.class: "nginx"
spec:
  rules:
  - host: "ingress.fullcycle.com.br"
    http:
      paths:
      - pathType: Prefix
        path: "/"
        backend:
          serviceName: goserver-service
          servicePort: 80
```

- annotations: Qual a base de configuracao sera utilizada para o ingress

- host: qual o DNS está onfigurado para ser o host de acesso ao cluster

É possivel criar por exemplo regras a partir de prefixo do dns redirecionado a requisicoes para outros services. Ex: `goserver-service` na porta 80.

Sendo assim os outros services nao precisam ter ip externo, apenas o ingress controller

