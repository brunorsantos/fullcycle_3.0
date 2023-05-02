# Namespace

Uma separacao virtual dos objetos do K8S.

Quando nao definimos explicitamente, vai ser utilizado o namespace `default`.

Pode ser utilizar para separar projetos.
É possivel limitar recursos por namesapce e tambem limitar permissoes por namesapaces.

Mostra todos os namespaces no cluster:
```
kubectl get namepace
```

Criar um namespace:

```
kubectl create ns [nome]
```

Para que um objeto seja criado em um namespace pode utilizar no comando:

```
kubectl apply -f file.yaml -n=[namespace]
```

Ou entao na spec da definicao do arquivo.

# Service account

O service account é um objeto do K8S que permite gerenciar os tipo de acesso atraves de roles associadas aos mesmos.

Um conteinet precisa de acessar objetos do K8S, para se manter. É adequado que a pod esteja associada a um service account diferente do default com acesso limitado por questoes de segurança.

```yml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: server

---

apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata: 
  name: server-read
rules: 
- apiGroups: [""]
  resources: ["pods","services"]
  verbs: ["get","Watch","list"]
- apiGroups: ["apps"]
  resources: ["deployments"]
  verbs: ["get","Watch","list"]

---

apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata: 
  name: server-read-bind
subjects:
- kind: ServiceAccount
  name: server
  namespace: prod
roleRef:
  kind: Role
  name: server-read 
  apiGroup: rbac.authorization.k8s.io
```

Neste exemplo é mostrado a criacao de um `ServiceAccount` novo, de uma nova `Role` que define as regras de acesso por grupos e de uma associacao de atraves de uma `RoleBinding`.

Após isto pode ser configurada na spec do container(No deployment por exemlplo) usando a tag `ServiceAccount`