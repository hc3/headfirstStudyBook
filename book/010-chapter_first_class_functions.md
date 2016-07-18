## funções de primeira classe

First Class Functions
- as funções em javascript podem ser declaradas de duas formas:
Function declaration :
````js
function quack(num) {
  for (var i = 0; i < num; i++) {
    console.log("Quack!");
  }
}
quack(3);
````
Function experession :
````js
var fly = function(num) {
  for (var i = 0; i < num; i++) {
    console.log("Flying!");
  }
};
fly(3);
````
Aqui podemos pensar que temos apenas mais do mesmo, já que no final são duas funções que irão fazer o que lhes foi mandado, então qual é a diferença entre function declaration e function expression?, veja bem a function declaration ela é lida antes do código vamos entender bem isso aqui, quando o browser é carregado as functions declarations são lidas e carregadas no caso a cima seria criado uma variável **quack** que receberia a referência para função, mas isso seria feito antes do browser carregar qualquer parte do código, na function expression não o valor para a variável fly será a referência para função anonima para qual a mesma foi atribuida, mas esse valor só será criado após o código ser lido.

<h5> Funções são valores! </h5>

quando criamos uma função seja com function declaration ou function expression estamos declarando uma variável que irá ser a referência para acessarmos essa função, então podemos atribuir funções a variáveis.

````js
function quack(num) {
  for (var i = 0; i < num; i++) {
  console.log("Quack!");
  }
}

var fly = function(num) {
  for (var i = 0; i < num; i++) {
  console.log("Flying!");
  }
}

var superFly = fly;
superFly(2);

var superQuack = quack;
superQuack(3);
````
declaramos novamente as duas funções sendo a primeira uma function declaration e a segunda uma function expression, nos dois casos serão criadas duas variáveis **quack** e **fly** que irão armazenar as referências para suas respectivas funções, depois passamos a referência que está na variável **fly** para **superFly** e invocamos **superFly** usando os parênteses, depois fazemos o mesmo com a variável **quack** o que quero que seja entendido aqui é que **referências são apenas referências tanto com declarations ou experessions**

<h5> Funções de primeira classe Javascript! </h5>

vimos anteriormente que funções são valores em javascript, podendo ser atribuidas as suas referências as variáveis, mas funções são executadas e ai que está a difereça entre funções e valores, podemos passar funções para variáveis, retornar funções de dentro de funções, armazenar objetos e arrays em funções, passar funções por paramêtro para outras funções.
**FIRST CLASS FUNCTIONS** esse é o termo usado para denomoinar esse tipo de função que tem:

* Atribuir o valor da função a variável ou armazenear em arrays e objetos.
* Passar por parâmetro para outras funções
* Retornar funções de dentro de funções.

<h5> Praticando first class functions! </h5>
vamos agora partir para uma abordagem mais prática do assunto, criaremos uma situação hipotética para um sistema de controle de viagens vamos criar a estrutura básica:
````js
var passengers = [ { name: "Jane Doloop", paid: true },
                  { name: "Dr. Evel", paid: true },
                  { name: "Sue Property", paid: false },
                  { name: "John Funcall", paid: true } ];
````
temos aqui uma estrutura denominada passengers que é um array de objetos cada objeto tem **name** e **paid** como atributos precisamos criar um código para processar os passageiros exibir o nome e ver se eles pagaram a passagem, para isso podemos criar três funções como já estavamos fazendo anteriormente vamos ver o código.
````js
function checkPaid(passengers) {
  for (var i = 0; i < passengers.length; i++) {
    if (!passengers[i].paid) {
      return false;
    }
  }
  return true;
}
````

````js
function checkNoFly(passengers) {
  for (var i = 0; i < passengers.length; i++) {
    if (onNoFlyList(passengers[i].name)) {
      return false;
    }
  }
  return true;
}
````

````js
function printPassengers(passengers) {
  for (var i = 0; i < passengers.length; i++) {
    console.log(passengers[i].name);
    return false;
  }
  return true;
}
````
Podemos ver aqui a duplicação de código nas funções **checkPaid** e **checkNoFly** ,vamos resolver isso com first class functions.
primeiro vamos criar uma nova função processPassengers que vai receber dois parâmetros o primeiro é a coleção de passageiros o segundo é uma função que vai fazer a verificação.
exemplo:
````js
function processPassengers(passengers, testFunction) {
  for (var i = 0; i < passengers.length; i++) {
    if (testFunction(passengers[i])) {
      return false;
    }
  }
  return true;
}
````
para entendermos melhor a função **processPassengers** recebe uma função como segundo parâmetro e essa função será a responsável pelo teste se o passageiro entrar no if e retornar true a função **processPassagenrs** vai retornar falso ou seja se o passageiro retornar true a função retorna falso por que o passageiro falhou no teste em qualquer outro caso **processPassengers** retornar true. Vamos criar as duas funções que vão executar esse teste.

````js
function checkNoFlyList(passenger) {
  return (passenger.name === "Dr. Evel");
}
````
vamos testar se o passageiro pode viajar e aqui todos os passageiros exceto "Dr. Evel" podem viajar, já que **checkNoFlyList** vai retornar true se o nome for igual a "Dr. Evel". lembrando que essa é a No Fly List ( lista dos que não podem viajar ).

````js
function checkNotPaid(passenger) {
  return (!passenger.paid);
}
````
e aqui checamos se o passageiro pagou a passagem se não tiver pago retorna true.

vamos colocar tudo junto agora:

````js
var allCanFly = processPassengers(passengers, checkNoFlyList);
if (!allCanFly) {
  console.log("The plane can't take off: we have a passenger on the no-fly-list.");
}
````

````js
var allPaid = processPassengers(passengers, checkNotPaid);
if (!allPaid) {
  console.log("The plane can't take off: not everyone has paid.");
}
````
