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
1º - primeiro o operador NEW vai criar um objeto vazio.
2º - **new** seta o **this** como ponto para criar o novo objeto.
3º - com o **this** fixado podemos chamar a função Dog passando os argumentos.
4º - ao entrar no corpo da função Dog temos atribuição a **this** para os três parâmetros.
5º - ao final da execução da função Dog o operador **new** vai retornar **this** com a referência para o novo objeto criado, **this** será retornado para você e não é necessário deixa explicíto usando **return** e após o novo objeto ser retornado nos vamos atribuir a referência para o mesmo á variável **fido**.
