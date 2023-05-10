Resiliencia é um conjunto de estrategias adotadas **intencionalmente** para a adaptacao de um sistema quando uma falha ocorre.

Em resumo as estategias para fazer o sistema superar as falhas de forma intencional. Considerando que temos certeza que o nosso software em algum momento vai falhar (Seja por falhas internas ou externas)

Ter estrategias de resiliencia nos possibilita minimizar os riscos de perdas de dados e transacoes importantes para o negocio.

# Estrategias

## Proteger e ser protegido

Um sistema em uma arquitetura distribuida precisa adotar mecanismos de autopreservacao para garantir ao maximo sua operacao com qualidade.

Um sistema nao pode ser egoista ao ponto de realizar mais requisicoes em um sistema que está falhando.

Um efeito domino pode ser causado se diversos sistemas no ecossistema comecam a ficar lentos (Um causa lentidao em outro)

## Health check

Sem sinais vitais nao é possivel saber a saude do sistema.

Usando um mecanismo que checa de tempos em tempo a saúde do sistema

Um sistema que nao está saudavel possui uma chance de se recuperar caso o trafego pare de ser direcionado a ele temporariamente.

O health check deve ter qualidade. (Ex: Pega medias das ultimas requisicoes, acessa ao banco, etc)

## Rate Limiting

Protege o sistema baseado no que ele foi projetado para suportar.

Configurando a quantidade maxima de requisicoes por segundo pode ser suportada.

Preferencia programada por tipo de client. Para nao prejudicar sistemas que sao mais importantes.

## Circuit Breaker

Protege o sistema fazendo com que as requisicoes feitas para ele sejam negadas. Ex: 500

- Circuito fechado = requisicoes chegam normalmente
- Circuito aberto = requisicoes nao chema ao sistema. Erro instantaneo ao client
- Circuito meio aberto = Permite uma quantidade limitada de requisicoes para verificacao se o sistema tem condicoes de voltar ao ar integralmente.

## API Gateway

Centraliza o recbimento de todas as requisicoes da aplicacao.

Em que serao aplicadas regras antes de redirecionar.

**No caso de resiliencia podem sem checadas:**

- Garante que requisicoes "inapropriadas" não chegue até o sistema
    - Ex: usuario nao autenticado

- Implementa politicas de rate limiting, Health check, etc
 
## Service mesh

- Controla o trafego de rede
     - Toda comunicacao entre servicos é feita via o service mesh
     - Pode ser controlado, com dados capturados e auxiliando a entender o que está ocorrendo
- Evita implementacao de protecao pelo proprio sistema
    - Ex: Rate limiting, retries, circuit breaker. Em que voce tem informacoes para tomar as decisoes para as configuracoes
- mTLS
    - Cria uma relacao criptografada interna entre os sevicos


## Comunicação assincrona

Dar a opcao de quem quiser fazer uma requisicao de forma com que nao precise de uma resposta imediata.

- Evita perda de dados
    - Usando filas
- Não ha perda de dados no envio de uma transacão se o server estiver fora
- Servidor pode processar a transacao em seu tempo quanto estiver online
- Entender com profundidade o message brooker/ sistema de stream

## Garantida de entrega: Retry

Existem tecnicas para fazer um retry melhor (Exemplo todos os clientes mandados retry ao mesmo tempo)

- Exponential backoff: Em cada tentativa se adiciona um tempo a mais para o proximo retry

- Exponential backoff - Jitter: Adiciona um ruido antes da proxima tentativa para evitar retentivas em concorrencia

## Garantida de entrega: Kafka

Usando message broker, pode ser configurar se queremos ter uma confirmacao de recebimento da mensagem pelo broker.

No kafka por exemplo.
É possivel utilizar
- Ack0 - O message broker nao devolve para o consumer se recebeu ou nao a mensagem
- Ack1 - Leader - O message broker devolve para o consumer se o lider recebeu ou nao a mensagem
- Ack1 - ALL - O message broker devolve para o consumer se o todas as replicas receberam a mensagens.

Deve ser avaliado caso a caso quando é mais importante utilizar cada um dos casos.

## Situacoes complexas

- O que acontece se o messa broker cair?
- Havera perda de mensagens?
- Seu sistema ficar fora do ar?
- Como garantir resiliencia?


