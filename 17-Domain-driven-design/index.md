## Softwares complexos

- DDD deve ser aplicado para casos de projetos complexos
- Grandes projetos possuem muitas áreas, muitas regras de negocio, muitas pessoas com diferentes visoes em diferentes contextos
- Não ha como não utilizar tecnicas avançadas em projetos de alta complexidade
- Grande parte da complexidade desse tipo de software não vem da tecnologica, mas sim da comunicação, separação de contextos, enentendimento do negócio por diversos ângulos


## Como o DDD pode ajudar

- Entender com profundidade o dominio e subdominio da aplicacao

Dominio é algo que esta ligado a funcao principal que queremos desenvolver.
Subdominio já é uma quebra desse dominio.

- Ter uma linguagem universal (linguagem ubiqua) entre todos os envolvidos

Todo mundo precisa estar na mesma pagina (até o codigo)

- Criar o design estrategico utilizando bounded contextos

- Criar o design tático para conseguir mapear e agregar as entidades e objetos de valor da aplicacao, bem como os eventos de dominio

- Clareza do que é complexidade de negocio e complexidade tecnica

Em resumo DDD é sobre modelar um linguagem universal dentro de contexto limitado explicito


# Dominios, subdominios e contextos

## Dominio vs subdominio

Em um dominio vamos ter subdominios to tipo:

- Core Domain
    - Coracao do negocio
    - Diferencial competitivo da empresa

- Support subdomain
    - Apoiam o dominio
    - Faz a operacao do dominio possivel
- Generic subdomain
    - Software auxiliares


## Espaço de problema e espaco de solucao

### Problema

Visao geral do dominio e suas complexiades -> Subdominios

### Solucao

Analise e modelagem do dominio -> contexto delimitados

## Bounded contexts

é uma divisao explicita dentro de um dominio. Dentro dessa divisao todos os termos da linguagem ubiqua tem o mesmo significado.

Quando termos iguais tem significados dirferentes, é um indicativos de que temos 2 diferentes contextos.

Ou entao palavras diferente representando a mesma coisa.

Vamos ter elementos que sao transversais, como `Cliente` que mesmo tendo o mesmo significado em contextos de diferentes, vao ter caracteristicas diferentes de acordo com o contexto. 

Ex: 
- Cliente em venda de ingresso terá Evento, Ticket, local, vendedor.
- Cliente em suporte terá Ticket (outro significado), Duvida, departamento, responsavel

# Modelagem estrategica

## Context mapping

