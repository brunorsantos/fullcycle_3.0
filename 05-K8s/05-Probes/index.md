# Probes

## Liveness Probe

É uma configuracao passada dentro da spec do container que verifica repetidamente se o container esta funcionando.

Essa verificacao pode ser atravez de HTTP(requisicao), comand (quando executa um comando dentro do container)
ou TCP(estabelecendo uma conexao tcp com o container). O mais utilizado é o http utilizando um endpoint de healtcheck criado manualmente na aplicacao.

Quando o liveness probe indentifica que o container nao está saudavel, ele o reinicia

É definido da seguinte forma:

```
          livenessProbe:
            httpGet:
              path: /healthz
              port: 80
            periodSeconds: 5
            failureThreshold: 3
            timeoutSeconds: 1 
            successThreshold: 1
```

- port: é valor do container que está expoxto no container(Não do service)
- periodSeconds: de quanto em quanto tempo será feita a verificacao
- failureThreshold: quantas vezes o check precisa retornar um erro para ser considerada falha no container(e reiniciar o mesmo)
- timeoutSeconds: quanto tempo será aguardado a resposta do container para ser considerado como erro
- successThreshold: quantas vezes é necessário um retorno de sucesso para ser realmente considerado que o container está saudavel

## Readiness probe

Verifica quando a aplicacao está pronta para receber trafego. 

Possivel visualizar na listagem dos pods o atributo READY com valor 1/1 (consideando um container por pod)

Ele tambem executa de tempos em tempos. Verificando se a aplicacao esta pronta tanto no momento inicial, ou após esse momento para remover o pod de Ready

```
          readinessProbe:
            httpGet:
              path: /healthz
              port: 80
            periodSeconds: 3
            failureThreshold: 1
            initialDelaySeconds: 10

```
- initialDelaySeconds: é um delay inicial que pode ser utilizado como gap para o startup da aplicacao. Em que somente apos isso as verificaçoes vão se inicial

### Readiness probe x Liveness Probe

Dependendo como os 2 estão configurados em conjuto, poderemos ter conflitos, pois o liveness pode reiniciar o container antes mesmo de atindir o readiness (Entrando em Loop)

Uma forma de evitar isso é ajustar o `initialDelaySeconds` de ambas as configuraçoes, fazendo o liveness aguardar que o container fique pronto. Porem como o readiness executa mesmo apos a startup (para redirecionar o trafego caso seja necessario) ainda assim pode ocorrer algum conflito caso o container seja reiniciado

## Startup probe

A solucao para lidar com a combinacao entre liveness e readiness probe, é utilizar o startup probe. Quanto tambem é util quando nao se sabe ao certo o tempo em que o aplicacao demora para ficar pronta inicial

Ele funcionará similar ao readiness porem apenas no processo de inicializacao no container.


```
          startupProbe:
            httpGet:
              path: /healthz
              port: 80
            periodSeconds: 3
            failureThreshold: 30
```

Com os valores de `failureThreshold` e `periodSeconds` podemos formar uma combinacao que funcionará como um timeout para a aplicacao ser iniciada. No exemplo acima seria um limite maximo 90 segundos. Porem seria iniciada rapidamente caso ela se inicie rapidamente


Apenas quando o startup for feito com sucesso que se iniciarao as verificacoes do readiness e liveness probe.

Sendo assim, podemos evitar utilizar o valor de `initialDelaySeconds` em ambas.