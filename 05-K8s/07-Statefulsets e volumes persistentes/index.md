## Stateless vs Stateless

Uma aplicacao Stateless é uma aplicacao que nao se preocupa em manter um estado (dados, sessao, etc).
Isto é a aplicacao em si nao salva nenhum dado que seja necessario para ser utiliza em uma futura requisicao por exemplo.
Enquanto em uma aplicacao Stateful, é necessario este salvamento.

## Volumes persistentes

Para utilizar volumes persistentes no k8s, atraves de pool de storage disponivel para o cluster. De maneira que os espacos sao disponibilidades para serem utilizados atravez do Claims.

O pool de storage por ser estatico ou dinamico. No modo estatico, previamente é criado um ou mais pool de storage com tamanhos definidos. Geramente é utilizado nos modelos On premisse

No modo dinamico(mais utilizado) são utilizados os `StorageClass`. É um especificação que faz com que exita um driver para que dinamicamente seja possivel provisionar espaco em disco para uma determinada aplicação.

Nesse caso, quando for feita uma claim para uma storageClass, ela ficará responsavel por gerenciar junto com o provedor de nuvem o espaço em disco

