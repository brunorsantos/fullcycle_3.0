## Stateless vs Stateless

Uma aplicacao Stateless é uma aplicacao que nao se preocupa em manter um estado (dados, sessao, etc).
Isto é a aplicacao em si nao salva nenhum dado que seja necessario para ser utiliza em uma futura requisicao por exemplo.
Enquanto em uma aplicacao Stateful, é necessario este salvamento.

## Volumes persistentes

Para utilizar volumes persistentes no k8s, atraves de pool de storage disponivel para o cluster. De maneira que os espacos sao disponibilidades para serem utilizados atravez do Claims.

O pool de storage por ser estatico ou dinamico. No modo estatico, previamente é criado um ou mais pool de storage com tamanhos definidos. Geramente é utilizado nos modelos On premisse

No modo dinamico(mais utilizado) são utilizados os `StorageClass`. É um especificação que faz com que exita um driver para que dinamicamente seja possivel provisionar espaco em disco para uma determinada aplicação.

Nesse caso, quando for feita uma claim para uma storageClass, ela ficará responsavel por gerenciar junto com o provedor de nuvem o espaço em disco

Podemos ver informações do StorageClass utilizando
```
kubectl get storageclass
```

Que sera exibido informações do storageClass especificas provedor de nuvem utilizado.



## Persitent volume claim

Ao criar um claim, seguindo o exemplo:


```yml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: goserver-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
```


Estamos solicitando para o storageClass (considerando que o mesmo existe) 5Gb de espaco.

Em accessModes está definido neste caso que o acesso a leitura só pode ser realizada por pods que estejam no mesmo node do persitent volume


Para fazer o bind desse Pvc, definimos no nivel do deployment(ou pod) o volume:

```yml
    volumes:
    - name: goserver-volume
        persistentVolumeClaim:
        claimName: goserver-pvc
```

E montamos o mesmo nos containers

```yml
        volumeMounts:
        - mountPath: "/go/pvc"
            name: goserver-volume
```

## Statefulset
