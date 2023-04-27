# Cert-manager

É possivel utilizando ingress incluir certificado TLS que se renovará automaticamente por hosts.

Seguindo as intrucoes na pagina do [cert-manager](https://cert-manager.io/v1.1-docs/installation/kubernetes/) para k8s, será instado no cluster a aplicacao que ficara responsável por isso.

Apos a instalacao, deve ser criado um manifesto de tipo `ClusterIssuer` conforme abaixo

```yml
apiVersion: cert-manager.io/v1alpha2
kind: ClusterIssuer
metadata:
  name: letsencrypt
  namespace: cert-manager
spec:
  acme:
    server: https://acme-v02.api.letsencrypt.org/directory
    email: wesley@schoolofnet.com
    privateKeySecretRef:
      name: letsencrypt-tls
    solvers:
    - http01:
        ingress:
          class: nginx
```

Apos isto, deve ser associar o certificado no manifesto do ingress

```yml

apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: ingress-host
  annotations:
    kubernetes.io/ingress.class: "nginx"
    cert-manager.io/cluster-issuer: "letsencrypt"
    ingress.kubernetes.io/force-ssl-redirect: "true"
spec:
  rules:
  - host: "ingress.fullcycle.com.br"
    http:
      paths:
      - pathType: Prefix
        path: "/admin"
        backend:
          serviceName: goserver-service
          servicePort: 80
  tls:
  - hosts:
    - "ingress.fullcycle.com.br"
    secretName: letsencrypt-tls
```