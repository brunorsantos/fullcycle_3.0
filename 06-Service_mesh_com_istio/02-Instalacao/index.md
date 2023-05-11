- Usar [k3d](https://k3d.io/v5.4.9/) como base


https://istio.io/latest/docs/setup/getting-started/

- Deve se instalar o binario do istioclt na maquina. Baixando e inserindo no PATH

Com o `istioctl` deve se executar:

```
istioctl install
```

Que usará o profile default 

Existem addons interessantes para instalar como:

- [kiali](https://istio.io/latest/docs/ops/integrations/kiali/)
- [jagger](https://istio.io/latest/docs/tasks/observability/distributed-tracing/jaeger/)
- [prometeus](https://istio.io/latest/docs/ops/integrations/prometheus/)
- [grafana](https://istio.io/latest/docs/ops/integrations/grafana/)


Para abrir dashboard do kiali
```
istioctl dashboad kiali
```