## Funções de anônimas, scope e closures.

Já conhecemos as duas maneiras de se criar funções em javascript, sendo elas **function declaration** e **function expression**, mas ainda existem as **anonymous Functions** ou seja funções que não tem nome, quando criamos uma declaration estamos definitivamente dando um nome para função mas quando criamos uma function expression não estamos dando um nome para a função e sim atribuindo a mesma para uma variável, e nesse contexto entram as funções anônimas.

<h3> Funções Anônimas </h3>

````js
function handler() { alert("O yeah"); }
window.onload = handler;
````

````js
window.onload = function() { alert("O yeah"); }
````
no primeiro código criamos uma function declaration com o nome de **handler** e depois atribuimos a função para a propriedade **onload** e quando a página for carregada a função handler será executada, já no segundo exemplo temos o uso da função anônima atribuindo a mesma para prorpiedade **onload**, nos dois casos tudo funciona da mesma forma, mas podemos ver que no segundo economizamos uma linha de código e com isso temos um código mais legível.
Okay já sabemos que funções podem ser atribuidas a variáveis que podem ser passadas como parâmetro para outras funções e que podem ser retornadas de dentro de outras funções mas até o momento estamos escrevendo um código muito **VERBOSO** vamos ao exemplo:

````js
function cookieAlarm() {
  alert("Hora de acordar!");
}

setTimeout(cookieAlarm,60000);
````

````js
setTimeout(function() {
  alert("Hora de acordar!");
},60000)
````
aqui fizemos o uso da função anônima passando a mesma por parâmetro para uma função.

<h3> Quando uma função é definida? </h3>

Como já vimos o browser faz 2 etapas para carregar o código javascript, na primeira ele procura por functions declarations e faz a criação das variáveis que irão referenciar as mesmas, na segunda o browser executa o código da primeira até a última linha atribuindo a referencia para as variáveis que recebem function expression por conta disso funções criadas com function expression são executadas seguindo o fluxo do código, vamos entender melhor no exemplo:

````js
var migrating = true;

if(migrating) {
  quack(4);
  fly(4);
}

var fly = function(num) {
  for (i = 0; i < num; i++) {
    console.log("Flying!");
  }
};

function quack(num) {
  for (i = 0; i < num; i++) {
    console.log("Quack!");
  }
}
````
Ao tentar executar esse código vamos ter um erro, isso porque a function expression está sendo invocada antes de sua declaração ou seja o browser não carregou a função na variável **fly**, no momento em que foi invocada a função a variável está como **undefined**. Já **quack** funciona normalmente já que é uma function declaration e ela é carregada primeiro pelo browser, a esse fenômeno damos o nome de **hoisting** ou seja podemos criar functions declartions em qualquer parte do código graças ao hoisting, com as functions expressions não é bem assim quando criamos uma e atribuimos a uma variável global como foi feito no código acima não podemos invocar a mesma antes de sua declaração.

<h3> Scope e Closures </h3>


````js

var migrating = true;

var fly = function(num) {
  var sound = "Flying";
  function wingFlapper() {
    console.log(sound);
  }
  for (var i = 0; i < num; i++) {
    wingFlapper();
  }
};

function quack(num) {
  var sound = "Quack";
  var quacker = function() {
    console.log(sound);
  };
  for (var i = 0; i < num; i++) {
    quacker();
  }
}

if (migrating) {
  quack(4);
  fly(4);
}
````
