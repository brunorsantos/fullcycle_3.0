## Resources

Podemos definir na criacao do container da pod, os recursos que ela vai consumir.

Utilizando a tag `resources` podemos definir tanto os recursos minimos necessarios, quando os limites que podem ser alcançados pelo container.



```
resources:
    requests:
        cpu: 100m
        memory: 20Mi
    limits:
        cpu: 500m // ou "0.5"
        memory: 25Mi
```

- requests: define os recursos minimos para que o recurso seja provisionado. Enquanto estes recursos nao estiverem disponiveis no cluster o provisionamento ficará pendente.

- limits: define os limites maximos que o container pode utilizar. Uma boa pratica é que a soma de limite maximos de todos conteiners não ultrapasse o total do cluster.

Para verificar o consumo de cpu e memoria:

kubectl top pod [nome da pod]


## HPA

O Horizontal Pod Autoscaler, é um objeto que gerencia o deployment controlando a quantidade de replicas das pods do mesmo a partir da quantidade de recursos.


```yml
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: goserver-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: goserver
  minReplicas: 1
  maxReplicas: 5
  targetCPUUtilizationPercentage: 25
```

No exemplo acima, vemos que configuramos o target do do hpa atraves do nome do deployment. 
Em que configuramos um minimo e maximo de replicas de pods desde deployment desejado.
Tambem definimos um valor de media de utilizacao de CPU da pods em execução no momento para fazer um scaling ou downscaling. Sendo que o esse valor pode ser de memoria ou alguma metrica personalizada.