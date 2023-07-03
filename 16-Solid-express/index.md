# Single responsability principle

Uma classe deve ter apenas uma responsabilidade.
Quando colocamos muita coisa para fazer nessa classe estamos complicando o codigo

Dica: Uma classe deve ter apenas um motivo unico para mudar

Exemplo de ferir o principio:

Classe Curso responsavel por definir o campos da curso e persistir os dados desse curso em banco.



# Open closed Principle

Toda classe deve ser aberta para extensao e fechada para modificacao

Tentar utilizar de recursos da orientacao de objetos para incluir novos comportamentos ao inves de modificar a mesma classe.

Exemplo de ferir o principio:

Classe de video, em que dentro da classe faz logica baseada no valor desse type(ex: movie, tv show) para calcular algo.
Poderia ser resolvido criando uma especializao de cada type extendendo uma classe abstrata video

# Liskov Substitution Principle

Subclasses podem ser substituidas pelas classes pai


O Princípio da Substituição de Liskov diz que objetos de uma classe derivada devem poder ser usados como objetos da classe base sem alterar a corretude do programa.

A classe filha precisa compartilhar todos os metodos e atributos da classe pai (Ter e conseguir executar).

# Interface Segregation Principle

Uma classe nao é obrigada a implementar uma interface que ela nao utilizará

Não implementar uma interface a nao ser que voce va utilizar todos os metodos que ela contem, se nao for o caso, crie uma nova interface.

# Dependency Inversion Principle

Dependa de abstracoes e nao de implementacoes
Inverter as dependencias (Instanciar fora da classe)


Exemplo de ferir o principio:

Classe de movie que ao retornar uma categoria, se retorna um new DramaCategory() e alem disso um set de categoria espera um DramaCategory.
Nesse caso deveria ter por exemplo um construtor que espere a interface(ou classe abstrata) Category. Sendo assim o metodo Set tambem esperaria um Category. Desta forma nao estamos mais instanciando nada na classe, apenas quem chama sendo que é possivel o chamador escolher a implementacao adequada para ele (Ex: Teste unitario para uma implementacao de um mock como banco)


