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

O statefulset funciona como o deployment.
Porem as pods que ele cria ele sao no formato [nome do deployment]-0. Em que o 0 é relativo a ordem de criacao dos mesmos.

Por padrao cada pod é iniciado e terminado um a um individualmente e ordenadamente

```yml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mysql
spec:
  serviceName: mysql-h
  replicas: 3
  selector: 
      matchLabels:
        app: mysql
  template:
    metadata:
      labels:
        app: mysql 
    spec:
      containers:
        - name: mysql 
          image: mysql 
          env:
            - name: MYSQL_ROOT_PASSWORD
              value: root 
```

Esse funcionamento é util no caso de utilizacao de volumes nas pods, para as situações em que pode ser necessario controlar replicas de disco a partir da pod criada anteriormente. Isto é o controle de ordem de criacao e remocao das pods é necessario ser feito de forma ordenada.

## Headless service

Outra necessidade especifica que pode ser necessaria para trabalhar com pods que utilizam disco, é acessar um pod diretamente (Exemplo: Um dos discos vc tem acesso de leitura)

Para possibilitar isso podemos utilizar Headless service. Que é um service comum sem um IP, em que automaticamente ele criará um DNS para cada pod do statefulset

Podemos criar um headless service assim:

```yml
apiVersion: v1
kind: Service
metadata:
  name: mysql-h
spec:
  selector:
    app: mysql
  ports: 
  - port: 3306
  clusterIP: None

```

O nome do service deve ser o mesmo utilizado no statefulset em `serviceName`. Em que aplicando o service, será possivel acessar especificamente uma pod utilizando o DNS: mysql-0.mysql-h (Para acessar o pod mysql-0).

## Criando volumes dinamicamente em statefulset

É possivel que cada pod do statefulset tenha seu proprio volume persistente dinamicamente utilizando claims(Atraves de um template de claim dentro do statefulset)

```yml
  volumeClaimTemplates:
  - metadata: 
      name: mysql-volume 
    spec: 
      accessModes:
        - ReadWriteOnce
      resources:
        requests: 
          storage: 5Gi 
```

E montando o volume nos containers com:

```yml
    spec:
      containers:
        - name: mysql 
          image: mysql 
          env:
            - name: MYSQL_ROOT_PASSWORD
              value: root 
          volumeMounts:
            - mountPath: /var/lib/mysql
              name: mysql-volume
```

Neste caso, para cada replica sera criado um volume de 5gb que fica atachado a pod correspondente. Ou seja se a pod morrer e for recriada o vinculo com o volume ja criado será restabelecido com a nova pod com o mesmo nome.

