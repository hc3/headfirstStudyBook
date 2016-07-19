## Funções de Primeira Classe
### First Class Functions

as funções em javascript podem ser declaradas de duas formas:

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

Aqui podemos pensar que temos apenas mais do mesmo, já que no final são duas funções que irão fazer o que lhes foi mandado, então qual é a diferença entre function declaration e function expression? veja bem a function declaration ela é lida antes do código, vamos entender bem isso aqui, quando o browser é carregado as functions declarations são lidas e carregadas no caso a cima seria criado uma variável **quack** que receberia a referência para função, mas isso seria feito antes do browser carregar qualquer parte do código, na function expression não, o valor para a variável fly será a referência para função anônima para qual a mesma foi atribuida, mas esse valor só será criado após o código ser lido.

<h3> Funções são valores! </h3>

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

declaramos novamente as duas funções sendo a primeira uma function declaration e a segunda uma function expression, nos dois casos serão criadas duas variáveis **quack** e **fly** que irão armazenar as referências para suas respectivas funções, depois passamos a referência que está na variável **fly** para **superFly** e invocamos **superFly** usando os parênteses, depois fazemos o mesmo com a variável **quack**, o que quero que seja entendido aqui é que **referências são apenas referências tanto com declarations ou experessions**.

<h3> Funções de primeira classe Javascript! </h3>

vimos anteriormente que funções são valores em javascript, podendo ser atribuidas as suas referências a variáveis, mas funções são executadas e ai que está a diferença entre funções e valores, podemos passar funções para variáveis, retornar funções de dentro de funções, armazenar objetos e arrays em funções, passar funções por paramêtro para outras funções.
**FIRST CLASS FUNCTIONS**
esse é o termo usado para denomoinar esse tipo de função:

* Atribuir o valor da função a variável ou armazenear em arrays e objetos.
* Passar por parâmetro para outras funções
* Retornar funções de dentro de funções.

<h3> Passando funções por parâmetro </h3>

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

podemos ver como é simples a passagem de parâmetros usando funções com isso temos uma composição do código que pode ser reaproveitado em diversas partes, e se acontecer alguma mudança só precisamos alterar a função que estar sendo passada por parâmetro.

<h3> Retornando funções de dentro de funções </h3>

Vamos alterar um pouco os dados:

````js
var passengers = [ { name: "Jane Doloop", paid: true, ticket: "coach" },
                  { name: "Dr. Evel", paid: true, ticket: "firstclass" },
                  { name: "Sue Property", paid: false, ticket: "firstclass" },
                  { name: "John Funcall", paid: true, ticket: "coach" } ];
````

temos o tipo da cabite onde primeira classe tem bebidas de coquetéis e coach é a classe básica vamos criar uma função que vai verificar qual o tipo da passagem do cliente e assim servir a bebida adequada ao mesmo.

````js
function serveCustomer(passenger) {
  if (passenger.ticket === "firstclass") {
    alert("Would you like a cocktail or wine?");
  } else {
    alert("Your choice is cola or water.");
  }
  // fazer outras coisas...
}
````

podemos ver como foi fácil usando um bloco if resolvemos o problema, mas ai fica a dúvida e se existissem outras classes? como "economica" , "super" e se os drinks mudarem? podemos ver que esse código pode gerar muita complicação dependendo da alteração que possa vir.
vamos separar o código que varia em outra função:

````js
function createDrinkOrder(passenger) {
  if (passenger.ticket === "firstclass") {
    alert("Would you like a cocktail or wine?");
  } else {
    alert("Your choice is cola or water.");
  }
}
````

criamos outra função passando **passenger** e colocamos lá o código que varia na função **serverCustomer** vamos refatorar:

````js
function serverCustomer(passenger) {
  createDrinkOrder(passenger);
}
````

podemos ver que ficou muito melhor assim, mas e no dia-a-dia sera que esse código ia suprir nossas necessidades? acredito que não e se tivessemos 500 pasageiros para servir iamos fazer **createDrinkOrder** 500 vezes? hmm não parece muito legal , mas calma ai que podemos retornar funções de dentro de funções e isso vai resolver nosso problema.
vamos refatorar **createDrinkOrder**

````js
function createDrinkOrder(passengers) {
  var orderFunction;

  if (passenger.ticket === "firstclass") {
    orderFunction = function() {
      alert("Would you like a cocktail or wine?");
    }
  } else {
    orderFunction = function() {
      alert("Your choice is cola or water.");
    }
  }
  return orderFunction;
}
````

primeiro de tudo vamos criar uma variável que depedendo do atributo ticket irá exibir um alerta através de uma função que sera retornada, vamos ver o código:

````js
function serveCustomer(passenger) {
  var getDrinkOrderFunction = createDrinkOrder(passenger);
  getDrinkOrderFunction();
  // get dinner order
  getDrinkOrderFunction();
  getDrinkOrderFunction();
  // show movie
  getDrinkOrderFunction();
}
````

````js
function servePassengers(passengers) {
  for (var i = 0; i < passengers.length; i++) {
    serveCustomer(passengers[i]);
  }
}
````

````js
servePassengers(passengers);
````

finalizamos essa primeira parte que irá se aprofundar um pouco em funções aqui vimos o que são funções em javascript que são valores e que podem ser passados para variáveis, que podem serem passados por parâmetro para outras funções, e que podem ser retornadas por outras funções ( uma função que retorna outra função ), a partir da aqu já podemos pensar o quanto de reuso que pode e deve ser feitos com essa habilidade do javascript devemos sempre lembrar que as funções são de **primeira ordem**
