Para escalar horizontalmente é necessario ao desenvolver algumas preocupacoes em relacao a descentralizacao da maquina



- Disco efemero
    - Tudo que está no disco pode ser perdido
- Servidor de aplicativos vs Servidor de assets
    - NAo utilizar o servidor para guardar arquivos estaticos
- Cache centralizado
    - Não salvar cache diretamento no servidor. utilizar cache compartilhado
- Sessoes centralizadas
    - Não manter sessoes diretamente no servidor de aplicativos
- Upload/ Gravacao de arquivos
    - Nao deve gravar no servidor


# Escala banco de dados

- Aumentando recursos computacionais
- Distribuindo responsabilidades
    - Criando banco de dados especifico para leitura/Escrita
- Shards de forma horizontal
    - Forma de particionar o banco em fragmentos diferentes
- Serverless
    - Deixar o provedor de cloud preocupar com toda a infra de banco

## Otimizacao de queries e indices

- Trabalhar com indices de forma consciente
- APM (Application performance monitoring) nas queries
- Explain na queries
    - Exibe como o banco esta fazendo a busca
- CQRS (Command query Resposability Segregation)
    - Padrao para dividir quando os acessos da aplicacao sao para alteracao ou para busca

# Proxy reverso

É um servidor que fica a frente dos servidores web e encaminha as solicitacoes do cliente (por exemplo navegador web) para esses servidores web

## Solucoes populares

- Nginx
- HAProxy
- Traefik


