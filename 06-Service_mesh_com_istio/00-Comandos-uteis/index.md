Loop fazendo requests:

```
while true;do curl http://localhost:8000; echo; sleep 0.5; done;

```


## Fortio (Testes de carga)


Aplica fortio

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.17/samples/httpbin/sample-client/fortio-deploy.yaml
```

Cria variavel de ambiente:

```
export FORTIO_POD=$(kubectl get pods -lapp=fortio -o 'jsonpath={.items[0].metadata.name}')
```

Cria um loop para fazer requests:

```
kubectl exec "$FORTIO_POD" -c fortio -- fortio load -c 2 -qps 0 -t 200s -loglevel Warning http://nginx-service:8000

```
