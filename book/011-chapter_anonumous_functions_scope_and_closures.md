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

Como já vimos o browser faz 2 etapas para carregar o código javascript, na primeira ele procura por functions declarations e faz a criação das variáveis que irão referênciar as mesmas, na segunda o browser executa o código da primeira até a última linha atribuindo a referência para as variáveis que recebem function expression por conta disso funções criadas com function expression são executadas seguindo o fluxo do código, vamos entender melhor no exemplo:

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

È perfeitamente normal definir funções dentro de outras funções, mas devemos usar declaration ou expression? quando definimos uma função dentro da outra estamos alterando o escopo ou seja onde a função é visível vamos ver o código abaixo para poder entender esse conceito.

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
a função interna tem o escopo local a função externa tem o escopo global, então **fly** e **quack** tem o escopo global, a função **wingFlapper** será definida quando entrarmos no corpo da função **fly** a função **quacker** só será definida na sua chamada dentro do loop.

- Vamos entender melhor o escopo...

````js
var justAVar = "eu sou global!";

function ondeEstou() {
    var justAVar = "eu sou local!";

    reutnr justAVar;
}

var resultado = ondeEstou();
console.log(resultado);
````
foi criada uma variável global chamada **justAVar** depois foi criada uma função que cria uma nova variável chamada **justAVar** e retorna ao invocarmos essa função temos que a variável local foi passada e não a global, vamos alterar esse código e retornar uma função agora:

````js
var justAVar = "eu sou global!";

function ondeEstou() {
    var justAVar = "eu sou local!";

    function dentro() {
      return justAVar;
    }

    return dentro();
}

var resultado = ondeEstou();
console.log(resultado);
````
mesmo resultado.

vamos retornar a função sem invocar a mesma:

````js
var justAVar = "Oh, don't you worry about it, I'm GLOBAL";
function whereAreYou() {
  var justAVar = "Just an every day LOCAL";
  function inner() {
    return justAVar;
  }
  return inner;
}
var innerFunction = whereAreYou();
var result = innerFunction();
console.log(result);
````
quando chamarmos a função **whereAreYou()** vai ser retornado a referência para função interna **inner** e atribuida essa referência para **innerFunction** que quando for invocado vai retornar a variável local **justAVar**.
vamos tentar entender isso que está acontecendo aqui, existem duas variáveis com o mesmo nome **justAVar** sendo que uma tem o escopo global a outra tem o escopo local, todas as variáveis locais ficam armazenadas no ambiente e são definidas como local scope nesse exemplo temos apenas uma variável definida assim quando retornarmos a função **inner** vai ser retornada a função com a variável local atachada a mesma.

````js
var innerFunction = whereAreYou();
var result = innerFunction();
console.log(result);
````
essa parte do código da o sentido da coisa, veja que foi criado uma variável **innerFunction** e foi atribuida a função **whereAreYou** lembrando que essa função vai retornar a referência para a função interna **inner** que por sua vez vai retornar a variável local que está atachada a ela, com isso a variável **innerFunction** vai ter a referência para a função **whereAreYou**, depois disso criamos a variável **result** que vai receber a invocação da função **innerFunction** quando chamarmos o **console.log(result)** vamos ter a exibição da variável local que está na função **whereAreYou** com isso já da pra perceber a castaca que foi criada a uma função que retorna a refência para uma função interna que por sua vez retorna a variável local.
vamos entender o que são **CLOSURES**.
- Usando **closures** para implementar um contador mágico.

````js
var count = 0;
function counter() {
  count = count + 1;
  return count;
}

console.log(counter());
console.log(counter());
console.log(counter());
````
no código acima temos o uso de uma variável global **count** que vai ser incrementada pela função **counter()**, isso pode gerar uma série de problemas, como alguém da equipe pode usar o mesmo nome de variável, entre outros... sempre devemos evitar o escolo global.
**código refatorado**
````js
function makeCounter() {
  var count = 0;
  function counter() {
    count = count + 1;
    return count;
}
  return counter;
}
````
criamos uma função que cria um contador chamada **makeCounter()** e inserimos uma função dentro dela chamada **counter()** que vai acessar a variável local **count** e depois disso a função pai vai retornar a referência para função filha, quando fazemos ```` return  counter ```` ai está a **CLOSURE** vamos testar e ver o que acontece.

````js
var doCount = makeCounter();
console.log(doCount());
console.log(doCount());
console.log(doCount());
````
com isso temos a variável **count** encapsulada a única forma de conseguirmos acessar o valor de **count** é através da variável **doCount** e com isso criamos uma closure que vai ajudar no encapsulamento entre outras coisas...
mas retornar uma função de dentro de outra função não é a única maneira de criarmos uma closure, para criar uma closure precisamos ter uma função que executará um código que está fora do seu contexto outra forma de criar closures é passando uma função para outra função por parâmetro a função que será passada vai executar um código em um contexto diferente do que foi criada.

````js
function makeTimer(doneMessage, n) {

  setTimeout(function() {
    alert(doneMessage);
  }, n);

}

makeTimer("Cookies are done!", 1000);
````
podemos ver aqui que a função **makeTimer** recebe dois parâmetros que serão usados em uma função interna a closure é o fato da função interna ter acesso a uma variável que está fora do seu contexto que no caso é **doneMessage**, a closure tem o valor atual da variável e não uma copia da mesma podemos ver nesse novo código o exemplo:

````js
function setTimer(doneMessage, n) {
  setTimeout(function() {
    alert(doneMessage);
  }, n);

    doneMessage = "OUCH!";
}

setTimer("Cookies are done!", 1000);
````
quando a função for chamada a variável **doneMessage** exibirá a mensagem "OUCH!" , pois a closure pega o valor atual e não a referência passada.
