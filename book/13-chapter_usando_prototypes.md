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

Objetos em javascript podem herdar propriedades e comportamentos de outros objetos usando herança prototipica, vamos ver um pequeno exemplo de como um construtor pode usar o prototype para herança:

````js
function Dog(name, breed, weight) {
  this.name = name;
  this.breed = breed;
  this.weight = weight;
}
Dog.prototype.species = "Canine";

Dog.prototype.bark = function() {
  if (this.weight > 25) {
    console.log(this.name + " says Woof!");
  } else {
    console.log(this.name + " says Yip!");
  }
};
Dog.prototype.run = function() {
  console.log("Run!");
};
Dog.prototype.wag = function() {
  console.log("Wag!");
};
````
usando a propriedade **prototype** podemos criar comportamentos ou propriedades que serão herdadas por outros objetos que sejam instancias de **Dog** vamos fazer um teste driver para ver isso tudo funcionando.

````js
function Dog(name, breed, weight) {
  this.name = name;
  this.breed = breed;
  this.weight = weight;
}
Dog.prototype.species = "Canine";
Dog.prototype.bark = function() {
  if (this.weight > 25) {
    console.log(this.name + " says Woof!");
  } else {
    console.log(this.name + " says Yip!");
  }
};
Dog.prototype.run = function() {
  console.log("Run!");
};
Dog.prototype.wag = function() {
  console.log("Wag!");
};
var fido = new Dog("Fido", "Mixed", 38);
var fluffy = new Dog("Fluffy", "Poodle", 30);
var spot = new Dog("Spot", "Chihuahua", 10);

fido.bark();
fido.run();
fido.wag();
fluffy.bark();
fluffy.run();
fluffy.wag();
spot.bark();
spot.run();
spot.wag();
````
o construtor **Dog** tem três métodos e um atributo na sua propriedade prototype e partir do momento que criamos três novos objetos **fido**,**fluffy** e **spot** usando o operador **new** para criar novos Dogs é enviado também o prototype de Dog para as instancias dele, podemos é claro subscrever esses comportamentos por exemplo:

````js
// ...
var spot = new Dog("Spot", "Chihuahua", 10);
spot.bark = function() {
  console.log(this.name + " says WOOF!");
};
// ...
spot.bark();
spot.run();
spot.wag();
````
dessa forma o método **bark** do objeto **spot** é alterado e ao invocar **bark()** não será usado o valor do prototype já que o método foi subscrito no objeto spot, podemos agora pensar como o **this.name** funciona já que o método vem do prototipo? Quando estamos usando o **this** no construtor ele vai referenciar o objeto que está chamando o método. Podemos criar prototypes depois da instanciação dos objetos por exemplo:

````js
var barnaby = new Dog("Barnaby", "Basset Hound", 55);
Dog.prototype.sit = function() {
  console.log(this.name + " is now sitting");
}
````
o objeto barnaby vai herdar o método sit mesmo ele sendo criado na linha depois da sua instanciação, prototypes são dinâmicos, vamos ver algumas implementações mais "interessantes":

````js
Dog.prototype.sitting = false;
Dog.prototype.sit = function() {
  if (this.sitting) {
    console.log(this.name + " is already sitting");
  } else {
    this.sitting = true;
    console.log(this.name + " is now sitting");
  }
};
````
primeiro foi criado uma propriedade no prototype e foi atribuido o valor de falso para ela, logo apos temos a criação de um método que usa a propriedade que está no prototype ( usando o **this** ) e no bloco else temos a alteração dessa propriedade em **this.sitting = true**. Existe uma maneira de saber de onde vem a propriedade de um objeto se é do prototype ou é do próprio objeto.

````js
spot.hasOwnProperty("species");
fido.hasOwnProperty("species");
````
o método **hasOwnProperty** irá retornar falso pois a propriedade **species** está definida no prototype.

570
