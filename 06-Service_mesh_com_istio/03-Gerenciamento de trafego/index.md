# Gateway

Gerencia a entrada e saída do trafego. Trabalha no layers 4-6, garantindo o gerenciamento de portas, host e TLS. É conectado diretamente a um Virtual service que será responsavel pelo roteamento

# Virtual Service

Permite voce configurar como a requisiçoes serao roteadas para um serviço. Ela possui uma série de regras que quando aplicadas farão com que a requisição seja direcionada ao destino correto.

- roteamento de trafego
- Subsets
- Fault injection
- Retries
- Timeout

# Destination rules

A destination rule é usada para configurar o que acontece com o trafego quando ele chega naquele destino

