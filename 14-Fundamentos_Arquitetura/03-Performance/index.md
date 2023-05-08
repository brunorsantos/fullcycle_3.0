É o desempenho de uma software possui para completar um determinado workload

- Unidades de medidas
    - Latencia ou Response time
    - Throughput (Requisicao por minuto)


Ter um software performatico é diferente de ter um software escalavel

# Metricas para medir a performance

## Diminuindo a latência

Normalmente medida em milisegundos

Afetada pelo tempo de processamento de aplicacao, rede e chamadas externas

## Aumentando o throughput

Lidar com mais requisicoes

Diretamente ligado a latencia

# Principais razoes para baixa performance

- Processamento ineficiente
    - Problema no algoritmo

- Recursos computacionais limitados
    - Hardware

- Trabalhar de forma nao bloqueante

- Acesso serial a recursos
    - Ex: Loops de acessos em serie a API

# Principais razoes para baixa performance

- Escala da capacidade computacional (CPU, disco, memoria, rede)

- Lógica por tras do software (Algoritmo, queries, overhead de frameworks)

- Concorrencia ou paralelismo

- Banco de dados (tipos de bancos, schema)

- Caching

# Capacidade computacional: Escala vertical vs horizontal

- Escala vertical: Aumentar os recursos computacionais

- Escala horizontal: Adicionar o numero de maquinas

## Diferença entre concorrencia e paralelismo

Concorrencia é sobre lidar com muitas coisas ao mesmo tempo. Paralelismo é fazer muitas coisas ao mesmo tempo.

# Cache

## Cache na borda / Edge computing

Nem chega a bater no servidor, a borda ja devolve antes. Uma copia mais proxima fica em um provedor.

## Dados estaticos

Dados que nao mudam como Css, imagens. Que podem estar tambem em borda

## Paginas web

Salvar as paginas web para outras requisicoes nao precisarem de fazer todo o processamento(ir no banco por exemplo)

## Funcoes internas

Quando possivel salvar em cache algoritmos pesados ou dados que estao salvos em bancos de dados

## Objetos

Salvar o um objeto complexo inteiro em banco

## Cache exclusivo ou compartilhado

### Exclusivo

- Baixa latencia
- Duplicado entre os nós
- Problemas relacionados a sessões (salvando estado)

### Compartilhado

- Maior latencia
- Não ha duplicacao
- Sessoes compartilhadas
- Banco de dados externo
    - Redis
    - Memcache


# Caching vs Edge computing

Edge computing é um servico que consegue processar e salvar dados em servidor mais proximos de clientes. 
- Sendo assim o cache vai ser realizado mais proximo ao usuário
- Evitando a requisicao chagar ate o cloud provider ou infra
- Normalmente arquivos estaticos (cloudflare)
- CDN - Content delivery network (Ex: Videos espalhados para datacenters no mundo - akamai)
    - A empresa que trabalha assim, te cobra pela banda quando ela precisa espalhar um arquivos para as redes (quando um arquivo é acessado pela primeira vez)
- Cloudflare workers
    - Espalha na hora do deploy o arquivos, em que esse processamento utilzia servidores js
- Vercel
    - Suporta next.js e utiliza edge computing com js
