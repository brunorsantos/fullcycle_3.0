# Historico

Antigo ELK stack, composta por

- Elastic search
    - Search engine e analitycs
    - Baseado em Apache Lucene
    - Rapido
    - Escalavel
    - API rest


- Kibana
    - Dashboard em cima do elastic search

- Logstash
    - Engine coletora de dados em tempo real
    - Pipeline para transformação de dados que envia dados para elastic search

## Beats

Agente coletor de dados, que ajuda a substuir o logstash sendo mais facil enviar dados da aplicacao para o elasticsearch.

Pode pegar logs, metricas, network data, audit data, updatime monitoring.

Exemplos de recursos da familia beats

- Metricbeat: servico que coleta metricas de tipo de serviços. ex: elasticsearch, docker

- Heartbeat: servico que verifica em uma determinada lista de serviço qual esta up ou down (Verificado no kibana em uptime)

