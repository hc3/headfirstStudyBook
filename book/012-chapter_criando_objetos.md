## Criando Objetos.

podemos criar objetos de forma literal assim:

````js
var taxi = {
  make: "Webville Motors",
  model: "Taxi",
  year: 1955,
  color: "yellow",
  passengers: 4,
  convertible: false,
  mileage: 281341,
  started: false,
  start: function() { this.started = true;},
  stop: function() { this.started = false;},
  drive: function {
  // drive code here
  }
};
````
o resultado seria a criação de um objeto literal atribuido a variável taxi que pode ser usado a qualquer momento os objetos literais nos dão uma maneira simples para criar objetos mas e se fosse preciso criar muitos objetos ao mesmo tempo? Iriamos repetir esse código para os outros objetos e essa concerteza não é a melhor maneira de fazer isso.

<h3> Introdução a criação de objetos </h3>

os construtores ou factories já são bem conhecidos no mundo da OO, basicamente vamos ter uma função que irá retornar um objeto e toda vez que precisarmos criar um novo objeto vamos recorrer a essa função, vamos começar criando um objeto literal:

````js
var dog = {
  name: "Fido",
  breed: "Mixed",
  weight: 38
};
````
mas como criar um dog abstrato? vamos recorrer as funções construtoras.

````js
function Dog(name, breed, weight) {
this.name = name;
this.breed = breed;
this.weight = weight;
}
````
foi definida uma function declaration chamada **Dog** que recebe os parâmetros que são nada mais que os atributos do objeto, é usado o **this** para referênciar os atributos do proprio objeto, agora vamos usar esse construtor para criar novos objetos.

````js
var fido = new Dog("Fido", "Mixed", 38);
````
para criar um novo objeto usamos a palavra reservada **new** que já é muito conhecida entre os javeiros, seguido do nome da função construtora e depois passamos os argumentos que são (name,breed,weight) depois disso a variável fido sera evaluada com o objeto criado.

<h4> Como os construtores funcionam </h4>

Já vimos a implementação do construtor, agora vamos entender um pouco como ele funciona e para isso temos que entender o que o operador **new** faz primeiro vamos ter a invicação:
````js
var fido = new Dog("Fido", "Mixed", 38);
````
<ol>
  <li>  
  o operador NEW vai criar um objeto vazio.
  </li>
  <li>
  **new** seta o **this** como ponto para criar o novo objeto.
  </li>
  <li>
  com o **this** fixado podemos chamar a função Dog passando os argumentos.
  </li>
  <li>
  ao entrar no corpo da função Dog temos atribuição a **this** para os três parâmetros.
  </li>
  <li>
  ao final da execução da função Dog o operador **new** vai retornar **this** com a referência para o novo objeto criado, **this** será retornado para você e não é necessário deixa explicíto usando **return** e após o novo objeto ser retornado nos vamos atribuir a referência para o mesmo á variável **fido**.
  </li>
</ol>

Podemos colocar métodos nos construtores, criamos o objeto Dog para representar um cachorro mas esse cachorro não pode latir já que ele não tem o método latir então vamos implementar esse método no construtor.

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
a criação de métodos para objetos usando o construtores é a mesma usamos o this e uma função anônima com isso já podemos rodar um teste.
````js
var fido = new Dog("Fido", "Mixed", 38);
var fluffy = new Dog("Fluffy", "Poodle", 30);
var spot = new Dog("Spot", "Chihuahua", 10);
var dogs = [fido, fluffy, spot];
for (var i = 0; i < dogs.length; i++) {
  dogs[i].bark();
}
````

vamos construir carros agora, já aprendemos como usar os contrutores para criar objetos então vamos usar!

````js
var car = {
  make: "Chevy",
  model: "Bel Air",
  year: 1957,
  color: "red",
  passengers: 2,
  convertible: false,
  mileage: 1021,
  started: false,
  start: function() {
    this.started = true;
  },
  stop: function() {
    this.started = false;
  },
  drive: function() {
    if (this.started) {
      console.log(this.make + " " +
      this.model + " goes zoom zoom!");
    } else {
      console.log("Start the engine first.");
    }
  }
};
````
esse é o objeto carro temos que criar vários carros iguais a esse para poder usar um construtor então vamos imaginar como esse construtor ficaria:

````js
var chevy = new Car("Chevy", "Bel Air", 1957, "red", 2, false, 1021);
var cadi = new Car("GM", "Cadillac", 1955, "tan", 5, false, 12892);
var taxi = new Car("Webville Motors", "Taxi", 1955, "yellow", 4, false, 281341);
var fiat = new Car("Fiat", "500", 1957, "Medium Blue", 2, false, 88000);
````
muitos argumentos são passados me parece que está ficando algo confuso, vamos dar uma olhada na função construtra agora:

````js
function Car(make, model, year, color, passengers, convertible, mileage) {
  this.make = make;
  this.model = model;
  this.year = year;
  this.color = color;
  this.passengers = passengers;
  this.convertible = convertible;
  this.mileage = mileage;
  this.started = false;
  this.start = function() {
    this.started = true;
  };
//rest of the methods here
}
````
podemos ver quantos parâmetros são esperados na função construtra para que a mesma possa criar o objeto, nesses casos podemos passar esse parâmetros para um objeto literal e passar o objeto litral como parâmetro para função construtora vamos ver isso na prática.

````js
var cadi = new Car("GM", "Cadillac", 1955, "tan", 5, false, 12892);

var cadiParams = {make: "GM",
model: "Cadillac",
year: 1955,
color: "tan",
passengers: 5,
convertible: false,
mileage: 12892};
````
vamos remover os dados da função construtora e passar para um objeto literal, para então fazermos assim:

````js
var cadi = new Car(cadiParams);
````
540
