Exibe logs do pod:

```
kubectl logs [nome de pod]
```


Executa o bash dentro do container do pod:

```
kubeclt exect -it [nome do pod] -- bash
```

Aplica o deployment e acompanha os pods

```
kubectl apply -f k8s/deployment.yaml && watch -n1 kubectl get pods
```
