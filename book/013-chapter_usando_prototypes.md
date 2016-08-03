## Usando Prototypes

Nesse capitulo vamos aprender outras maneiras de criar interação entre os objetos vamos entender como extender a partir de objetos já existentes e ver como o javascript usa orientação a objetos ou como dizem orientação a prototipos.

<h3> Intrdução </h3>

para quem vem de linguagens como Java ou C++ entender a orientação a objetos em javascript pode ser um pouco mais complicado, primeiro devemos ter em mente que javascript não tem a orientação a objetos classica com classes em javascript temos uma orientação a Prototypes ou seja herança baseada em prototipos, algo que pode ser meio confuso mas aqui vamos tentar explicar de uma maneira mais simples.
vejamos o código construtor do capitulo anterior:

````js
function Dog(name, breed, weight) {
  this.name = name;
  this.breed = breed;
  this.weight = weight;
  this.bark = function() {
    if (this.weight > 25) {
      alert(this.name + " says Woof!");
    } else {
      alert(this.name + " says Yip!");
    }
  };
}
````
usando o construtor podemos criar um objetos consistente que pode ser customizado após sua criação, todos os objetos criados a partir do objeto **Dog** irão compartilhar dos mesmos atributos e métodos:

````js
var fido = new Dog("Fido", "Mixed", 38);
var fluffy = new Dog("Fluffy", "Poodle", 30);
var spot = new Dog("Spot", "Chihuahua", 10);
````
com isso vamos criar três cachorros que vão ter referência para a função **bark** mas aqui temos um pequeno problema, repetição de código com a função que está no construtor e se fosse necessário criar 5000 cachorros? teriamos 5000 funções que no final fazem a mesma coisa, todo o cachorro vai precisar ter a função **bark** e agora?

Realmente a duplicação de código é um problema, o código duplicado atrapalha na performace e a legibilidade do código e existem outras maneiras de criarmos objetos mais flexíveis, quando usamos construtores estamos querendo que as instancias reusem o comportamente já criado mas usando o construtor para isso estamos colocando esse comportamente em um único lugar dentro do construtor e com isso todas as instancias criadas a partir desse construtor tem uma copia do método, e para resolver esse problema vamos usar os prototypes criando objetos que são extensões de outros objetos.

<h3> O que são Prototypes? </h3>

569
