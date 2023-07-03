## O que é Open telemetry

- Framework de observabilidade para souftware cloud native.
- Conjunto de ferramentas, APIs s SDKs
- Instrumentacao, geracao, coleta e exportacao de dados de telemetria.

## Colector

Quem faz o recebimento, processamento e envio dos dados da instrumentacao.

Pode se trabalhar com open telemetry das formas

- Com agente collector (side car) em que o agente fica na mesma maquina que a aplicacao, e faz o trabalho de recebimento, processamento e envio para os vendors

- sem collector em que a propia aplicacao é responsavel por enviar os dados via endpoints para os vendors

- Com server collector, em que o collector fica em uma outra maquina.

## instrummentacao

Maneira de lidar como sua apliacao funciona para ser enviada para o vendor. 
Pode ser automatica, manual